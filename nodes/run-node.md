# GateChain Full Node Setup Guide

## Overview
GateChain full node is the core component supporting GateChain's operation. A GateChain "full node" has all the functionalities of GateChain, including building a local GateChain testnet, joining the GateChain public testnet, or joining the GateChain mainnet. It also supports downloading on-chain block data, validating and executing business logic, and monitoring consensus information.

## Supported Platforms
GateChain full node currently supports Unix environments (macOS, Ubuntu, CentOS).

## Hardware Requirements
Hardware must meet certain requirements to run a full node:

- Operating System: Mac OS 10.14.6 or above, CentOS Linux release 7.7.1908 or above, or Ubuntu 18.04.2 or above
- 4 CPU cores, 8GB+ RAM, and 100GB+ disk space
- Stable internet connection with at least 1MB/s bandwidth

## Installation Steps

### Method 1: Automated Installation Script
Note: Please ensure "wget" is installed in your environment

We maintain an installation script ("install.sh") on GitHub that handles the setup of chain executables. This uses the following defaults:

Executables are placed in "/usr/local/bin" (i.e., "gated" "gatecli")

```bash
# One-click installation (requires proxy)
bash <(wget -qO- https://raw.githubusercontent.com/gatechain/node-binary/master/node/install.sh)

# One-click installation for users in China (no proxy needed)
bash <(wget -qO- https://gatechainbucket.oss-cn-beijing.aliyuncs.com/auto-install.sh)
```

Note: If you're installing for the second time or more, you need to manually delete the local gated/gatecli files first.

### Method 2: Custom Installation 1
We currently use this repository to store historical versions of compiled node binaries.

1. Install Git LFS
Git LFS is a Git extension for managing large files. Please visit https://git-lfs.github.com/ for installation.

2. Clone the repository:
```bash
git lfs clone https://github.com/gatechain/node-binary.git
```

3. Select the corresponding version binary according to the changelog:
```bash
cd node-binary/node/{network}/{version}/{os_type}
```

4. Copy binaries to "/usr/local/bin":
```bash
cp gated gatecli /usr/local/bin
```

5. Create root directory for GateChain node $GATEHOME (i.e., ~/.gated):
```bash
mkdir ~/.gated
```

6. Copy "config.json" and "genesis.json" from "node-binary/node/{network}/{version}/config/" to "$GATEHOME/"

### Method 3: Custom Installation 2
Users can choose download links based on their system requirements.

Note: Please ensure "wget" is installed in your environment

#### For macOS:
```bash
# Download gated
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/mac/gated

# Download gatecli
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/mac/gatecli
```

#### For Linux:
```bash
# Download gated
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/linux/gated

# Download gatecli
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/binary/linux/gatecli
```

#### Download Configuration Files:
```bash
# Download config.json
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/config/config.json

# Download genesis.json
wget https://gatechainbucket.oss-cn-beijing.aliyuncs.com/config/genesis.json
```

Copy downloaded binaries to "/usr/local/bin":
```bash
cp gated gatecli /usr/local/bin
```

Create node root directory:
```bash
mkdir ~/.gated
```

Copy configuration files to "$GATEHOME/"

## Starting the Node

### Basic Start
```bash
gated start
```

### Start with GC Mode
To start in GC mode, modify the start command:
```bash
gated start --pruning nothing
```

### Start EVM RPC
```bash
gatecli evm rest-server --gm-websocket-port http://127.0.0.1:8085 --chain-id mainnet --laddr tcp://0.0.0.0:6060 --rpc-api web3,eth,personal,net,debug
```

For EVM RPC support, modify the following properties in config.json:
```json
"WsPort": "tcp://0.0.0.0:8085"
"IsWebSocketServerActive": true
```
Save changes and restart gated.