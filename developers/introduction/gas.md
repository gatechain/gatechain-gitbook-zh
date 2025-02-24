# GateChain Gas 机制概述

## 什么是 Gas？

在区块链网络中，**Gas** 是指衡量执行操作（如交易或智能合约）所需计算工作量的单位。用户支付 Gas 费用来补偿网络验证者在这些操作中消耗的资源。

## GateChain 的 Gas 机制

GateChain 作为下一代高性能公共区块链，实现了独特的 Gas 机制，以提高网络效率、降低用户交易成本，并增加其原生代币 GT 的稀缺性。

### 引入 EIP-1559 机制

在 GateChain v1.1.6 主网升级中，网络采用了受以太坊 **EIP-1559** 提案启发的费用结构。这种机制将交易费用分为两个部分：

1. **基础费用**：动态调整的费用，反映当前区块空间的需求。这部分费用会被销毁，有效减少 GT 代币的总供应量并增加其稀缺性。
2. **小费**：用户可以包含的可选附加费用，用于激励验证者优先处理他们的交易。

这种机制的优势包括：

- **提高网络效率**：通过动态调整基础费用，网络可以更好地处理不同程度的需求，从而使交易成本更可预测。
- **减少 GT 供应**：销毁基础费用会减少流通中的 GT 总量，可能随时间推移增加其价值。

### Gas 价格和限制调整

除了新的费用机制，GateChain 还对 Gas 价格和区块 Gas 限制进行了调整：

- **最低 Gas 价格**：设置为 10 NanoGT。
- **最大区块 Gas 限制**：设定为 150,000,000。

这些调整旨在优化网络性能并确保高效的交易处理。

## 结论

GateChain 的 Gas 机制通过采用动态费用结构和代币销毁策略，不仅提高了网络效率和降低了用户成本，还增强了 GT 代币的稀缺性，为用户提供了更优质的体验。
