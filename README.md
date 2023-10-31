# Grabit
**Grabit** is a blockchain built using the Cosmos SDK and Tendermint and created with Starport. 
The project aims to be a centralized HUB where users can create, mint, and transfer NFT tokens between different blockchains.

## Get started

### 1. System overview

The system consists of 4 components.
- Grabit chain that has an NFT module with only 1 function: CreateNFT
- Ethereum smart contracts where users mint and lock NFT.
- Grabit's Go client, which listens to LockNFT events on Ethereum and calls CreateNFT on the Grabit chain.
- Website where users use Metamask and Keplr to interact with the system.

### 2. Installation and running
Grabit requires Golang 1.16 or higher and starport. To run the blockchain on your local machine, go to the root of the project and run the command
```
starport chain serve
```
For the other components, please follow the instruction in each repos.

### 3. Usage

- At the beginning, users will go to the website and mint a predefined ERC721 NFT on the Ethereum testnet (Ropsten).
- After that, the NFT's creator will interact with the Locker smart contract. He will call the lock method, which will
    - Send the ERC721 NFT to Locker contract with the Grabit address of the new owner from Cosmos.
    - Emit the LockNFT event
- The Go client of Grabit will listen to the LockNFT event, parse the message, then call Grabit's NFT module's function CreateNFT.
- If everything goes well, a new NFT will be created on the Grabit chain with all the data from the previous ERC721 token.
