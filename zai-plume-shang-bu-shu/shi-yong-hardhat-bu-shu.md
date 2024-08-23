# 使用Hardhat部署

连接到[Plume测试网](https://docs.plumenetwork.xyz/plume/getting-started/connecting-to-plume)并使用桥接的SepoliaETH为您的钱包提供资金后，您可以使用在以太坊、Arbitrum、Optimism和Polygon开发中使用的相同工具轻松部署任何EVM兼容的智能合约。

所有工具都需要您提供部分或全部的[Plume测试网网络参数](https://docs.plumenetwork.xyz/plume/developer-resources/network-parameters)，以便它们可以部署到测试网。您可以在此处参考它们：

| Name               | Value                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------- |
| Network Name       | Plume Testnet                                                                            |
| HTTP RPC URL       | [https://testnet-rpc.plumenetwork.xyz/http](https://testnet-rpc.plumenetwork.xyz/http)   |
| WebSockets RPC URL | [wss://testnet-rpc.plumenetwork.xyz/ws](wss://testnet-rpc.plumenetwork.xyz/ws)           |
| Chain ID           | 161221135                                                                                |
| Currency Symbol    | ETH                                                                                      |
| Block Explorer URL | [https://testnet-explorer.plumenetwork.xyz/](https://testnet-explorer.plumenetwork.xyz/) |

## Hardhat设置

[Hardhat](https://hardhat.org/) 是一个用于部署智能合约的 Node.js 框架，由非营利组织 [Nomic Foundation](https://nomic.foundation/) 作为开源公共产品构建。只需按照他们的“[入门](https://hardhat.org/hardhat-runner/docs/getting-started)”文档创建一个新的 Node.js 项目并安装 Hardhat。我们还将安装 Nomic Foundation 的 `hardhat-ethers` [插件](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-ethers)，该插件将 `ethers.js` 添加到 [Hardhat 运行环境](https://hardhat.org/hardhat-runner/docs/advanced/hardhat-runtime-environment) 中，并允许我们编写脚本与链进行交互。

```
$ npm init
$ npm install --save-dev hardhat @nomicfoundation/hardhat-ethers
$ npx hardhat init
```

选择“创建一个空的 `hardhat.config.js`”，因为我们将从头开始编写自己的智能合约。让我们基于 [OpenZeppelin 的开源 ERC-721](https://docs.openzeppelin.com/contracts/4.x/erc721) 实现编写一个简单的独一无二的 NFT 合约，以便在 Plume 上标记 CBO 珍爱的劳力士手表。首先，安装 OpenZeppelin 的依赖项：

```
$ npm install @openzeppelin/contracts
```

对自动生成的 `hardhat.config.js` 文件进行以下调整，以准备部署到Plume测试网：

* 将 `hardhat-ethers` 插件导入 Hardhat 运行环境。
* 为了使用最新版本的 OpenZeppelin 合约，请确保 Solidity 编译器版本为 `0.8.20` 或以上。
* 添加 Plume testnet 网络参数。 你可以直接在配置文件中存储 testnet 私钥，使用 `dotenv` 从环境文件中加载，或者在执行以下命令前手动运行 `export PRIVATE_KEY=...`

```
require("@nomicfoundation/hardhat-ethers");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.25",
  settings: {
    evmVersion: "cancun"
  },
  networks: {
    hardhat: {},
    "plume-testnet": {
      url: "https://testnet-rpc.plumenetwork.xyz/http",
      chainId: 161221135,
      accounts: [process.env.PRIVATE_KEY]
    }
  }
};
```

现在，将以下智能合约保存在 `contracts/RolexYachtMaster40.sol` 中。 如果你打算验证这份合约，请在第 2 行的注释中插入你的名字，这样上传的源代码就会与其他遵循本指南的人不同。 运行 `npx hardhat compile` 来编译它：

```
// SPDX-License-Identifier: MIT
// Author: <YOUR NAME HERE>
pragma solidity ^0.8.25;

import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {ERC721} from "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract RolexYachtMaster40 is Ownable, ERC721 {
    error NFTAlreadyMinted();
    bool private _minted;

    constructor(
        address initialOwner
    ) Ownable(initialOwner) ERC721("Rolex Yacht-Master 40", "") {}

    function mint() public onlyOwner returns (uint256) {
        if (_minted) {
            revert NFTAlreadyMinted();
        }
        _safeMint(msg.sender, 0);
        _minted = true;
        return 0;
    }
}
```

## 部署NFT合约

要使用 Hardhat 将智能合约部署到 Plume 测试网络，请按照 "[部署合约](https://hardhat.org/hardhat-runner/docs/guides/deploying) "文档中的说明操作。 例如，你可以将以下部署脚本保存到 `scripts/deploy.js` :

```
const hre = require("hardhat");

async function main() {
  const [deployer] = await hre.ethers.getSigners();
  const nft = await hre.ethers.deployContract("RolexYachtMaster40", [deployer], {})
  await nft.waitForDeployment();
  console.log(`Successfully deployed NFT to ${nft.target}`);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

仔细检查私钥是否可被 Hardhat 访问，以及 `plume-testnet` 是否已在 `hardhat.config.js` 中正确配置后，只需运行部署脚本即可：&#x20;

```
$ npx hardhat compile                                                                                    
Compiled 1 Solidity file successfully (evm target: cancun).
$ npx hardhat run --network plume-testnet scripts/deploy.js
Successfully deployed NFT to 0x24fD012C1fd6c496609018e19264D30D580d2385
```

你可以在 [Plume 区块浏览器](https://plume-testnet.explorer.caldera.xyz/address/0x24fD012C1fd6c496609018e19264D30D580d2385) 上看到生成的智能合约。

## 验证NFT合约

Plume 测试网区块浏览器使用 [Blockscout](https://www.blockscout.com/) 的开源技术构建，并通过其兼容 Etherscan 的 API 支持使用 `hardhat-verify` [插件](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify)验证合约。有关详细信息，请参阅“[智能合约验证](https://docs.plumenetwork.xyz/plume/developer-resources/smart-contract-verification)”部分。

要验证您的智能合约，请按照 Blockscout 的“[Hardhat 验证插件](https://docs.blockscout.com/for-users/verifying-a-smart-contract/hardhat-verification-plugin)”页面中的说明进行操作。请注意，这些文档中的 `hardhat-etherscan` 插件已重命名为 `hardhat-verify`，您需要安装：

```
$ npm install --save-dev @nomicfoundation/hardhat-verify
```

对现有的 `hardhat.config.js` 文件进行以下调整：

* 将 `hardhat-verify` 插件导入 Hardhat 运行环境。
* 与Etherscan不同，Blockscout不需要API密钥，但 `hardhat-verify` 插件要求您输入任何非空字符串，因此我们可以使用 `“test”` 作为占位符。
* 添加Plume测试网区块浏览器URL。确保在API URL的末尾添加额外的 `/?` ，否则验证将失败。

```
require("@nomicfoundation/hardhat-ethers");
require("@nomicfoundation/hardhat-verify");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.25",
  settings: {
    evmVersion: "cancun"
  },
  networks: {
    hardhat: {},
    "plume-testnet": {
      url: "https://testnet-rpc.plumenetwork.xyz/http",
      chainId: 161221135,
      accounts: [process.env.PRIVATE_KEY]
    }
  },
  etherscan: {
    apiKey: {
      "plume-testnet": "test"
    },
    customChains: [
      {
        network: "plume-testnet",
        chainId: 161221135,
        urls: {
          apiURL: "https://testnet-explorer.plumenetwork.xyz/api\?",
          browserURL: "https://testnet-explorer.plumenetwork.xyz"
        }
      }
    ]
  }
};
```

让我们通过将构造函数参数（即部署者的地址）保存到环境变量中，并在先前部署的合约地址上运行 `verify`命令来验证现有合约：

```
$ export DEPLOYER_ADDRESS=0x96774F9f5693dFb95c973b676DFE6EaFc6f95E6d                                
$ npx hardhat verify --network plume-testnet \
    0x24fD012C1fd6c496609018e19264D30D580d2385 $DEPLOYER_ADDRESS
Successfully submitted source code for contract
contracts/RolexYachtMaster40.sol:RolexYachtMaster40 at 0x24fD012C1fd6c496609018e19264D30D580d2385
for verification on the block explorer. Waiting for verification result...

Successfully verified contract RolexYachtMaster40 on the block explorer.
https://testnet-explorer.plumenetwork.xyz/address/0x24fD012C1fd6c496609018e19264D30D580d2385#code
```

您可以在[Plume区块浏览器](https://plume-testnet.explorer.caldera.xyz/address/0x41b5Bd0dFC1EF2d73630D3676867eA328b6E7706)上查看已验证的智能合约。

## Fork测试

要在 Plume Testnet 的分叉上部署智能合约，请确保安装带有 `unknown-txs` 标签的 2.20.x 版本的 Hardhat：

```
$ # Install using your preferred package manager, for example:
$ yarn add -D hardhat@unknown-txs
$ npm install -D hardhat@unknown-txs
$ pnpm install -D hardhat@unknown-txs
```

使用此 Hardhat 版本编译，并将以下内容添加到您的 `hardhat.config.js` 中的 `networks` ：

```
hardhat: {
  forking: {
    url: "https://testnet-rpc.plumenetwork.xyz/http",
  },
  chainId: 161221135
},
```

运行分叉节点：

```
$ npx hardhat node --fork https://testnet-rpc.plumenetwork.xyz/http

Nothing to compile
No need to generate any newer typings.
✅ Generated documentation for 11 contracts
{
  chainId: 161221135,
  deployer: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266'
}
Deploying to Plume-Testnet
deploying "RolexYachtMaster40" (tx: 0xf49634229a8c1f4e9b72fd57e5774afc0dbfa2feeed457592b4a8aaeb22d233a)...: deployed at 0x5FbDB2315678afecb367f032d93F642f64180aa3 with 1321634 gas
{
  Contracts: { RolexYachtMaster40: '0x5FbDB2315678afecb367f032d93F642f64180aa3' }
}
Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/
```
