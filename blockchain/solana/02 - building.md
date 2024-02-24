i am using the [solana cookbook](https://solanacookbook.com/) as reference to learn basic concepts, solana cli

## Stuff to Get Started with TS or JS
1.  `npm install --save @solana/web3.js` 
2. `npm install --save @solana/spl-token`
3. `npm install --save @solana/wallet-adapter-wallets \ @solana/wallet-adapter-base`
4. also, install Rust
5. install the Solana CLI, follow instructions online

## Clusters in SOLANA
- clusters are basically simulated blockchain networks that are used for testing
- solana has various clusters

3 Popular Clusters are :-
1. **Devnet**: Devnet serves as a playground for anyone who wants to take Solana for a test drive, as a user, token holder, app developer, or validator. Think of this as the local development environment.
2. **Testnet**: Testnet is where we stress-test recent release features on a live cluster, particularly focused on network performance, stability and validator behavior. Think of this as a test environment.
3. **Mainnet Beta**: This is the main network where Solana apps can be deployed and interacted with, using real SOL. Think of this as the live environment.

## Wallet / Keypair

A wallet is your keypair - this is what holds the SOL tokens. A keypair has a public and private key.
#### Keys

- **Public Key**: This publicly available key is how others can send you transactions.
- **Private Key**: This allows you to prove ownership and use the cryptocurrency associated with your public address. Never share this with anyone.

Think of keys like a mailbox. The public key is the address of the box, where anyone can send drop mail (transactions) in the slot. Only the person with the private key can open the mailbox (prove ownership) and read the messages (use the transactions).

## What is an RPC?
It stands for **REMOTE PROCEDURE CALL**.. it is an endpoint where you can send requests to get blockchain data

## Generating a Keypair and Connecting 
```js
const { PublicKey, Keypair, Connection, clusterApiUrl } = require("@solana/web3.js");

const newPair = Keypair.generate();
const publicKey = new PublicKey(newPair.publicKey).toString();
const privateKey = newPair.secretKey;
const connection = new Connection(clusterApiUrl("devnet"), "confirmed");

console.log(`The Public key is ${publicKey}`)
console.log(connection);
```

- solana web3.js returns the private key in a Uint8 Array form and not in base58.
- to convert it into a normal string private key form, you can use the `bs58` library and do `bs58.encode(privateKey)` to do so.
- here the `PublicKey()` is a class to access the public key from a keypair

## Getting Wallet Balance
**STEPS  -**
1. Make a connection to the cluster
2. Get the keypair (you can either use your earlier created keypair or derive your keypair using the private key)
3. Use the getBalance method and input in the public key

```js
const { PublicKey, Keypair, Connection, clusterApiUrl, LAMPORTS_PER_SOL } = require("@solana/web3.js");

const newPair = Keypair.generate();
const publicKey = new PublicKey(newPair.publicKey);
const privateKey = newPair.secretKey;
const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
  
const getWalletBalance = async() => {
    try{
        const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
        console.log("Connection Object  : ", connection);  
        const keypair = await Keypair.fromSecretKey(privateKey);
        const walletBalance = await connection.getBalance(new PublicKey(keypair.publicKey));
        console.log(`Wallet Balance  :  ${parseInt(walletBalance / LAMPORTS_PER_SOL)} SOL`)
    } catch (err){
        console.log(err);
    }
}
  
getWalletBalance();
```

```js
const { PublicKey, Keypair, Connection, clusterApiUrl, LAMPORTS_PER_SOL } = require("@solana/web3.js");

const newPair = Keypair.generate();
const publicKey = new PublicKey(newPair.publicKey);
const privateKey = newPair.secretKey;
const connection = new Connection(clusterApiUrl("devnet"), "confirmed");
  
const getWalletBalance = async() => {
    try{
        // you have already made a connection above so you can use it and a keypair is also with us so simply get the wallet balance
        const balance = await connection.getBalance(publicKey);
        console.log(`Wallet Balance : ${parseInt(balance / LAMPORTS_PER_SOL)} SOL`);
    } catch (e) {
        console.log(e);
    }
}

getWalletBalance();
```

both these codes are exactly the same just coded in a different manner 

## Airdropping SOL in your Wallet
```js
const requestAirdrop = async() => {
    try {
        const airdropSignature = await connection.requestAirdrop(newPair.publicKey, 2 * LAMPORTS_PER_SOL);
        await connection.confirmTransaction(airdropSignature);
        getWalletBalance();
    } catch (err) {
        console.log(err)
    }
}
  
requestAirdrop()
```

## Common Issue 
when you run your code quite a lot of times on the devnet you get rate limitted for a lot of test SOL airdrop requests and then you cant do shit
to fix, you can start up your own block validator in the terminal using the Solana CLI
here's what to do - 

type in the terminal  `solana-test-validator`
this will spin up a local validator node with unlimited airdrops and no rate limits
to connect to this, in the Connection you made remove the clusterApiUrl stuff and it should look like this
`const connection = new Connection(your-rpc-url-here, "confirmed")`

## Transferring SOL from one wallet to another

STEPS - 
1. Airdrop some SOL in 1st wallet
2. generate 2nd wallet
3. add a new transaction where you input both the public addresses and the amount of SOL to transfer
4. then you need to sign the transaction using your connection object, the transaction you just created and the keypair of 'from' wallet (basically the private key is needed to sign the transaction)
5. you console.log this signature and check it on the devnet explorer

```js
// Import Solana web3 functionalities

const {
    Connection,
    PublicKey,
    clusterApiUrl,
    Keypair,
    LAMPORTS_PER_SOL,
    Transaction,
    SystemProgram,
    sendAndConfirmTransaction
} = require("@solana/web3.js");
  
// Making a keypair and getting the private key
const newPair = Keypair.generate();
console.log(newPair.secretKey);
const secretKey = new Uint8Array(
    [
        59, 197, 190, 205,  60, 176, 129,  20, 232, 201,  99,
  199, 246, 192, 193, 149,  27,  30, 160, 156, 145,  51,
   11, 182, 144,   6,  97, 217,  87,  17, 183, 161,  13,
  241, 223,  17, 244,  20, 109, 116, 103, 255,  92,  28,
   88,  36, 226, 217, 103, 144, 100,  22, 100,  18, 236,
  226,  60, 127,   7, 206, 137,  24, 131, 187
    ]            
);
  
const transferSol = async() => {
    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");  
    // Get Keypair from Secret Key
    var from = Keypair.fromSecretKey(secretKey);
      
    // (Optional) - Other things you can try:
    // 1) Form array from userSecretKey
    // const from = Keypair.fromSecretKey(Uint8Array.from(userSecretKey));
    // 2) Make a new Keypair (starts with 0 SOL)
    // const from = Keypair.generate();
  
    // Generate another Keypair (account we'll be sending to)
    const to = Keypair.generate();
 
    // Aidrop 2 SOL to Sender wallet
    console.log("Airdopping some SOL to Sender wallet!");
    const fromAirDropSignature = await connection.requestAirdrop(
        new PublicKey(from.publicKey),
        2 * LAMPORTS_PER_SOL
    );
  
    // Latest blockhash (unique identifer of the block) of the cluster
    let latestBlockHash = await connection.getLatestBlockhash();
  
    // Confirm transaction using the last valid block height (refers to its time)
    // to check for transaction expiration
    await connection.confirmTransaction({
        blockhash: latestBlockHash.blockhash,
        lastValidBlockHeight: latestBlockHash.lastValidBlockHeight,
        signature: fromAirDropSignature
    });  

    console.log("Airdrop completed for the Sender account");  

    // Send money from "from" wallet and into "to" wallet
    var transaction = new Transaction().add(
        SystemProgram.transfer({
            fromPubkey: from.publicKey,
            toPubkey: to.publicKey,
            lamports: LAMPORTS_PER_SOL / 100
        })
    );
  
    // Sign transaction
    var signature = await sendAndConfirmTransaction(
        connection,
        transaction,
        [from]
    );
    console.log('Signature is', signature);
}  

transferSol();
```


## Node Provider?
**NODE** - 
- a node is a program running on a physical computer system 
- connects with the blockchain network, sends and receives transactions and validates TXs
- the blockchain is made up of nodes and hence decentralized
- only way to access blockchain information
- nodes are hard to manage and setup

- so **NODE PROVIDERS** offer a way to access blockchain information without running a node
- in our case, Phantom Wallet provides us with the connection to Solana network

## Wallet Integration using solanaweb3js and React

```ts
import React from 'react';
import './App.css';
import {
  PublicKey,
  Transaction,
} from "@solana/web3.js";
import {useEffect , useState } from "react";
  
// create types
type DisplayEncoding = "utf8" | "hex";
  
type PhantomEvent = "disconnect" | "connect" | "accountChanged";
type PhantomRequestMethod =
  | "connect"
  | "disconnect"
  | "signTransaction"
  | "signAllTransactions"
  | "signMessage";
  
interface ConnectOpts {
  onlyIfTrusted: boolean;
}
  
// create a provider interface (hint: think of this as an object) to store the Phantom Provider
interface PhantomProvider {
  publicKey: PublicKey | null;
  isConnected: boolean | null;
  signTransaction: (transaction: Transaction) => Promise<Transaction>;
  signAllTransactions: (transactions: Transaction[]) => Promise<Transaction[]>;
  signMessage: (
    message: Uint8Array | string,
    display?: DisplayEncoding
  ) => Promise<any>;
  connect: (opts?: Partial<ConnectOpts>) => Promise<{ publicKey: PublicKey }>;
  disconnect: () => Promise<void>;
  on: (event: PhantomEvent, handler: (args: any) => void) => void;
  request: (method: PhantomRequestMethod, params: any) => Promise<unknown>;
}
  
 /**
 * @description gets Phantom provider, if it exists
 */
 const getProvider = (): PhantomProvider | undefined => {
  if ("solana" in window) {
    // @ts-ignore
    const provider = window.solana as any;
    if (provider.isPhantom) return provider as PhantomProvider;
  }
};
  
export default function App() {
  // create state variable for the provider
  const [provider, setProvider] = useState<PhantomProvider | undefined>(
    undefined
  );
  
  // create state variable for the wallet key
  const [walletKey, setWalletKey] = useState<String | undefined>(
  undefined
  );
  
  // this is the function that runs whenever the component updates (e.g. render, refresh)
  useEffect(() => {
    const provider = getProvider();
  
    // if the phantom provider exists, set this as the provider
    if (provider) setProvider(provider);
    else setProvider(undefined);
  }, []);
  
  /**
   * @description prompts user to connect wallet if it exists.
   * This function is called when the connect wallet button is clicked
   */
  const connectWallet = async () => {
    // @ts-ignore
    const { solana } = window;
  
    // checks if phantom wallet exists
    if (solana) {
      try {
        // connects wallet and returns response which includes the wallet public key
        const response = await solana.connect();
        console.log('wallet account ', response.publicKey.toString());
        // update walletKey to be the public key
        setWalletKey(response.publicKey.toString());
      } catch (err) {
          console.log(err);
      }
    }
  };

  /**
   * @description disconnects wallet if it exists.
   * This function is called when the disconnect wallet button is clicked
   */
  const disconnectWallet = async () => {
    // @ts-ignore
    const { solana } = window;
    // checks if phantom wallet exists
    if (solana) {
      try {
        await solana.disconnect();
        setWalletKey(undefined)
        }
      } catch (err) {
          console.log(err);
      }
    }
  };
  
  // HTML code for the app
  return (
    <div className="App">
      <header className="App-header">
        <h2>Connect to Phantom Wallet</h2>
      {provider && !walletKey && (
      <button
        style={{
          fontSize: "16px",
          padding: "15px",
          fontWeight: "bold",
          borderRadius: "5px",
        }}
        onClick={connectWallet}
      >
        Connect Wallet
      </button>
        )}
        {provider && walletKey && (
            <div>
              <p>{walletKey}</p>
              <button
                style={{
                  fontSize: "16px",
                  padding: "15px",
                  fontWeight: "bold",
                  borderRadius: "5px",
                  position: "absolute",
                  top: "28px",
                  right: "28px"
                }}
                onClick={disconnectWallet}
              >
                Disconnect Wallet
              </button>
            </div>
        )}
        {!provider && (
          <p>
            No provider found. Install{" "}
            <a href="https://phantom.app/">Phantom Browser extension</a>
          </p>
        )}
        </header>
    </div>
  );
}
```


## Solana working?
- solana programs are written in C, C++, Rust and deployed on the Solana Blockchain.
- Javascript SDK, Solana CLI, Interface, Rust SDK etc. are used to send transactions and queries to these programs on the blockchain through node providers
- An application interacts with a Solana cluster by sending it [transactions](https://docs.solana.com/developing/programming-model/transactions) with one or more [instructions](https://docs.solana.com/developing/programming-model/transactions#instructions). The Solana [runtime](https://docs.solana.com/developing/programming-model/runtime) passes those instructions to [programs](https://docs.solana.com/terminology#program) deployed by app developers beforehand. An instruction might, for example, tell a program to transfer [lamports](https://docs.solana.com/terminology#lamport) from one [account](https://docs.solana.com/developing/programming-model/accounts) to another or create an interactive contract that governs how lamports are transferred. In our example, we are going to send an instruction that _**says hello**_ to the deployed Solana program. Instructions are executed sequentially and atomically for each transaction. If any instruction is invalid, *all account changes in the transaction are discarded*.  (copied from docs)
- **READ ALL STUFF OVER AT THE SOLANA DOCS**

## What are Programs?
- programs are a set of instructions built in Rust, C, C++, TS to give instructions to a dApp and make them work accordingly
- another word for SMART CONTRACTS

# Tokens
- tokens on Solana are called SPL Tokens
- They can be either fungible or non-fungible
- created using SPLToken Library
- SPL stands for **Solana Program Library**
- Terminology - Fungible Tokens = SPL Tokens, Non Fungible Tokens = NFTs

**Fungible assets** are interchangeable and can be swapped with other fungible tokens.

Some real-life examples are Euros, INR, and Dollars. Each of these currencies can be exchanged for one another, making them fungible. The same applies to **fungible tokens**.

**Non-fungible assets** are unique assets that cannot be interchanged for one another.

For example, you may have two cupcakes of the same flavor made at two different bakeries, but they would still not be the same since there is a unique aspect associated with the owner/creator of the cupcake.


## NFTs
Non-fungible tokens are unique digital assets whose ownership and transfer can be recorded on the blockchain. Examples of digital assets can be images, domains, and any unique digital assets that can be recorded on the blockchain.

Metaplex protocol is also an essential NFT ecosystem for marketplaces, games, arts and collectibles on Solana.

**HOW DO NFTs GO UP FOR SALE?**
- first the owner needs to deploy a NFT Standard contract on the blockchain of their choice by specify the name and symbol for the NFT
- The next step is to mint the NFT. They are minted in form of tokens using mint() function
- The next step is Selling the tokens 

## More on PoH
- What does ETHEREUM do? It takes the standardized centralized time in UTC to validate the transactions in the order they were received. This is slow and also beats the concept of Decentralization
- So to tackle, Solana created it's own time. It validates nodes using **Verifiable Delay Function(VDF)**, every block producer has to go through this VDF
- each tx is marked with a unique hash and time, this info gives a verifiable order of events
- each node is able to decipher these cryptographic time so they can validate the time locally
- an upper bound of time is set, and the lower bound is gotten from the previous hashes
- this vdf wont tell you that its 12:02:15 pm but will tell you exactly when in past and future of global state machine a transaction occured

## Accounts
- everything in Solana is handled by accounts, you can [read here](https://solana.wiki/docs/solidity-guide/accounts/)
#### Details on Accounts

Solana programs are essentially stateless. This means they do not store any information. So, where do all the variables and states get stored? - in the accounts.

Accounts are responsible for holding all types of data on the Solana blockchain. This data can be an executable smart contract as a whole or variables/data associated with the smart contract. Accounts also just refer to the accounts on your wallet that be used to store, send and receive tokens.
With the help of accounts, SOLANA can run multiple transactions parallelly unlike Ethereum

#### Types of accounts

- Non-executable account: Stores different types of data such as program variables, user balances, etc.
- Executable account: This is used only for storing program code.

#### Account Ownership

Every time we create an account using a wallet, the created account is initialized to be _owned_ by a built-in program called the System program. Each account includes some metadata such as owner(to define access control over the account), is executable(y/n), and other such parameters.

#### Rent
we need to pay rent for keeping our program on the chain, if we have a balance of 2 SOL in program, then it is considered rent-exempted

## Associated Token Account Program
example : You have a wallet on Solana chain, then you will have a public address for your account.
then all the tokens you own have a different account and address. different wallets have different addresses for the same token, but the mint account for all the wallets is same.
now, if i want to send USDC tokens to someone and I only have the public address of the person's wallet, then HOW SHIT WILL HAPPEN?
Here comes the Associated Token Account Program, it maps the token accounts to the wallet


## Minting SPL Tokens
- we need to install the `spl-token library` first
- then you can see the resources [here](https://medium.com/@jorge_londono_31005/understanding-solanas-mint-account-and-token-accounts-546c0590e8e)

STEPS - 
- airdrop some sol into wallet for fees
- create mint account for token
- create tokenAccount for from and to wallet
- mint token to from tokenAccount
- then transfer tokens from 'from' to 'to'
- the code is given below

```js
import { clusterApiUrl, Connection, Keypair, LAMPORTS_PER_SOL } from '@solana/web3.js';

import { createMint, getOrCreateAssociatedTokenAccount, mintTo, transfer } from '@solana/spl-token';

  

(async () => {

    // Step 1: Connect to cluster and generate a new Keypair

    const connection = new Connection(clusterApiUrl("devnet"), "confirmed");

    const fromWallet = Keypair.generate();

    const toWallet = Keypair.generate();

  

    // Step 2: Airdrop SOL into your from wallet

    const airdropSignature = await connection.requestAirdrop(fromWallet.publicKey, 2*LAMPORTS_PER_SOL);

    await connection.confirmTransaction(airdropSignature, { commitment : "confirmed" });

    // Step 3: Create new token mint and get the token account of the fromWallet address

    //If the token account does not exist, create it

    const mint = await createMint(connection, fromWallet, fromWallet.publicKey, null, 9); // public key of mint account

    const fromTokenAccount = await getOrCreateAssociatedTokenAccount(   // it returns the public address of token account

        connection,

        fromWallet,

        mint,

        fromWallet.publicKey

    )

    //Step 4: Mint a new token to the from account

    let signature = await mintTo(connection, fromWallet, mint, fromTokenAccount.address, fromWallet.publicKey, 1000000000, [])

    console.log("mint tx  : ", signature);

  

    //Step 5: Get the token account of the to-wallet address and if it does not exist, create it

    const toTokenAccount = await getOrCreateAssociatedTokenAccount(connection, fromWallet, mint, toWallet.publicKey)

  

    //Step 6: Transfer the new token to the to-wallet's token account that was just created

    // Transfer the new token to the "toTokenAccount" we just created

    signature = await transfer(connection, fromWallet, fromTokenAccount.address, toTokenAccount.address, fromWallet.publicKey, 1000000000, [])

    console.log("transfer fx  : ", signature)

})();
```

## Minting NFTs using MetaPlex Candy Machine
**Why Solana for NFTs?**

Minting a bunch of NFTs is really pricey on other networks and thus we will be minting our NFTs on Solana Network.

**Who will pay for minting?**

If the minters want to mint a huge number of NFTs (say 10,000,000), it will be very costly for the minter to undertake the cost of minting. Thus, we will be building our own Candy Machine where the price will be paid by the buyer of the NFT.

The candy machine here can be considered analogous to a real-world candy machine where we fill in the machine with candies (NFTs) beforehand & the customers can buy the candy (NFT) by paying the price set earlier for these NFTs.

**What will we use?**

We will use the de-facto standard for NFTs on Solana - Metaplex.

**What is Metaplex and what is Candy Machine?**

Metaplex is a collection of tools, smart contracts, and more designed to make the process of creating and launching NFTs easier.

Metaplex is a protocol built on top of Solana that allows:

- Creating/Minting non-fungible tokens (NFTs)
- Starting a variety of auctions for primary/secondary sales
- Visualizing NFTs in a standard way across wallets and applications

The candy-machine is an on chain Solana program (smart contract) that governs fair mints. It will help interact with the candy-machine program. We will be using it to:

- Upload our images and metadata to Arweave, then register them on the solana block-chain
- Verify the state of our candy-machine
- Mint individual tokens

**SETUP?**
- Sugar CLI
- Solana CLI
- ts-node
- node

we will have to deal with the CLI, because we still haven't learnt to write contracts in SOLANA using rust
so open up your terminal and type in these commands

`solana-keygen new --outfile ./wallet.json`  to create new wallet
`solana config set --keypair ./wallet.json` to associate it with solana and sugar CLI
`solana config set --url https://api.devnet.solana.com` to connect to devnet
`solana airdrop 1`   to fund wallet with 1 SOL


Go to the Metaplex docs to study about the `config.json` you need to create 
A NFT has 2 things, a .png and a .json file for its metadata containing the name, description, value, attributes etc.

**NEXT STEPS -**
1. VERIFY AND UPLOAD - `sugar validate` and `sugar upload`
2. DEPLOY using `sugar deploy` and `sugar verify`
3. MINT using `sugar mint`

[EVERYTHING IS MENTIONED HERE](https://docs.metaplex.com/deprecated/candy-machine-js-cli/introduction)

## UI
we can build a UI for candy machine using Metaplex Umi. refer docs for info