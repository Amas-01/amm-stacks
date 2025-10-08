# AMM Stacks

An Automated Market Maker (AMM) implementation on the Stacks blockchain. This project provides decentralized token swapping, liquidity provision, and pool management using Clarity smart contracts and a modern Next.js frontend.

## Features

- **Decentralized Token Swapping**: Swap tokens directly from liquidity pools without intermediaries.
- **Liquidity Pools**: Create and manage liquidity pools for token pairs with customizable fees.
- **Liquidity Provision**: Add and remove liquidity to earn trading fees.
- **Wallet Integration**: Connect Stacks wallets for seamless interactions.
- **Real-time Estimates**: Get instant swap output estimates based on pool reserves.

## Core Features

#### `create-pool`
Creates a new liquidity pool for two tokens with a specified fee.
- **Parameters**: `token-0` (trait), `token-1` (trait), `fee` (uint)
- **Requirements**: Tokens must be ordered correctly (token-0 < token-1), pool must not already exist.
- **Returns**: Success confirmation.

#### `add-liquidity`
Adds liquidity to an existing pool.
- **Parameters**: `token-0` (trait), `token-1` (trait), `fee` (uint), `amount-0-desired` (uint), `amount-1-desired` (uint), `amount-0-min` (uint), `amount-1-min` (uint)
- **Logic**: Calculates optimal token amounts based on current pool ratio, transfers tokens to pool, mints liquidity tokens.
- **Returns**: Success confirmation with added amounts.

#### `remove-liquidity`
Removes liquidity from a pool.
- **Parameters**: `token-0` (trait), `token-1` (trait), `fee` (uint), `liquidity` (uint)
- **Logic**: Burns liquidity tokens, transfers proportional token amounts back to user.
- **Returns**: Success confirmation with removed amounts.

#### `swap`
Swaps tokens in a pool using the constant product formula (x * y = k).
- **Parameters**: `token-0` (trait), `token-1` (trait), `fee` (uint), `input-amount` (uint), `zero-for-one` (bool)
- **Logic**: Calculates output amount, deducts fees, updates pool reserves.
- **Returns**: Success confirmation.

## Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- [Clarinet](https://github.com/hirosystems/clarinet) (for contract development and testing)
- [Stacks Wallet](https://wallet.hiro.so/) (for interacting with the dApp)

## Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd amm-stacks-master
   ```

2. Install root dependencies:
   ```bash
   npm install
   ```

3. Install frontend dependencies:
   ```bash
   cd frontend
   npm install
   cd ..
   ```

## Building the Project

### Smart Contracts

1. Check contract syntax and deploy to local simnet:
   ```bash
   clarinet check
   clarinet deployments generate --devnet
   ```

2. Run contract tests:
   ```bash
   npm test
   ```

### Frontend

1. Start the development server:
   ```bash
   cd frontend
   npm run dev
   ```

2. Build for production:
   ```bash
   npm run build
   npm start
   ```

## Testing

Run the full test suite:
```bash
npm run test
```

Run tests with coverage:
```bash
npm run test:report
```

Watch mode for continuous testing:
```bash
npm run test:watch
```

## Deployment

### Testnet Deployment

1. Configure your Stacks account in `deployments/default.testnet-plan.yaml`

2. Deploy to testnet:
   ```bash
   clarinet deployments apply --testnet
   ```

## Usage

1. **Connect Wallet**: Use the Hiro Wallet to connect to the dApp.

2. **Swap Tokens**: On the home page, use the swap interface to exchange tokens instantly.

3. **Manage Pools**: Navigate to the `/pools` page for pool management:
   - **View Pools**: See all existing liquidity pools.
   - **Create Pool**: Create a new liquidity pool for a token pair.
   - **Add Liquidity**: Provide tokens to a pool to earn trading fees.
   - **Remove Liquidity**: Withdraw your tokens and accumulated fees from a pool.

All core functions (create-pool, add-liquidity, remove-liquidity, swap) are implemented as smart contract functions and accessible through the frontend components on the respective pages.

## Architecture

- **Smart Contracts**: Written in Clarity, Stacks' smart contract language. Implements AMM logic with constant product formula.
- **Frontend**: Next.js with React, TypeScript, and Tailwind CSS. Uses Stacks.js for blockchain interactions.
- **Testing**: Vitest for unit testing contracts and integration tests.
- **Deployment**: Clarinet for managing contract deployments across networks.




