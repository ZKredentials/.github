# ZKredentials - Decentralized, privacy-focused talent verification powered by zk-SNARKs
![zkred-01](https://user-images.githubusercontent.com/110725797/232240026-27dada90-c1b7-4665-91da-e916999c49c0.png)

ZKredentials is a decentralized resume verification platform that empowers anonymous developers by leveraging zero-knowledge proofs (zk-SNARKs), Ethereum blockchain, and the InterPlanetary File System (IPFS). The platform is designed to revolutionize talent discovery and validation while preserving privacy and ensuring security.

## Technology Stack

- Frontend: React and Next.js
- Backend: Node.js
- Smart Contracts: Solidity
- GraphQL APIs: Custom Subgraphs with The Graph
- Authentication: OAuth (GitHub, WorldID)
- IPFS Storage: Client Library

## How it Works

### User Authentication

Users log in using their GitHub or WorldID account via OAuth, allowing the platform to fetch relevant data using the GitHub GraphQL API or verify their unique human status with WorldID. The system can continually add more modules based on user demand for different credibility sources.

### User Registration

Users are minted a resume ERC-721 token when they create their profile for the first time. If a user isn't registered yet, they will not have an ERC-721. Each user can only have one ERC-721 for each module.

### Resume Generation

Users can select special criteria unique to each module to build their resume. Taking GitHub as an example, users select specific GitHub-based criteria for their resumes, which triggers the backend to generate zero-knowledge proofs (ZK proofs) for each criterion, ensuring data verification without revealing sensitive information.

### Serialize ZK proofs

The generated ZK proofs are converted into a suitable format, such as a JSON object.

### Add ZK proofs to IPFS

ZK proofs are uploaded to IPFS via a client library. IPFS then returns a content identifier (CID) for the uploaded proofs.

### Store the CID on-chain

A MetaMask transaction is triggered to store the CID in the respective smart contract depending on the module (GitHub, WorldID), associating it with the user's Ethereum address. An ERC-721 token is minted for the user. This ERC-721 will enable other platforms to build on top of the dApp since all resume information is stored inside it. Once an ERC-721 is minted to the user, it also means the user is registered for that specific module.

### User Profile

The platform displays the user's generated resumes and associated ZK proofs, allowing users to view, edit, delete, and manage their data.

### Resume Verification

Another user can input the Ethereum address or unique proof identifier to verify a resume. The frontend fetches the associated CID from the respective smart contract, retrieves the ZK proofs from IPFS, and verifies their validity through the Verifier.sol smart contract.

### Chat with Anon Devs powered by Push Protocol

Push is integrated into ZKredentials to allow potential employers to reach out and chat with anon developers after viewing their resume on the app for further discussion.
