# 测试币水龙头

你可以从Plume的[官方水龙头](https://faucet.plumenetwork.xyz/)获取ETH和GOON。请注意，这些都是测试网代币，没有任何货币价值。

## ETH测试币水龙头

ETH 在 Plume 测试网上用于支付 gas，是通过桥接到 Plume 的 Ethereum Sepolia 上的 ETH。你可以直接从 Plume 的[官方水龙头](https://faucet.plumenetwork.xyz/)获取 ETH，或者使用 Plume [测试网桥](https://testnet-bridge.plumenetwork.xyz/)将 SepoliaETH 桥接到 Plume。交易将在三分钟内确认。

您可以从以下公共水龙头获取SepoliaETH：

* [Alchemy Faucet](https://sepoliafaucet.com/) （需要 Alchemy 账户）
* [Infura Faucet](https://www.infura.io/faucet/sepolia) （需要 Infura 账户）
* [QuickNode Faucet](https://faucet.quicknode.com/ethereum/sepolia) （需要在以太坊主网钱包里有 0.001 ETH 的余额）
* [Sepolia PoW Faucet](https://sepolia-faucet.pk910.de/) （需要你提供算力以防止机器人）

## 稳定币测试币水龙头

您可以通过访问 Plume 区块浏览器上的 [USDC 水龙头](https://plume-testnet.explorer.caldera.xyz/address/0x5Df3B533850E05e37cC4DfAf54EDd0c0C0fa5C12?tab=write\_contract)获取稳定币。您可以直接连接到您的 Plume 测试网钱包，并在 `1. requestTokens` 下点击“Write”以获取 100,000 个假的测试网 USDC：

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

或者，您可以直接在稳定币水龙头合约上调用 `requestTokens`（无参数）。主要的代币合约地址是：

| Contract Name | Contract Address                                                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GOON          | [0xbA22114ec75f0D55C34A5E5A3cf384484Ad9e733](https://testnet-explorer.plumenetwork.xyz/token/0xbA22114ec75f0D55C34A5E5A3cf384484Ad9e733)                |
| goonUSD       | [0x5c1409a46cD113b3A667Db6dF0a8D7bE37ed3BB3](https://testnet-explorer.plumenetwork.xyz/token/0x5c1409a46cD113b3A667Db6dF0a8D7bE37ed3BB3)                |
| stRWA         | [0x5F10335c4F626e8BeDf717F72b49D1f96d60f18f](https://testnet-explorer.plumenetwork.xyz/address/0x5F10335c4F626e8BeDf717F72b49D1f96d60f18f)              |
| NEST          | [0xd806259C3389Da7921316fb5489490EA5E2f88C6](https://testnet-explorer.plumenetwork.xyz/token/0xd806259C3389Da7921316fb5489490EA5E2f88C6)                |
| USDC          | [0xEa237441c92CAe6FC17Caaf9a7acB3f953be4bd1](https://testnet-explorer.plumenetwork.xyz/token/0xEa237441c92CAe6FC17Caaf9a7acB3f953be4bd1)                |
| DAI           | [0x1aa70741167155E08bD319bE096C94eE54C6CA19](https://testnet-explorer.plumenetwork.xyz/token/0x1aa70741167155E08bD319bE096C94eE54C6CA19)                |
| USDT          | [0x4632403a83fb736Ab2c76b4C32FAc9F81e2CfcE2](https://testnet-explorer.plumenetwork.xyz/token/0x4632403a83fb736Ab2c76b4C32FAc9F81e2CfcE2)                |
| USDCFaucet    | [0x5Df3B533850E05e37cC4DfAf54EDd0c0C0fa5C12](https://testnet-explorer.plumenetwork.xyz/address/0x5Df3B533850E05e37cC4DfAf54EDd0c0C0fa5C12)              |
| DAIFaucet     | [0x52D0cfaA17Af15766f7A51Dc42d96F52A1D683Ef](https://testnet-explorer.plumenetwork.xyz/address/0x52D0cfaA17Af15766f7A51Dc42d96F52A1D683Ef)              |
| USDTFaucet    | [0xA4066fd45235E6b42E47890502Dc30B71B04588f](https://testnet-explorer.plumenetwork.xyz/address/0xA4066fd45235E6b42E47890502Dc30B71B04588f)              |
| ETHFaucet     | [0x9Cb7c940e57CC000606f99d02852804DcF495E46](https://testnet-explorer.plumenetwork.xyz/address/0x9Cb7c940e57CC000606f99d02852804DcF495E46?tab=contract) |
