# 使用Thirdweb部署

连接到[Plume测试网](https://docs.plumenetwork.xyz/plume/getting-started/connecting-to-plume)并使用桥接的SepoliaETH为您的钱包提供资金后，您可以使用在以太坊、Arbitrum、Optimism和Polygon开发中使用的相同工具轻松部署任何EVM兼容的智能合约。

## 网络参数

所有工具都需要您提供部分或全部的[Plume测试网网络参数](https://docs.plumenetwork.xyz/plume/developer-resources/network-parameters)，以便它们可以部署到测试网。您可以在此处参考它们：

| Name               | Value                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------- |
| Network Name       | Plume Testnet                                                                            |
| HTTP RPC URL       | [https://testnet-rpc.plumenetwork.xyz/http](https://testnet-rpc.plumenetwork.xyz/http)   |
| WebSockets RPC URL | [wss://testnet-rpc.plumenetwork.xyz/ws](wss://testnet-rpc.plumenetwork.xyz/ws)           |
| Chain ID           | 161221135                                                                                |
| Currency Symbol    | ETH                                                                                      |
| Block Explorer URL | [https://testnet-explorer.plumenetwork.xyz/](https://testnet-explorer.plumenetwork.xyz/) |

| Name               | Value                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------- |
| Network Name       | Plume Testnet                                                                            |
| HTTP RPC URL       | [https://testnet-rpc.plumenetwork.xyz/http](https://testnet-rpc.plumenetwork.xyz/http)   |
| WebSockets RPC URL | [wss://testnet-rpc.plumenetwork.xyz/ws](wss://testnet-rpc.plumenetwork.xyz/ws)           |
| Chain ID           | 161221135                                                                                |
| Currency Symbol    | ETH                                                                                      |
| Block Explorer URL | [https://testnet-explorer.plumenetwork.xyz/](https://testnet-explorer.plumenetwork.xyz/) |

## Thirdweb设置

[Thirdweb](https://thirdweb.com/)是一家构建开源开发者工具并提供无代码网页界面以在任何兼容EVM的网络上部署和管理智能合约的公司。只需使用已资助的测试网钱包[注册一个免费账户](https://thirdweb.com/deploy)即可开始。

## 部署NFT合约

<figure><img src="../.gitbook/assets/image (1).avif" alt=""><figcaption></figcaption></figure>

要在Thirdweb上部署代币化资产，请导航到[“合约”选项卡中的“探索”](https://thirdweb.com/explore)部分，然后点击“NFT集合”。然后点击“立即部署”并填写您的资产详细信息。

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

在“网络/链”部分，点击“选择网络”，然后搜索并选择“Plume Testnet”。

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

最后，点击“立即部署”，并使用您连接的钱包签署一系列4笔交易。确保您的钱包在每笔交易中都连接到Plume测试网。您的NFT将在一分钟内在Plume测试网上线。

## Mint Single NFT

返回到[“合约”](https://thirdweb.com/dashboard/contracts/deploy)选项卡并点击您新部署的合同。在左侧边栏的“扩展”下点击“NFTs”选项卡，然后点击“铸造”以从您的收藏中铸造一个NFT。由于您连接的钱包是唯一具有铸造者角色的钱包，只要您只铸造一个NFT，这个NFT收藏将保持为1对1的NFT。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

填写详细信息，点击“铸造NFT”，并签署单笔交易以铸造NFT。您还可以在[Plume Testnet区块浏览器](https://plume-testnet.explorer.caldera.xyz/)的“代币”部分中看到生成的NFT。

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

