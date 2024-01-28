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

