# Smart Contract Lottery

A compact, audit-friendly raffle (lottery) example written in Solidity and tested with Foundry. The contract uses Chainlink VRF v2.5 to obtain verifiable randomness when selecting a winner.

## Deployed Contract

- [Sepolia Etherscan: 0x717A7DF2178c19Be012D58dc3813C19B1351290B](https://sepolia.etherscan.io/address/0x717A7DF2178c19Be012D58dc3813C19B1351290B)

## Prerequisites

- Foundry (`forge`, `cast`, `anvil`) installed and configured
- Solidity 0.8.x toolchain (project uses 0.8.19)
- Optional: Sepolia RPC provider (Alchemy/Infura) and Etherscan API key for verification

## Setup

1. Clone the repository and enter its root.
2. Create a `.env` file with:
   ```
   SEPOLIA_RPC_URL=<your-sepolia-rpc-url>
   ETHERSCAN_API_KEY=<your-etherscan-api-key>
   ```
3. Install project dependencies:
   ```
   make install
   ```

## Build & Test

- Build:
  ```
  make build
  ```
- Test:
  ```
  make test
  ```
  (Or use `forge build` / `forge test` directly.)

## Local Development

- Use `anvil` for local testing. The helper config deploys `VRFCoordinatorV2_5Mock` and a `LinkToken` mock when running locally.
- Tests run against mocks by default on chain id 31337.

## Chainlink VRF (Sepolia) Notes

- The contract requires a funded VRF subscription. For Sepolia:
  1. Create a subscription and fund it with LINK (or use scripts provided).
  2. Add the deployed raffle contract as a consumer of that subscription.
- The deployment script will attempt to create/fund a subscription when `config.subscriptionId == 0`. Verify the `subscriptionId` in `HelperConfig` before production use.

## Deployment

- Using Makefile:
  ```
  make deploy-sepolia
  ```
- Or directly:
  ```
  forge script script/DeployRaffle.s.sol:DeployRaffle --rpc-url $SEPOLIA_RPC_URL --account <account> --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
  ```


