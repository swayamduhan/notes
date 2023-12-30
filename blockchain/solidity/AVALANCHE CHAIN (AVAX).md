
- faster confirmation times, takes 1 second
- highly scalable
- avalanche network consists of 3 primary blockchains - 
	- Platform chain or P chain to manage validators and create subnets or new blockchains (snowman consensus)
	- Exchange chain or X chain to transfer assets ( avalanche consensus protocol)
	- Contract chain or C chain as smart contract blockchain (snowman consensus)
- AVAX - native token, to maintain price the avax used as fees is burned
- Snowtrace is the block explorer ( same as etherscan and polyscan )

- AWS and Ava Labs have formed an exciting partnership to accelerate the adoption of the groundbreaking Avalanche blockchain platform 🤝 This collaboration is revolutionizing the blockchain ecosystem by leveraging AWS's cutting-edge cloud solutions, including Amazon EC2, to deliver consistent millisecond performance for transactions on Avalanche ⏱️With AWS's global infrastructure and commitment to compliance, launching validator nodes and Subnets has never been easier, empowering developers to build and scale their applications effortlessly. This strategic alliance between AWS and Ava Labs showcases the immense potential of Avalanche and serves as a compelling reason for others to join the platform and experience the benefits of this powerful partnership firsthand
- recently integrated with shopify for their nft library
- trader joe's XYZ is a DEX to swap, yield farming and stake
## Avalanche P-Chain: The Backbone of the Network

The P-Chain is like the backstage manager of the Avalanche platform, responsible for all the heavy lifting 🏋️ and behind-the-scenes work necessary to keep the network running smoothly. This chain is the ultimate multitasker, managing everything from creating and managing new blockchains and subnets to staking operations that secure the network and maintain consensus across all subnets on the Avalanche network.

By locking up AVAX tokens as collateral, users can become validators or delegate their tokens to an existing validator to participate in the consensus process. Validators are like the guardians of the network, verifying transactions and adding new blocks to the chain, and are rewarded with AVAX tokens for their hard work 💰

But that's not all the P-Chain can do. It also supports the creation of custom subnets, which are like separate playgrounds with their own unique set of rules and parameters. You can use them to experiment with different execution environments or create private networks for your specific needs.

Think of the P-Chain as the backbone of the Avalanche platform, providing the infrastructure and governance mechanisms necessary to maintain a secure and decentralized network 🌐🔒

The P-Chain is an instance of the Platform Virtual Machine. To get started with the P-Chain, you can use the [P-Chain API](https://docs.avax.network/apis/avalanchego/apis/p-chain) which supports the creation of new blockchains and Subnets, the addition of validators to Subnets, staking operations, and other platform-level operations.

## Enter the Avalanche X-Chain

This powerful chain is responsible for the creation and trading of digital smart assets, known as Avalanche Native Tokens, which can represent anything from cryptocurrencies to stocks, bonds, and even real estate 🏡. With the user-friendly [X-Chain API](https://docs.avax.network/apis/avalanchego/apis/x-chain), creating and trading these tokens has never been easier.

But the X-Chain isn't just easy to use - it's also lightning-fast ⚡ and incredibly affordable. With high throughput and low transaction fees, you can trade assets quickly and efficiently. And with the added benefit of atomic swaps, there's no need to rely on centralized exchanges or intermediaries to exchange one asset for another.

## Avalanche C-Chain: Decentralized Applications Made Easy

Welcome to the Avalanche C-Chain, the heart of decentralized application (dApp) development on Avalanche! As an implementation of the Ethereum Virtual Machine (EVM), the C-Chain supports the creation and execution of smart contracts written in Solidity. This makes it easy for developers familiar with Ethereum to build and deploy decentralized applications (dApps) on Avalanche - that’s you! 😉

With its high performance and low transaction fees, the C-Chain is the perfect platform for building high-volume dApps. It offers sub-second finality, and it’s low gas fees mean you won't break the bank when developing and deploying your applications 💸

The C-Chain also supports interoperability with other blockchains, including Ethereum, thanks to cross-chain bridges 🌉 This means that assets and data can be transferred between the two chains, opening up new possibilities for decentralized finance (DeFi) and other use cases.

To get started with the C-Chain, simply use the [C-Chain API](https://docs.avax.network/apis/avalanchego/apis/x-chain) which provides a similar interface to the Ethereum JSON-RPC API, making it easy for developers to interact with the C-Chain using their existing tools and libraries.


## Example hardhat config file for using avalanche

```
require("@nomicfoundation/hardhat-toolbox");

  

const FORK_FUJI = false

const FORK_MAINNET = false

let forkingData = undefined;

  

if (FORK_MAINNET) {

  forkingData = {

    url: 'https://api.avax.network/ext/bc/C/rpcc',

  }

}

if (FORK_FUJI) {

  forkingData = {

    url: 'https://api.avax-test.network/ext/bc/C/rpc',

  }

}

  
  

/** @type import('hardhat/config').HardhatUserConfig */

module.exports = {

  solidity: "0.8.18",

  networks: {

    hardhat: {

      gasPrice: 225000000000,

      chainId: !forkingData ? 43112 : undefined, //Only specify a chainId if we are not forking

      forking: forkingData

    },

    fuji: {

      url: 'https://api.avax-test.network/ext/bc/C/rpc',

      gasPrice: 225000000000,

      chainId: 43113,

      accounts: [

        // "YOUR PRIVATE KEY HERE"

      ]

    },

    mainnet: {

      url: 'https://api.avax.network/ext/bc/C/rpc',

      gasPrice: 225000000000,

      chainId: 43114,

      accounts: [

        // "YOUR PRIVATE KEY HERE"

      ]

    }

  }

}
```

