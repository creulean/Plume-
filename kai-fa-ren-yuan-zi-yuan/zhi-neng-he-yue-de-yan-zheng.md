# 智能合约的验证

Plume的[原生区块浏览器](https://plume-testnet.explorer.caldera.xyz/)是我们自己托管的[Blockscout](https://www.blockscout.com/)部署，这是一个开源的区块浏览器，实施了兼容[Etherscan的API](https://etherscan.io/apis)。与Etherscan不同，Plume区块浏览器不需要任何API密钥来验证合约。与Etherscan类似，我们提供多种方法来验证您的智能合约。验证适用于Solidity和Vyper智能合约。



## 使用 Hardhat 插件进行验证

您可以使用由 [Nomic Foundation](https://nomic.foundation/) 开发的 `hardhat-verify` [插件](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify)在Plume区块浏览器上验证您的智能合约。请参阅 [“使用Hardhat部署”](https://docs.plumenetwork.xyz/plume/deploying-on-plume/deploy-with-hardhat#verify-nft-contract) 部分，了解部署和验证简单NFT合约的分步指南。步骤如下：

1. 安装 `hardhat-verify 插件。`

```
$ npm install --save-dev @nomicfoundation/hardhat-verify
```

2. 将以下更改添加到您的 `hardhat.config.js` 文件中
   * 将 `hardhat-verify` 插件导入到 Hardhat 运行时环境中。
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

3. 在现有合约上运行 `npx hardhat verify` 任务。例如：

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

您可以在[Plume区块浏览器](https://plume-testnet.explorer.caldera.xyz/address/0x24fD012C1fd6c496609018e19264D30D580d2385?tab=contract)上查看生成的已验证智能合约代码。



## 通过网络界面验证

您可以在Plume区块浏览器的网页界面上手动验证您的智能合约。只需在搜索栏中输入合约地址，点击合约详情，然后导航到“合约”选项卡并点击“验证并发布”：

<figure><img src="../.gitbook/assets/image (2).avif" alt=""><figcaption></figcaption></figure>

Plume区块浏览器支持每种智能合约编程语言的三种不同合约验证方法。您可以提交扁平化的源代码、多部分文件或标准JSON输入。

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## 扁平化源代码

有七个输入字段用于验证智能合约的扁平化源代码：

|          字段名称          |                                                                                             描述                                                                                             |
| :--------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|     Is Yul contract    |                                                                              如果您在 Yul 中编写了合同的任何部分或整个合同，请选中此项。                                                                              |
| Include nightly builds |                                                                                        选中此项以显示每夜构建。                                                                                        |
|    Compiler version    |                                                                             选择合约的`pragma solidity`指令中指定的编译器版本。                                                                             |
|       EVM version      |                                                                            选择您编译合约时使用的EVM版本，如果没有选择特定版本，请选择默认版本。                                                                            |
|  Optimization enabled  |                                                                     200 是 Solidity 编译器的默认优化级别。如果您使用不同的优化级别编译了合约，请编辑此数字。                                                                    |
|      Contract code     | 在此粘贴您的扁平化合约代码。您可以使用 [Foundry](https://book.getfoundry.sh/reference/forge/forge-flatten)、[Hardhat](https://hardhat.org/hardhat-runner/docs/advanced/flattening) 和其他在线提供的开源扁平化工具包来扁平化您的合约代码。 |
| Add contract libraries |                                                             在您的智能合约中添加最多10个合约库。您必须指定库的名称（例如 `ERC721.sol`）及其在 Plume 测试网上当前部署的地址。                                                            |

一旦您完成输入数据，请点击底部的“验证并发布”，您的合约将在Plume区块浏览器上得到验证！

## 标准 JSON 输入

有三个输入字段用于使用标准JSON输入验证智能合约：

\


|          字段名称          |                                                                   描述                                                                  |
| :--------------------: | :-----------------------------------------------------------------------------------------------------------------------------------: |
| Include nightly builds |                                                              选中此项以显示每夜构建。                                                             |
|    Compiler version    |                                                   选择合约的`pragma solidity`指令中指定的编译器版本。                                                  |
|      Contract code     | 上传您的标准输入 JSON 文件。它应符合 [Solidity 编译器输入 API 的官方格式](https://docs.soliditylang.org/en/latest/using-the-compiler.html#input-description)。. |

一旦您完成输入数据，请点击底部的“验证并发布”，您的合约将在Plume区块浏览器上得到验证！

## Multi-Part 文件

使用标准JSON输入验证智能合约有四个输入字段：\


|          字段名称          |                          描述                         |
| :--------------------: | :-------------------------------------------------: |
| Include nightly builds |                     选中此项以显示每夜构建。                    |
|    Compiler version    |          选择合约的`pragma solidity`指令中指定的编译器版本。         |
|       EVM version      |         选择您编译合约时使用的EVM版本，如果没有选择特定版本，请选择默认版本。        |
|  Optimization enabled  | 200 是 Solidity 编译器的默认优化级别。如果您使用不同的优化级别编译了合约，请编辑此数字。 |
|         Sources        |              上传整个合约的所有Solidity和Yul源文件。              |

一旦您完成输入数据，请点击底部的“验证并发布”，您的合约将在Plume区块浏览器上得到验证！
