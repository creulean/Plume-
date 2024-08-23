# 使用Foundry部署

连接到[Plume测试网](../zhun-bei-gong-zuo/lian-jie-dao-plume.md)并使用桥接的SepoliaETH为您的钱包提供资金后，您可以使用在以太坊、Arbitrum、Optimism和Polygon开发中使用的相同工具轻松部署任何EVM兼容的智能合约。

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

## Foundry设置

[Foundry](https://getfoundry.sh/) 是一个用于部署智能合约的 Solidity 框架，由 [Paradigm](https://paradigm.xyz/) 构建，并用 Rust 编写以实现极快的速度。只需按照他们的“[入门](https://book.getfoundry.sh/getting-started/installation)”文档安装和运行 Foundry，然后按照他们的“[项目](https://book.getfoundry.sh/projects/creating-a-new-project)”文档创建一个新项目：

```
$ curl -L https://foundry.paradigm.xyz | bash
$ foundryup
$ forge init
```

让我们基于 [OpenZeppelin 的开源 ERC-721](https://docs.openzeppelin.com/contracts/4.x/erc721) 实现编写一个简单的一对一 NFT 合约，以便在 Plume 上标记 CBO 珍爱的劳力士手表。 首先，安装 OpenZeppelin 的依赖关系：

```
// SPDX-License-Identifier: MIT
pragma solidity 0.8.25;

import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {ERC721} from "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract RolexYachtMaster40 is Ownable, ERC721 {
    error NFTAlreadyMinted();
    bool private _minted;

    constructor() Ownable(msg.sender) ERC721("Rolex Yacht-Master 40", "") {}

    function mint() public onlyOwner returns (uint256) {
        if (_minted) {
            revert NFTAlreadyMinted();
        }
        _safeMint(owner(), 0);
        _minted = true;
        return 0;
    }
}
```

## 部署NFT合约

要使用 Foundry 将智能合约部署到 Plume 测试网，请按照“[部署](https://book.getfoundry.sh/forge/deploying)”文档中的说明进行操作，并将您的 `ETH_RPC_URL` 环境变量设置为 Plume RPC URL。

```
$ export ETH_RPC_URL=https://testnet-rpc.plumenetwork.xyz/http
$ export PRIVATE_KEY=<your_plume_private_key>
$ forge create src/RolexYachtMaster40.sol:RolexYachtMaster40 \
    --rpc-url $ETH_RPC_URL --private-key $PRIVATE_KEY
[⠢] Compiling...
[⠒] Compiling 1 files with 0.8.25
[⠑] Compiler run successful!
[⠘] Solc 0.8.25 finished in 435.45ms
Deployer: 0x96774F9f5693dFb95c973b676DFE6EaFc6f95E6d
Deployed to: 0x2094274284904Fa7EF04cd9912392E495c980974
Transaction hash: 0x651ed7b05933ca2cbac061316b707bc6ea830c2648ff5d5edbfeb0b08ed7bd59
```

您可以在[Plume区块浏览器](https://plume-testnet.explorer.caldera.xyz/address/0x2094274284904Fa7EF04cd9912392E495c980974)上查看生成的智能合约。

## 验证NFT合约

Plume 测试网区块浏览器使用 [Blockscout](https://www.blockscout.com/) 的开源技术构建，并通过其兼容 Etherscan 的 API 支持合约验证。有关详细信息，请参阅“[智能合约验证](https://docs.plumenetwork.xyz/plume/developer-resources/smart-contract-verification)”部分。

要验证您的智能合约，请按照 Blockscout 的“[Foundry 合约验证](https://docs.blockscout.com/for-users/verifying-a-smart-contract/openzeppelin-contract-verification#foundry-forge)”页面中的说明进行操作。请确保在验证后的 URL 末尾添加额外的 `/?` ，否则验证将失败：

```
$ export ETH_RPC_URL=https://testnet-rpc.plumenetwork.xyz/http
$ export VERIFIER_URL=https://testnet-explorer.plumenetwork.xyz/api\?
$ export PRIVATE_KEY=<your_plume_private_key>
$ forge create src/RolexYachtMaster40.sol:RolexYachtMaster40 \
    --rpc-url $ETH_RPC_URL --private-key $PRIVATE_KEY --legacy \
    --verify --verifier blockscout --verifier-url $VERIFIER_URL
[⠢] Compiling...No files changed, compilation skipped
[⠆] Compiling...
Deployer: 0x96774F9f5693dFb95c973b676DFE6EaFc6f95E6d
Deployed to: 0x41b5Bd0dFC1EF2d73630D3676867eA328b6E7706
Transaction hash: 0x6e20a2d47c2c8c255e983484c56e459409317bd85472ad9d699a65d45fd71251
Starting contract verification...
Waiting for blockscout to detect contract deployment...
Start verifying contract `0x41b5Bd0dFC1EF2d73630D3676867eA328b6E7706` deployed on 161221135

Submitting verification for [src/RolexYachtMaster40.sol:RolexYachtMaster40] 0x41b5Bd0dFC1EF2d73630D3676867eA328b6E7706.
Submitted contract for verification:
        Response: `OK`
        GUID: `41b5bd0dfc1ef2d73630d3676867ea328b6e770665c10e39`
        URL:
        https://testnet-explorer.plumenetwork.xyz/address/0x41b5bd0dfc1ef2d73630d3676867ea328b6e7706
Contract verification status:
Response: `OK`
Details: `Unknown UID`
```

您可以在[Plume区块浏览器](https://plume-testnet.explorer.caldera.xyz/address/0x41b5Bd0dFC1EF2d73630D3676867eA328b6E7706)上查看已验证的智能合约。

## Fork测试

要在 Plume 测试网的本地分叉上进行测试，请在 Foundry 中使用 `--fork-url` 参数。此外，您还可以使用 `--fork-block-number 1` 等标志来设置区块号。

```
$ forge test --fork-url https://testnet-rpc.plumenetwork.xyz/http
```

## 常见问题

在使用 Foundry 部署时，您可能会遇到错误，因为 Foundry 在 L2 上的 gas 估算存在一个 bug。为了解决这个问题，请确保：

* 您的`foundry.toml`明确设置了EVM版本：

```
evm_version = "cancun"
```

* 您的 `forge create` 或部署脚本包括以下标志：

```
$ forge create --legacy --skip-simulation
```
