# MistCoin reverse engineering

Purpose of this repo is to get the Solidity source code of the very first ERC-20 token called MistCoin (MC) which was created on November 3rd, 2015

## Learnings so far
* Compiler has to be Solidity <= 0.1.6 since the contract was deployed on November 3rd, 2015 and version 0.1.7 was release on November 17 2015. See [Solidity version history](https://github.com/ethereum/solidity/releases?page=10)
* In [this Reddit post](https://www.reddit.com/r/ethereum/comments/3rcnrx/ethereum_wallet_beta3_contract_deployment_and/) which was exactly on the same date as the deployment of MistCoin Fabian included a link of the Mist wallet (version 0.3.5) and [release notes](https://github.com/ethereum/mist/releases/tag/0.3.5) on how to deploy a token.
* [The token example](http://chriseth.github.io/browser-solidity/?gist=909d02feff3a2e59f714#gist=909d02feff3a2e59f714) which was used does contain all the methods of the MistCoin token. This example is included in the repo at `contracts/MyToken.sol`. However it doesn't compile to the bytecode of the MistCoin contract

## Notes

* [MistCoin token on Etherscan](https://etherscan.io/token/0xf4eced2f682ce333f96f2d8966c613ded8fc95dd)
* You can use [this webpage](https://piyolab.github.io/playground/ethereum/getEncodedFunctionSignature/) to see the bytecode of a function. for example putting in `name()` converts to `06fdde03` (remove the `0x` part)

## Bytecode

The bytecode that comes with the contract

```
0x606060405260e060020a600035046306fdde038114610047578063313ce567146100a457806370a08231146100b057806395d89b41146100c8578063a9059cbb14610123575b005b61015260008054602060026001831615610100026000190190921691909104601f810182900490910260809081016040526060828152929190828280156101f55780601f106101ca576101008083540402835291602001916101f5565b6101c060025460ff1681565b6101c060043560036020526000908152604090205481565b610152600180546020601f6002600019610100858716150201909316929092049182018190040260809081016040526060828152929190828280156101f55780601f106101ca576101008083540402835291602001916101f5565b610045600435602435600160a060020a033316600090815260036020526040902054819010156101fd57610002565b60405180806020018281038252838181518152602001915080519060200190808383829060006004602084601f0104600302600f01f150905090810190601f1680156101b25780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6060908152602090f35b820191906000526020600020905b8154815290600101906020018083116101d857829003601f168201915b505050505081565b600160a060020a03821660009081526040902054808201101561021f57610002565b806003600050600033600160a060020a03168152602001908152602001600020600082828250540392505081905550806003600050600084600160a060020a0316815260200190815260200160002060008282825054019250508190555081600160a060020a031633600160a060020a03167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a3505056
```

## Functions in the bytecode

```
06fdde03 -> name()
313ce567 -> decimals()
70a08231 -> balanceOf(address)
95d89b41 -> symbol()
a9059cbb -> transfer(address,uint256)
```

## Compile

* Make sure you have nodejs installed
* Make sure the `solc` dependency is installed (npm i)
* Run `node deploy.js` to compile the contract `contracs/MyToken.sol`