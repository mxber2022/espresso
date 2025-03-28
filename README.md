# Current implementation

Deployed contracts available in `nitro-contracts/espresso-deployments/arbSepolia.json`

```json
{
  "EthBridge": "0xad3DEDd73840B4cEcfA1DaFD434DB5437aAA55C4",
  "EthSequencerInbox": "0x62A60C2d82A5Ba5Efc02956a746f290De9226058",
  "EthInbox": "0xEFd7AfF02ef982771C1d7655A9151a675bB08920",
  "EthRollupEventInbox": "0x4a8b93686983fF380b0c11a1aF2448b142F38664",
  "EthOutbox": "0x783d8eE69a37b909Bf5fd988D8bba8C7F99A5a66",
  "ERC20Bridge": "0x0c25c1bF545F634d7b6F215D71995c504F53b9f8",
  "ERC20SequencerInbox": "0x083c2fe2233c33FA307710D9A31073b4A8adf04E",
  "ERC20Inbox": "0x4cD3d5f513294c2545cd7DD410d58748B8175E56",
  "ERC20RollupEventInbox": "0xe7Ef506bC1Ae5aE7fe66e5E9C6D3251651490c64",
  "ERC20Outbox": "0x32aBe1548B8BD7f2C0Ce56B01df17D2b59E6a698",
  "BridgeCreator": "0xad3DEDd73840B4cEcfA1DaFD434DB5437aAA55C4",
  "OneStepProver0": "0x9BC6Ae919D8d40f0a4148342FA3B38d6B08DFea9",
  "OneStepProverMemory": "0xd8027189B57F6eCC7EbB2235C056437f752c4FdF",
  "OneStepProverMath": "0xfd59e32c0b07151AB2269834fD4976Aa4D08781b",
  "OneStepProverHostIo": "0x9e3bdcdB7C6d02517044D2136533db486928537b",
  "OneStepProofEntry": "0xb375fAcCfc8eaB0F3f0A5F82f564fADA1E02BFa4",
  "ChallengeManager": "0x73dA955491ab7f30886D8883Ce569352A9d96819",
  "RollupAdminLogic": "0x7cA6eA2505255C7Bd05DffF2fc4524074c277F75",
  "RollupUserLogic": "0xbf2Fe04D97D5D1EB12e51F835baF1F11A34e4762",
  "UpgradeExecutor": "0x61153F3C05a139d95eCb601A91FAcdd25175517E",
  "ValidatorUtils": "0xDcC0e65A0C8E9C9521f6E9eC3614963e4BD26F57",
  "ValidatorWalletCreator": "0x0e55bE49D3FEF17CFC1D791731Fd608A9499C8CF",
  "RollupCreator": "0x6e35a812cFb342b72c1265b305388baC0B295274",
  "DeployHelper": "0xA5773DBD294BAdB81C8EFBf6Dda84479bBBe5D43"
}
```

Current `.env`

```js
ARBISCAN_API_KEY="FI22AY4KC6U5JCUNZYCFPV8PB698789RNU"
DEVNET_PRIVKEY="CONTRACT_DEPLOYER_PRIVATE_KEY"
ESPRESSO_TEE_VERIFIER_ADDRESS="0x8354db765810dF8F24f1477B06e91E5b17a408bF"
ROLLUP_CREATOR_ADDRESS="0x6e35a812cFb342b72c1265b305388baC0B295274"
```

Returned via CLI on hardhat deployment

```markdown
Congratulations! 🎉🎉🎉 All DONE! Here's your addresses:
RollupProxy Contract created at address: `0x7A6074218a171e57d1198386f9500EC9b0f1e684`
Attempting to verify Rollup contract at address `0x7A6074218a171e57d1198386f9500EC9b0f1e684`
src/rollup/RollupProxy.sol:RollupProxy at `0x7A6074218a171e57d1198386f9500EC9b0f1e684`

Contract RollupProxy is already verified.
Inbox (proxy) Contract created at address: `0xffC822D13e3743fff3fAFE9FC49eC82d6FF9269C`
Outbox (proxy) Contract created at address: `0x00603B7D7B010289C38B42645Aaca34AB2D429C7`
rollupEventInbox (proxy) Contract created at address: `0x340CF68F829d3a4B85958860AB36751c124592f1`
challengeManager (proxy) Contract created at address: `0xA5996Cd20C3D6B1D947Bec3E6908B35f35A43592`
AdminProxy Contract created at address: `0xA917cAdF349ca58621f9499A7f7281532C9108a8`
SequencerInbox (proxy) created at address: `0x09Af9f124E6597Fd6507fd37759E9Cd7795CCAd3`
Bridge (proxy) Contract created at address: `0xf2061896724Da22e583C1918b3d1054035157a08`
ValidatorUtils Contract created at address: `0xDcC0e65A0C8E9C9521f6E9eC3614963e4BD26F57`
ValidatorWalletCreator Contract created at address: `0x0e55bE49D3FEF17CFC1D791731Fd608A9499C8CF`
All deployed at block number: 136646779
```

## Testing the Chain

### To verify your chain is running correctly:

#### Check Confirmed Nodes by the Validator/Staker

```bash
cast call --rpc-url https://arbitrum-sepolia-rpc.publicnode.com 0x7A6074218a171e57d1198386f9500EC9b0f1e684 "latestConfirmed()(uint256)"
```

#### Test bridge functionality:

```bash
cast send --rpc-url https://arbitrum-sepolia-rpc.publicnode.com 0xffC822D13e3743fff3fAFE9FC49eC82d6FF9269C 'depositEth() external payable returns (uint256)' --private-key YOUR_PRIVATE_KEY_WITH_FUNDS  --value 100000000 -vvvv
```

Note: Bridging transactions can take up to 15 minutes to finalize.

#### Verify your balance:

```bash
cast balance 0x1a85310597135633BAe67106f5859Ae3FF7D13cE --rpc-url http://127.0.0.1:8547
```

Test sending transactions:

```bash
cast send ANY_ADDRESS --value 1 --private-key YOUR_PRIVATE_KEY_WITH_FUNDS --rpc-url http://127.0.0.1:8547
```

For a more consistent test, you can also continuously send transactions to the rollup. This approach simulates a more realistic environment by continually submitting transactions, allowing you to see how the system handles ongoing activity. (See the next section for details.)

#### Check recipient balance:

```bash
cast balance ANY_ADDRESS --rpc-url http://127.0.0.1:8547
```

If successful, the recipient's balance should show 1 wei or the amount you sent if different.

### Transaction Flow Generator

If you want to generate test transactions on your rollup, navigate to the tx-generator repository subfolder and follow the README instructions:

```bash
cd tx-generator
```

This script continuously generates transactions to help you evaluate your rollup and the Espresso Network.