# GateChain Governance

GateChain adopts a decentralized governance mechanism that allows token holders to participate in on-chain governance decisions. This article will introduce GateChain's governance mechanism and participation methods.

## Governance Overview

GateChain's governance system allows GT holders to:

- Submit governance proposals
- Vote on proposals
- Participate in important parameter modifications
- Decide on protocol upgrades

## Governance Proposals

### Proposal Types

1. Parameter Change Proposals
   - Modify system parameters
   - Adjust economic model
   - Update governance rules

2. Software Upgrade Proposals
   - Protocol upgrades
   - Feature updates
   - Security fixes

3. Community Fund Usage Proposals
   - Ecosystem building
   - Development incentives
   - Marketing promotion

### Proposal Process

1. Proposal Initiation
   - Requires staking a certain amount of GT
   - Provide detailed proposal description
   - Set voting period

2. Voting Phase
   - Staked GT holders can vote
   - Voting weight proportional to stake amount
   - Three options: Support/Against/Abstain

3. Proposal Execution
   - Automatically executes when passing conditions are met
   - Returns staked GT if not passed
   - Execution results recorded on-chain

## Participation Methods

### 1. Stake GT

- Minimum stake: 1000 GT
- Staking period: No less than 14 days
- Staking rewards: Voting rights and revenue sharing

### 2. Submit Proposal

```bash
POST /v1/gov/submit-proposal
```

Proposal parameters:
- title: Proposal title
- description: Detailed description
- deposit: Stake amount
- voting_period: Voting period

### 3. Voting

```bash
POST /v1/gov/vote
```

Voting parameters:
- proposal_id: Proposal ID
- option: Voting option (Yes/No/Abstain)
- voter: Voter address

## Governance Parameters

| Parameter | Description | Default Value |
|------|------|--------|
| min_deposit | Minimum stake amount | 1000 GT |
| voting_period | Voting period | 14 days |
| quorum | Minimum participation rate | 40% |
| threshold | Passing threshold | 50% |

