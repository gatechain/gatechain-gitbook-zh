# GateChain 全节点设置指南

## 概述
GateChain 全节点是支持 GateChain 运行的核心组件。GateChain "全节点"具备 GateChain 的所有功能，包括构建本地 GateChain 测试网、加入 GateChain 公共测试网或加入 GateChain 主网。它还支持下载链上区块数据、验证和执行业务逻辑以及监控共识信息。

## 支持的平台
GateChain 全节点目前支持 Unix 环境（macOS、Ubuntu、CentOS）。

## 硬件要求
运行全节点的硬件必须满足以下要求：

- 操作系统：Mac OS 10.14.6 或更高版本、CentOS Linux release 7.7.1908 或更高版本，或 Ubuntu 18.04.2 或更高版本
- 4 核 CPU、8GB+ 内存和 100GB+ 磁盘空间
- 稳定的网络连接，带宽至少 1MB/s

## 安装步骤

### 方法一：自动安装脚本
注意：请确保您的环境中已安装 "wget"

我们在 GitHub 上维护了一个安装脚本（"install.sh"），用于处理链可执行文件的设置。默认设置如下：

可执行文件放置在 "/usr/local/bin"（即 "gated" "gatecli"）

```bash
# 一键安装（需要代理）
bash <(wget -qO- https://raw.githubusercontent.com/gatechain/node-binary/master/node/install.sh)

# 中国用户一键安装（无需代理）
bash <(wget -qO- https://gatechainbucket.oss-cn-beijing.aliyuncs.com/auto-install.sh)
```

注意：如果您是第二次或多次安装，需要先手动删除本地 gated/gatecli 文件。

### 方法二：自定义安装 1
我们目前使用此仓库存储已编译节点二进制文件的历史版本。

1. 安装 Git LFS
Git LFS 是用于管理大文件的 Git 扩展。请访问 https://git-lfs.github.com/ 进行安装。

2. 克隆仓库：
```bash
git lfs clone https://github.com/gatechain/node-binary.git
```

3. 根据更新日志选择相应版本的二进制文件：
```bash
cd node-binary/node/{network}/{version}/{os_type}
```

4. 将二进制文件复制到 "/usr/local/bin"：
```bash
cp gated gatecli /usr/local/bin
```

5. 创建 GateChain 节点根目录 $GATEHOME（即 ~/.gated）：
```bash
mkdir ~/.gated
```

6. 从 "node-binary/node/{network}/{version}/config/" 复制 "config.json" 和 "genesis.json" 到 "$GATEHOME/"

### 方法三：自定义安装 2
用户可以根据系统要求选择下载链接。

注意：请确保您的环境中已安装 "wget"

#### macOS 系统：
```bash
# 下载 gated
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/mac/gated

# 下载 gatecli
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/mac/gatecli
```

#### Linux 系统：
```bash
# 下载 gated
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/linux/gated

# 下载 gatecli
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/linux/gatecli
```

#### 下载配置文件：
```bash
# 下载 config.json
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/config/config.json

# 下载 genesis.json
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/config/genesis.json
```

将下载的二进制文件复制到 "/usr/local/bin"：
```bash
cp gated gatecli /usr/local/bin
```

创建节点根目录：
```bash
mkdir ~/.gated
```

将配置文件复制到 "$GATEHOME/"

## 启动节点

### 基本启动
```bash
gated start
```

### GC 模式启动
要以 GC 模式启动，修改启动命令：
```bash
gated start --pruning nothing
```

### 启动 EVM RPC
```bash
gatecli evm rest-server --gm-websocket-port http://127.0.0.1:8085 --chain-id mainnet --laddr tcp://0.0.0.0:6060 --rpc-api web3,eth,personal,net,debug
```

要支持 EVM RPC，请修改 config.json 中的以下属性：
```json
"WsPort": "tcp://0.0.0.0:8085"
"IsWebSocketServerActive": true
```
保存更改并重启 gated。

### 与节点交互
您可以使用 [gatecli 命令行界面](../api/http.md) 或 [RPC API](../api/http.md) 与本地节点进行交互。