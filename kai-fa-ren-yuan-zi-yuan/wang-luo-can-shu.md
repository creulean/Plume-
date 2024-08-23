---
description: Plume 测试网目前部署在以太坊 Sepolia 测试网上。
---

# 网络参数

## 基础网络参数

* Network Name: Plume Testnet
* Chain ID: `161221135`
* Currency Symbol: ETH
* Settlement Layer: Ethereum Sepolia (Chain ID: `11155111`)
* Latest Supported EVM Version: Cancun

## URLs列表

* HTTP RPC URL: [https://testnet-rpc.plumenetwork.xyz/http](https://testnet-rpc.plumenetwork.xyz/http)
* WebSockets RPC URL: [wss://testnet-rpc.plumenetwork.xyz/ws](wss://testnet-rpc.plumenetwork.xyz/ws)
* Plume Testnet Block Explorer: [https://testnet-explorer.plumenetwork.xyz/](https://testnet-explorer.plumenetwork.xyz/)
* Plume Testnet Bridge: [https://testnet-bridge.plumenetwork.xyz/](https://testnet-bridge.plumenetwork.xyz/)
* Plume Faucet: [https://faucet.plumenetwork.xyz/](https://faucet.plumenetwork.xyz/)

## 钱包地址

下面的钱包地址用于管理 Plume 测试网络。

| Wallet Name                                         | Wallet Address                               | Chain            |
| --------------------------------------------------- | -------------------------------------------- | ---------------- |
| Chain Owner                                         | `0xe4F993164bECAB437706ad8A59178256BC80C124` | Ethereum Sepolia |
| Batch Poster                                        | `0xEAC3C7A432cD58ed75Fa9229E04D205Bf18bd438` | Ethereum Sepolia |
| Staker                                              | `0xd5da6772Cfb22332FC53c2b9703cd380b469F40e` | Ethereum Sepolia |
| Network Fee Receiver + Infrastructure Fee Collector | `0xe4F993164bECAB437706ad8A59178256BC80C124` | Plume Testnet    |



## 合约地址

下面的合约地址分为以太坊 Sepolia 上的合约和 Plume 测试网络上的合约。



## 以太坊Sepolia测试网

| Contract Name                      | Contract Address                             |
| ---------------------------------- | -------------------------------------------- |
| Rollup                             | `0xc7Ef9D4581BF2A150Cb7e975365aB8aDfC105357` |
| Delayed Inbox                      | `0x3E2e3F4F24eDdD9d6968B7b88F1Bf408FC9fEFd6` |
| Outbox                             | `0xE30a5eaFFA772Ed729a955292359cf827541D77F` |
| Sequencer Inbox                    | `0x42BD861f74608090D356E82aaA716D458f39F2D3` |
| Bridge                             | `0x13C706e7F727d88d381B35C27E687a03757277fd` |
| Utils                              | `0xE6b83B5b83BbF4Ee578c316756717d01Ebbb2079` |
| Validator Wallet Creator           | `0x761aDFED7f31ce28812713d814DfEA5E09b7a0b1` |
| Upgrade Executor                   | `0x86709d920F574cA0e5AD191E801Ac286819c4C16` |
| L2 Upgrade Executor                | `0xb9EFe40eAf6E66A3342898d9Fa2337d3b96a7CA4` |
| L1 Arbitrum Generic-Custom Gateway | `0x62bba57b0c8087FA60109264fC5E298Ca0647570` |
| L1 Multicall                       | `0xb80931C59150f5bbeAa1D8989Da783637b4bA005` |
| L1 Proxy Admin                     | `0x3e08f9C10Fa6427Eb94d893C61bB08aaF4e1b9d0` |
| L1 Gateway Router                  | `0x19e6c4820F57B354D5C8C5e4d1A3255c746c4e8D` |
| L1 Standard ERC20 Gateway          | `0x6EBF7450a7A31F3A00B4767353aa76EE54bCb75e` |
| L1 WETH Gateway                    | `0x637107A196814CaaAC407Bb282905961d665AD89` |
| L1 WETH                            | `0x7b79995e5f793A07Bc00c21412e50Ecae098E7f9` |



## Plume测试网

| Contract Name                      | Contract Address                             |
| ---------------------------------- | -------------------------------------------- |
| L2 Arbitrum Generic-Custom Gateway | `0x28d7918998835A62294Ec5f237377516c7FB8D46` |
| L2 Multicall                       | `0xE915bA31Bd0d0F9c3165C4Ff06a88727a8509239` |
| L2 Proxy Admin                     | `0x5Aa26C3A1e6E372e9648EEDC39A232A2529272ef` |
| L2 Gateway Router                  | `0xb089611b887900f79A4b9ab8fB08D7Bd75e102F7` |
| L2 Standard ERC20 Gateway          | `0x68d237955B2284BD0737ec1d3b577B1d935866aF` |
| L2 WETH Gateway                    | `0xC3E04dAe7E86F2f28366be835568fB8D9A9A374f` |
| L2 WETH                            | `0xe76Fda9882510850439Cba890960CED1d1Dc195e` |
| L2 USDC                            | `0xEa237441c92CAe6FC17Caaf9a7acB3f953be4bd1` |
| L2 USDC Faucet                     | `0x5Df3B533850E05e37cC4DfAf54EDd0c0C0fa5C12` |



## 预编译

以下预编译始终与 Arbitrum Sepolia 上的相应预编译具有相同的地址。

| Wallet Name      | Wallet Address                             |
| ---------------- | ------------------------------------------ |
| ArbAddressTable  | 0x0000000000000000000000000000000000000066 |
| ArbAggregator    | 0x000000000000000000000000000000000000006D |
| ArbBLS           | 0x0000000000000000000000000000000000000067 |
| ArbFunctionTable | 0x0000000000000000000000000000000000000068 |
| ArbGasInfo       | 0x000000000000000000000000000000000000006C |
| ArbInfo          | 0x0000000000000000000000000000000000000065 |
| ArbOwner         | 0x0000000000000000000000000000000000000070 |
| ArbOwnerPublic   | 0x000000000000000000000000000000000000006b |
| ArbRetryableTx   | 0x000000000000000000000000000000000000006E |
| ArbStatistics    | 0x000000000000000000000000000000000000006F |
| ArbSys           | 0x0000000000000000000000000000000000000064 |
| NodeInterface    | 0x00000000000000000000000000000000000000C8 |
