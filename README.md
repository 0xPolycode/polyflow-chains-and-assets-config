# Polyflow Chain and Asset Config

This repository contains files for chain configuration and ERC20/ERC721 token lists for Polyflow backend.  
There are two configuration files: `chain-defs.json` and `token-defs.json`.

## `chain-defs.json`
This file contains configuration for chains.

Example:
```json
{
    "chains": [
        {
            "chainId": 1,
            "rpcUrl": "https://mainnet.infura.io/v3/{rpcKey}",
            "name": "Ethereum Mainnet",
            "decimals": 18,
            "usdPriceFeed": {
                "chainId": 1,
                "contractAddress": "0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419"
            }
        }
    ]
}
```

Fields:

`chainId` - ID of the chain.  
`rpcUrl` - RPC URL of the chain, may contain `{rpcKey}` placeholder which will be replaced with
RPC credentials specified via Polyflow backend properties.  
`name` - Name of the chain.  
`decimals` - Number of decimals of the chain-native asset.  
`usdPriceFeed` - Definition of [ChainLink price feed contract](https://docs.chain.link/data-feeds/price-feeds/addresses).
This price feed is expected to be in USD.  
`usdPriceFeed.chainId` - ID of the chain on which the price feed contract is deployed (usually Ethereum).
The chain must be defined in `chains` array for this chain ID, otherwise fetching price feed will not be possible.  
`usdPriceFeed.contractAddress` - Contract address of the price feed contract.

## `token-defs.json`
This file contains configuration for ERC20 and ERC721 tokens.

Example:
```json
{
    "erc20Tokens": [
        {
            "address": "0x1f9840a85d5af5bf1d1762f925bdaddc4201f984",
            "chainIds": [
                1
            ],
            "name": "Uniswap",
            "usdPriceFeed": {
                "chainId": 1,
                "contractAddress": "0x553303d460EE0afB37EdFf9bE42922D8FF63220e"
            },
            "decimals": 18
        }
    ],
    "erc721Tokens": [
        {
            "address": "0xBC4CA0EdA7647A8aB7C2061c2E118A18a936f13D",
            "chainId": 1,
            "name": "Bored Ape Yacht Club",
            "ethPriceFeed": {
                "chainId": 1,
                "contractAddress": "0x352f2Bc3039429fC2fe62004a1575aE74001CfcE"
            }
        }
    ]
}
```

Fields:

`address` - Contract address of the ERC20/ERC721 token.  
`chainIds` - **Only for ERC20 tokens.** List of chain IDs on which this ERC20 token is deployed.  
`chainId` - **Only for ERC721 tokens.** Chain ID on which this ERC721 token is deployed.  
`name` - Name of the ERC20/ERC721 token.  
`usdPriceFeed` - **Only for ERC20 tokens.** Definition of [ChainLink price feed contract](https://docs.chain.link/data-feeds/price-feeds/addresses).
This price feed is expected to be in USD.  
`usdPriceFeed.chainId` - ID of the chain on which the price feed contract is deployed (usually Ethereum).
The chain must be defined in `chain-defs.json`.  
`usdPriceFeed.contractAddress` - Contract address of the price feed contract.  
`ethPriceFeed` - **Only for ERC721 tokens.** Definition of [ChainLink NFT floor price contract](https://docs.chain.link/data-feeds/nft-floor-price/addresses).
This price feed is expected to be in ETH.  
`ethPriceFeed.chainId` - ID of the chain on which the price feed contract is deployed (usually Ethereum).
The chain must be defined in `chain-defs.json`.  
`ethPriceFeed.contractAddress` - Contract address of the price feed contract.  
`decimals` - **Only for ERC20 tokens.** The nubmer of decimals for the token.
