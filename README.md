# Metaplex NFT Collection

A Solana program built with Anchor for managing NFT collections using Metaplex Core. This program provides a whitelist-based creator system and comprehensive NFT collection management features including minting, freezing, thawing, and updating NFTs.

## Features

- **Creator Whitelisting**: Only whitelisted creators can create collections
- **Collection Creation**: Create NFT collections with custom metadata
- **NFT Minting**: Mint NFTs that are automatically frozen and belong to a collection
- **Freeze/Thaw Management**: Control the transferability of NFTs
- **NFT Updates**: Update NFT metadata (e.g., name) by authorized collection creators
- **Authorization System**: Secure PDA-based authority management for collections

## Prerequisites

- [Rust](https://www.rust-lang.org/tools/install) (latest stable version)
- [Anchor](https://www.anchor-lang.com/docs/installation) (v0.32.1 or later)
- [Node.js](https://nodejs.org/) (v18 or later)
- [Yarn](https://yarnpkg.com/) package manager

## Installation

1. Clone the repository:
```bash
cd metaplex-nft-collection
```

2. Install dependencies:
```bash
yarn install
```

3. Build the program:
```bash
anchor build
```

## Program Structure

### Instructions

- **`whitelist_creator`**: Adds a creator to the whitelist (only callable by program upgrade authority)
- **`create_collection`**: Creates a new NFT collection (only whitelisted creators)
- **`mint_nft`**: Mints an NFT in a collection (minted frozen by default)
- **`freeze_nft`**: Freezes an NFT to prevent transfers (collection creator only)
- **`thaw_nft`**: Thaws a frozen NFT to allow transfers (collection creator only)
- **`update_nft`**: Updates NFT metadata like name (collection creator only)

### State Accounts

- **`WhitelistedCreators`**: PDA storing up to 10 whitelisted creator public keys
- **`CollectionAuthority`**: PDA storing collection authority information including creator, collection, NFT name, and NFT URI

### Error Codes

- `CreatorListFull`: The creator whitelist is full (max 10 creators)
- `CreatorAlreadyWhitelisted`: The creator is already in the whitelist
- `NotAuthorized`: The signer is not authorized for this operation
- `CollectionAlreadyInitialized`: The collection account is already initialized
- `AssetAlreadyInitialized`: The asset account is already initialized
- `CollectionNotInitialized`: The collection account is not initialized
- `InvalidCollection`: The provided collection is invalid

## Usage

### Setting Up

1. Configure your Solana CLI:
```bash
solana config set --url localnet  # or devnet/mainnet
```

2. Generate a keypair if you don't have one:
```bash
solana-keygen new
```

3. Airdrop SOL (for localnet/devnet):
```bash
solana airdrop 2 <your-wallet-address>
```

### Running Tests

Run the test suite:
```bash
anchor test --skip-local-validator
```



The tests cover:
- Whitelisting creators
- Creating collections (with authorization checks)
- Minting NFTs
- Freezing and thawing NFTs
- Updating NFT metadata
- Error cases for unauthorized operations



## Deployment

### Local Development

1. Start a local validator:
```bash
surfpool start
```

2. In another terminal, deploy the program:
```bash

anchor test --skip-local-validator
```

### Devnet/Mainnet

1. Update `Anchor.toml` with the appropriate cluster configuration


```

## Project Structure

```
metaplex-nft-collection/
├── programs/
│   └── metaplex-nft-collection/
│       └── src/
│           ├── lib.rs                 # Main program entry point
│           ├── error.rs               # Custom error definitions
│           ├── instructions/          # Instruction handlers
│           │   ├── create_collection.rs
│           │   ├── mint_nft.rs
│           │   ├── freeze_nft.rs
│           │   ├── thaw_nft.rs
│           │   ├── update_nft.rs
│           │   └── whitelist_creator.rs
│           └── state/                 # State account definitions
│               ├── collection_authority.rs
│               └── whitelist_creators.rs
├── tests/
│   └── metaplex-nft-collection.ts     # Test suite
├── migrations/
│   └── deploy.ts                      # Deployment script
└── Anchor.toml                        # Anchor configuration
```

## Dependencies

### Rust Dependencies
- `anchor-lang`: Anchor framework
- `mpl-core`: Metaplex Core program integration

### TypeScript Dependencies
- `@coral-xyz/anchor`: Anchor TypeScript client
- `@metaplex-foundation/mpl-core`: Metaplex Core TypeScript SDK
- `@solana/web3.js`: Solana web3.js library

## Security Considerations

- Only whitelisted creators can create collections
- Collection creators have exclusive authority to freeze, thaw, and update NFTs in their collections
- Creator whitelisting is restricted to the program upgrade authority
- All operations use PDA-based signing for secure authority management

## License

ISC

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For issues and questions, please open an issue on the repository.

