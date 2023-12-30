

## Converting address to payable

easy way - payable(_addressHere_)
bigger way - address(uint160(_originalAddress_))
this was used in earlier versions before the payable modifier came into picture. to convert an address into payable we need to first convert it into a unsigner integer of 160bits

## Fallback functions
used to handle function calls that dont exist or if ether has been sent to address without any function call

- BEFORE 0.6.0
	 function() external payable
- AFTER 0.6.0
	 fallback() external payable


## Abstract Contracts (just like abstract classes, blueprints)
Like any OOPS language, Solidity provides abstract contracts. Abstract contracts are similar to abstract classes in OOPS languages such as Java and Typescript. There is no abstract term in Solidity for establishing an abstract contract. However, if a contract includes unimplemented functions, it becomes abstract.

- Instance of an abstract cannot be created
- Derived contract will implement the abstract function and use them as and when required
- Contracts that have at least one function without its implementation is abstract
- Also in the case when we don’t intend to create a contract directly we can consider the contract to be abstract
- Abstract contracts are used as base contracts so that the child contract can inherit and utilize its functions
- Any derived contract inherited from it should provide an implementation for the incomplete functions, and if the derived contract is also not implementing the incomplete functions then that derived contract will also be marked as abstract.

The abstract contract is an abstract (incomplete / hypothetical) design of a contract. The implementation of contract provides the implementation of the abstract function in it. Once the abstract contract is created, you need to extend it by using is keyword.

```
pragma solidity ^0.5.0;

contract CalciAbstract {
   function getResult() public view returns(uint);
}
contract Compute is CalciAbstract {
   function getResult() public view returns(uint) {
      uint a = 1;
      uint b = 2;
      uint result = a + b;
      return result;
   }
}

```

## Interface
Usually a set of rules defined for created something. eg: ERC20 Tokens
Interfaces can have only unimplemented functions. Also, they are neither compiled nor deployed. They are also called pure abstract contracts

- Cannot implement any of their functions. All interface functions are implicitly virtual
- Are defined with the keyword interface
- Cannot inherit other contracts or interfaces (after solidity 6.0.0 interfaces can inherit from interfaces) but other contracts can inherit from interfaces
- Function state mutability can be pure , view , payable or default(blank)
- Fallback functions cannot be defined in an Interface
- Interface functions are implicitly "virtual"
- Cannot define a constructor
- Functions can be defined external only
- Cannot have state variables but local variables definition is allowed

```
// Interface for a token contract
interface ERC20Token {
    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address recipient, uint256 amount) external returns (bool);
    event Transfer(address indexed from, address indexed to, uint256 value);
}
```

```
contract MyToken is ERC20Token {                   // is ERC20Token is not mandatory
    uint256 private _totalSupply;

    // Constructor sets the initial total supply
    constructor(uint256 initialSupply) public {
        _totalSupply = initialSupply;
    }

    function totalSupply() external view returns (uint256) {
        return _totalSupply;
    }

    // Other ERC-20 functions and implementations...
}

```

```
// Contract that uses the ERC20Token interface
contract MyContract {
    ERC20Token public token;

    constructor(address tokenAddress) public {
        token = ERC20Token(tokenAddress);
    }

    function getTokenTotalSupply() public view returns (uint256) {
        return token.totalSupply();
    }

    function getMyTokenBalance() public view returns (uint256) {
        return token.balanceOf(msg.sender);
    }

    function transferTokens(address to, uint256 amount) public returns (bool) {
        return token.transfer(to, amount);
    }
}

```

## Abstract class and Inheritance Comparison

It's the same as in most other object-oriented programming languages:

- Interface only declares functions, cannot implement them
- Abstract class can declare functions (same as interface) as well as implement them.
- Both cannot be instantiated
- Both need to be implemented/inherited from other contract

## ERC20 Tokens
A set of rules set for creating tokens. we need to have certain functions in our token contract according to the interface.
Read more at openzeppelin and use its ERC20 Library :)

Basic setup :
```
// contracts/GLDToken.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract GLDToken is ERC20 {
    constructor(uint256 initialSupply) public ERC20("Gold", "GLD") {
        _mint(msg.sender, initialSupply);
    }
}
```
you can also set the number of decimals for your token


this is the super hook used to extend the contract and add additional functionalities, eg : here a valid recipient function is added after the functionalites of \_beforeTokenTransfer go through
```
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract ERC20WithSafeTransfer is ERC20 {
    function _beforeTokenTransfer(address from, address to, uint256 amount)
        internal virtual override
    {
        super._beforeTokenTransfer(from, to, amount);

        require(_validRecipient(to), "ERC20WithSafeTransfer: invalid recipient");
    }

    function _validRecipient(address to) private view returns (bool) {
        ...
    }

    ...
}
```


