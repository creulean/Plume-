# 代币标准

Plume 支持多种代币标准，以涵盖所有类别的现实世界资产的全部用例。资产发行者可以直接从 Plume 管理仪表板对其资产进行代币化，并通过单击即可部署任何这些代币合约。以下是我们支持的代币标准及其各自用例的表格：

|                                            代币标准                                           |            描述           |                                               现实世界资产的例子                                               |
| :---------------------------------------------------------------------------------------: | :---------------------: | :---------------------------------------------------------------------------------------------------: |
|               [ERC-20](https://eips.ethereum.org/EIPS/eip-20) Token Standard              | 非同质化代币不是投资合同（无利润预期，不分割） |     <p></p><ul><li>可以兑换实物服务的加密货币和稳定币</li><li>餐厅、航空公司、零售商、运动队等的忠诚积分。</li><li>碳抵消信用</li></ul><p></p>    |
|       [ERC-721](https://eips.ethereum.org/EIPS/eip-721) Non-Fungible Token Standard       |       非同质化代币不是投资合同      |            <ul><li>完整的艺术品如绘画、雕塑、版画、手工艺品等。</li><li>单独的威士忌桶</li><li>专利、商标、版权等知识产权。</li></ul>            |
|          [ERC-1155](https://eips.ethereum.org/EIPS/eip-1155) Multi Token Standard         |       非同质化代币不是投资合同      |    <ul><li>稀有的实物收藏品如邮票、硬币、宝可梦卡牌等。</li><li>网络游戏中的资源和物品</li><li>可交易的实体活动门票</li><li>物联网物理设备</li></ul>    |
| [ERC-3643](https://eips.ethereum.org/EIPS/eip-3643) T-REX - Token for Regulated EXchanges |         同质化证券代币         | <ul><li>对太阳能农场、基础设施、采矿等实物项目的投资。</li><li>商业和住宅房地产</li><li>像贵金属、原油、农产品等商品。</li><li>股票、债券和其他工具</li></ul> |

## ERC-3643: T-REX - 受监管的交易所代币

[ERC-3643](https://eips.ethereum.org/EIPS/eip-3643) 定义了一种可以以合规方式代表机构级安全代币的代币标准。使用 ERC-3643 将其现实世界资产代币化的资产发行人可以访问设置转让限制、冻结代币、销毁代币和强制转让代币的接口——这些都是由证券机构监管的现实世界资产代币化表示的关键操作。

[ERC-3643 由 Tokeny 开发](https://tokeny.com/erc3643/)，并于 2021 年 7 月作为 EIP 提交，Tokeny 还在 GitHub 上开发了一个[开源参考实现](https://github.com/TokenySolutions/T-REX)。该标准完全兼容 ERC-20，因为它实现了所有必需的 [ERC-20 方法和事件](https://eips.ethereum.org/EIPS/eip-20)。

## 相关不支持代币的标准

我们选择在Plume的初始发布中不支持某些相关的代币标准。许多这些标准在社区中采用率低，并且只有一个参考实现。我们将仅在有专门的RWA项目请求加入Plume时，才考虑支持其中一些代币标准。

特别是，我们不支持任何已定稿的灵魂绑定代币标准。灵魂绑定代币在现实世界资产生态系统中的主要用例是证明用户身份和认证状态，这将由 [ONCHAINID系统](https://onchainid.com/) 提供，并与ERC-3643 T-REX标准进行本地集成。现有的灵魂绑定代币标准在基础ERC-721 NFT标准之上提供的功能最少，并且没有看到任何严肃的采用。

|                                               代币标准                                              |           描述          |                                                                                                                        当前状态                                                                                                                        |
| :---------------------------------------------------------------------------------------------: | :-------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|         [ERC-1400](https://github.com/ethereum/eips/issues/1400) Security Token Standard        |        可替代证券代币        | <ul><li>扩展ERC-20以管理身份、合规性、转让限制、赎回和撤销代币化证券</li><li>尚未达到ERC标准轨道</li><li>自2021年以来开发者活动有限</li><li>主要由<a href="https://polymath.network/erc-1400">Polymath Network</a>倡导，并且<a href="https://dune.com/queries/3604558/6073348">部署和生态系统支持有限</a></li></ul> |
| [ERC-4519](https://eips.ethereum.org/EIPS/eip-4519) Non-Fungible Tokens Tied to Physical Assets |      代表实物的非同质化代币      |                                    <ul><li>扩展ERC-721以建立物联网设备的安全通信通道</li><li>仅在<a href="https://ieeexplore.ieee.org/document/10189330">作者撰写的研究论文中引用</a></li><li><strong>可以根据要求在Plume上实施新的物联网项目</strong></li></ul>                                   |
|             [ERC-4973](https://eips.ethereum.org/EIPS/eip-4973) Account-Bound Tokens            | 具有标准ERC-721元数据的灵魂绑定代币 |                                                                          <ul><li>实现 <code>ERC721Metadata</code> 接口但不扩展 ERC-721</li><li>未被任何活跃项目使用</li><li>仍在审核阶段</li></ul>                                                                         |
|               [ERC-5114](https://eips.ethereum.org/EIPS/eip-5114) Soulbound Badge               |      只能铸造的灵魂绑定代币      |                                                                                           <ul><li>不扩展任何内容</li><li>未被任何活跃项目使用</li><li>仍处于最后呼叫阶段</li></ul>                                                                                           |
|            [ERC-5192](https://eips.ethereum.org/EIPS/eip-5192) Minimal Soulbound NFTs           |    扩展ERC-721的灵魂绑定代币   |                                                                        <ul><li>通过在转移函数上抛出并返回一个布尔值来扩展 ERC-721，以确定它是否被锁定。</li><li>ERC-721上只有一个新功能</li><li>未被任何活跃项目使用</li></ul>                                                                       |
|         [ERC-5484](https://eips.ethereum.org/EIPS/eip-5484) Consensual Soulbound Tokens         |    具有不可变销毁授权的灵魂绑定代币   |                                                                           <ul><li>通过在转移功能上抛出并允许发行者或接收者销毁代币来扩展ERC-721</li><li>ERC-721上只有一个新功能</li><li>未被任何活跃项目使用</li></ul>                                                                          |
|              [ERC-5507](https://eips.ethereum.org/EIPS/eip-5507) Refundable Tokens              |     可退还的同质化和非同质化代币    |                                                               <ul><li>扩展 ERC-20、ERC-721 和 ERC-1155 的退款功能</li><li>在一段时间内将资金托管</li><li><strong>可以根据要求在Plume上实施新的购物项目</strong></li></ul>                                                              |
|              [ERC-6065](https://eips.ethereum.org/EIPS/eip-6065) Real Estate Token              |      代表房地产的非同质化代币     |                                                                             <ul><li>扩展 ERC-721 以在链上表示房地产的法律细节</li><li><strong>可以根据要求在Plume上实施新的房地产项目</strong></li></ul>                                                                            |
|          [ERC-6239](https://eips.ethereum.org/EIPS/eip-6239) Semantic Soulbound Tokens          |    灵魂绑定代币的结构化社交图数据    |                                                 <ul><li>扩展 ERC-5192 与资源开发框架三元组</li><li>仅供作者自己的初创公司<a href="https://relationlabs.ai/">Relation Labs</a>使用</li><li>社交图数据与在Plume上引导现实世界资产无关</li></ul>                                                 |
|            [ERC-6672](https://eips.ethereum.org/EIPS/eip-6672) Multi-Redeemable NFTs            |    可在多种场景中兑换的非同质化代币   |                                                                                 <ul><li>扩展 ERC-721 具有赎回功能</li><li><strong>可以根据要求在Plume上实施新的售票项目</strong></li></ul>                                                                                 |
