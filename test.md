Here is a comprehensive `README.md` based on the content analyzed from the provided files:

# GMI Launchpad Contracts

This repository contains the smart contracts for the **GMI Launchpad** project, which enables the creation of various types of ERC-721 NFT collections with different features like whitelisting, public sales, pausing, and refund mechanisms.

The contracts are primarily written in **Solidity `0.8.22`**.

## Project Status

The GMI Launchpad Contracts repository is under active maintenance by **Energi**.

## Contract Types Overview

The launchpad supports several token contract types to accommodate different project needs:

| Contract Name Family | Base Standard | Refundable? | Marketplace Restriction? | Key Feature |
| :--- | :--- | :--- | :--- | :--- |
| **Standard** (`GMIERC721`) | ERC721A | No | No | Standard minting, ERC-721 with gas optimization for batch minting. |
| **100% Refundable** (`GMIERC721R`) | ERC721Enumerable | Yes (Full Refund) | No | Holders can refund tokens for the full price paid by burning the NFT. |
| **80% Refundable** (`GMIERC721R80`) | ERC721Enumerable | Yes (80% Refund) | No | Holders can refund 80% of the price paid. Owner keeps 20%. |
| **ERC721C** (`GMIERC721C`) | ERC721A | No | Yes | Standard minting with trading restricted to whitelisted marketplaces via `OperatorFilter`. |
| **100% Refundable C** (`GMIERC721RC`) | ERC721Enumerable | Yes (Full Refund) | Yes | 100% Refundable logic with marketplace restrictions. |
| **80% Refundable C** (`GMIERC721R80C`) | ERC721Enumerable | Yes (80% Refund) | Yes | 80% Refundable logic with marketplace restrictions and fee splitting to `OperatorRegistry`. |

**NOTE**: Contracts with 'C' in their names follow the **ERC721C standard**, where trading of those NFTs is limited to selected marketplaces registered with the `OperatorRegistry`.

## Authors and Acknowledgment

- [@zakialam](https://github.com/zalam003)
- [@leon](https://github.com/LeonDolinar)
- [@haidar.ali](https://github.com/haidaralimasu)

## Quickstart

### Requirements

- node **v18.17.0**
- yarn **v1.22.19**

### Setup

1.  **Clone the repo**:
    ```sh
    git clone <repository-url>
    cd lin-jin5-launchpad-contracts
    ```

2.  **Setup environment file**: Copy the example file to create your local environment file.
    ```sh
    cp .env.example .env
    ```

3.  **Install all dependencies**:
    ```sh
    yarn
    ```

4.  **Setup environment variables in `.env`**:
    ```sh
    INFURA_PROJECT_ID='Infura project id'
    WALLET_PRIVATE_KEY='Your wallet private key'
    ETHERSCAN_API_KEY='Etherscan api key'
    ```

### Running Commands

-   **Compile Contracts**:
    ```sh
    yarn compile
    ```

-   **Run Test Cases (Runs all unit tests)**:
    ```sh
    yarn test
    ```    *(Note: The scripts defined in `package.json` run a specific subset of tests in sequence.)*

-   **Format Code**:
    ```sh
    yarn lint
    ```

## Deployment Scripts

Deployment is handled via Hardhat scripts located in the `scripts/` directory. All deployment examples use placeholder addresses/values which must be updated for a real deployment.

### Standard ERC721 Deployments

| Contract | Testnet Command | Mainnet Command |
| :--- | :--- | :--- |
| **Standard** (`GMIERC721`) | `npx hardhat run scripts/deploy-erc721.js --network energiTestnet` | `npx hardhat run scripts/deploy-erc721.js --network energiMainnet` |
| **100% Refundable** (`GMIERC721R`) | `npx hardhat run scripts/deploy-erc721r.js --network energiTestnet` | `npx hardhat run scripts/deploy-erc721r.js --network energiMainnet` |
| **80% Refundable** (`GMIERC721R80`) | `npx hardhat run scripts/deploy-erc721r80.js --network energiTestnet` | `npx hardhat run scripts/deploy-erc721r80.js --network energiMainnet` |

### ERC721C Deployments

For ERC721C variants, you must provide the deployed `OperatorRegistryProxy` address during deployment.

| Contract | Deployment Script Command |
| :--- | :--- |
| **Standard ERC721C** | `npx hardhat run scripts/erc721c/deploy-erc721c.js --network <network name>` |
| **100% Refundable ERC721C** | `npx hardhat run scripts/erc721c/deploy-erc721rc.js --network <network name>` |
| **80% Refundable ERC721C** | `npx hardhat run scripts/erc721c/deploy-erc721rc80.js --network <network name>` |

### Operator Registry Deployment

The Operator Registry must be deployed before any ERC721C contracts.

-   **Deploy Operator Registry**:
    ```sh
    npx hardhat run scripts/erc721c/deploy-operatorRegistry.js
    ```
    This script deploys the Proxy Admin, Logic Contract, and the Proxy, outputting the key addresses.

## Documentation

Detailed documentation on the available functions for each contract variant is found in the following Markdown files:

-   [Standard NFT Contracts and Standard ERC721C NFT Contracts](./docs/Standard.md)
-   [100% Refundable NFT Contracts and 100% Refundable ERC721C NFT Contracts](./docs/Refundable100.md)
-   [80% Refundable NFT Contracts and 80% Refundable ERC721C NFT Contracts](./docs/Refundable80.md)

## License

GMI Launchpad Contracts repo is available under the **MIT license**. See the [LICENSE](LICENSE) file for more info.
