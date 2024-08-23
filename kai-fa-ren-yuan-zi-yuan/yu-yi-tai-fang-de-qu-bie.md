# 与以太坊的区别

Plume 构建在 [Arbitrum Nitro](https://docs.arbitrum.io/inside-arbitrum-nitro/) 堆栈之上——该堆栈为所有 Arbitrum 链提供支持，包括 Arbitrum One 和 Arbitrum Nova。Arbitrum Nitro 堆栈旨在与以太坊保持高度兼容性和一致性，因此一般来说，您应该能够将您的合约从以太坊和其他 EVM 兼容链直接部署到 Plume 上而无需修改。本页面详细介绍了剩余的细微差异。

## Plume特定差异

Plume主网将对Arbitrum Nitro的[状态转换功能](https://docs.arbitrum.io/inside-arbitrum-nitro/#sequencing-followed-by-deterministic-execution)进行轻微修改，与其他链相比。具体来说，我们正在优化执行客户端，以更高效地执行在处理现实世界资产时更常用的某些操作。最终结果是我们可以减少这些操作的gas费用，使其对最终用户来说更便宜，因为这些操作被调用的频率很高。

第一个减少gas费用的功能是从[以太坊认证服务（EAS）](https://attest.sh/)获取认证的功能。我们将EAS认证和模式注册合约作为预部署，这是[Optimism](https://docs.optimism.io/chain/identity/contracts-eas)的一个功能，而Arbitrum没有。这使得dapp开发人员可以构建符合身份验证和反洗钱要求的应用程序，而无需花费大量的gas。

## Solidity差异

以下属性在 Plume 上与以太坊相比也返回不同的值：

* `blockhash()`
* `block.coinbase`
* `block.diffiulty`
* `block.prevrandao`
* `block.number`
* `msg.sender`

有关详细信息，请参阅官方 Arbitrum 文档中的[“Solidity 支持”](https://docs.arbitrum.io/for-devs/concepts/differences-between-arbitrum-ethereum/solidity-support)。

## 区块编号

Plume 网络上的区块有自己的 L2 区块编号，这些编号独立于以太坊区块编号。例如，一个以太坊区块可以包含多个 Plume 区块，尽管一个 Plume 区块只能在一个以太坊区块中。

Plume 区块编号从创世区块的 0 开始，并随着交易通过排序器而按顺序增加。如果 Plume 网络上没有交易，则不会创建 Plume 区块。可以使用 Solidity 中的 `block.number` 访问当前 L1 区块编号的近似值。可以使用 `ArbSys` 预编译访问当前 Plume 区块编号：

```
ArbSys(100).arbBlockNumber()
```

有关详细信息，请参阅官方 Arbitrum 文档中的[“区块编号和时间”](https://docs.arbitrum.io/for-devs/concepts/differences-between-arbitrum-ethereum/block-numbers-and-time)。

## RPC 方法

Plume上的大多数RPC方法的行为类似于以太坊，但某些方法的输出略有不同或添加了特定于Plume的附加信息，包括但不限于：

* `eth_getTransactionByHash`
* `eth_getTransactionReceipt`
* `eth_getBlockByHash`
* `eth_syncing`

有关详细信息，请参阅官方 Arbitrum 文档中的[“RPC 方法”](https://docs.arbitrum.io/for-devs/concepts/differences-between-arbitrum-ethereum/rpc-methods)。

## L2汇总特定功能

Plume 上有一些特定于 L2 rollups 和 Arbitrum Nitro 堆栈的附加功能：

* 以太坊合约可以通过[可重试票](https://docs.arbitrum.io/arbos/l1-to-l2-messaging)直接在Plume上发送消息。
* Plume合约可以在7天后使用 [Outbox](https://docs.arbitrum.io/arbos/l2-to-l1-messaging) 直接在以太坊上发送消息。
* [Plume有特定的预编译](https://docs.plumenetwork.xyz/plume/developer-resources/network-parameters#precompiles)，具有以太坊上不存在的特殊固定地址。
* 有一个 [特殊](https://docs.arbitrum.io/for-devs/concepts/nodeinterface) 的 `NodeInterface` [预编译](https://docs.arbitrum.io/for-devs/concepts/nodeinterface)，只能通过RPC调用访问。
* Plume上的用户必须支付燃气费，用于（1）将其交易数据存储为L1 calldata和（2）在L2上执行交易，涵盖计算和存储的成本。有关更多详细信息，请参阅官方Arbitrum文档中的[“Gas and Fees”](https://docs.arbitrum.io/arbos/gas)。
