# ATS（另类交易系统）集成

本节探讨替代交易系统在Plume网络中的作用，以及它们如何实现符合法规的代币化证券交易。

## 另类交易系统 (ATS)

ATS 是符合监管要求并在 FINRA 注册的代币化证券交易场所。它们在初级发行和二级市场交易中匹配买家。在美国，它们是机构资产发行者的必需合作伙伴。与传统交易所不同，ATS 没有相同的监管负担，使其在各种类型的证券交易中更加灵活和易于访问。

## 两种结算流程类型

FINRA注册的经纪交易商可以申请ATS许可证。选择使用非托管方式（即不持有客户资产）的经纪交易商可以允许合格客户使用其API进行交易。他们通常使用以下其中一种结算类型。

### 四步流程：

1. 订单提交：买卖双方将订单发送到ATS。
2. 订单匹配：ATS匹配这些订单。
3. 交易通知：ATS通知双方匹配结果。
4. 结算：双方直接或通过其托管人结算交易。

### 三步流程：

1. 订单和结算准备：买卖双方向ATS提交订单，并同时指示其托管人准备结算匹配的交易。
2. 订单匹配：ATS匹配订单。
3. 通知和结算执行：ATS通知所有各方及其托管人匹配结果，触发托管人根据先前指示执行交易。

这两种结算方案都受益于使用区块链。



## Plume上的ATS提供商

几家注册的另类交易系统已签署协议，旨在支持Plume Network上的机构资产发行人和投资者。

* **Texture Capital**：一家非托管经纪商，拥有以API为先的另类交易系统。支持美国的初级发行和二级市场交易。
* **tZERO**：资本市场区块链创新的领导者，tZERO为私营公司和其他发行人提供交易其数字证券的ATS。
* **Openfinance**：提供代币化证券的交易和结算服务。提供合规的平台进行二级市场交易，提高另类资产的流动性和可及性。
* **Archax**：为机构投资者设计的欧盟监管交易场所。提供受监管、安全且高效的数字证券环境。



## 与ATS供应商集成

* **选择ATS提供商**：根据您的具体需求选择提供商，考虑资产类型、交易量和合规性等因素。
* **集成过程**：与ATS提供商合作，将其交易系统集成到您的Plume Network运营中。这通常涉及API集成，以实现无缝交易体验。
* **合规和法律考虑**：确保ATS提供商遵守所有相关的证券法规和法律要求。
* **教育您的用户**：提供资源和信息，帮助用户了解二级交易的运作以及ATS在生态系统中的作用。

通过了解和利用ATS进行二级交易，Plume Network的参与者可以参与更广泛的交易活动，受益于增加的流动性和市场可及性。
