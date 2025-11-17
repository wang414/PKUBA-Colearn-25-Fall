# Week 1 - 智能合约编写与交互

## 目标

通过编写智能合约与靶子合约交互，获取 Flag 并触发 `ProblemSolved` 事件。

## 靶子合约信息

合约地址：`0x4a6C0c0dc8bD8276b65956c9978ef941C3550A1B`

所在网络: Ethereum Sepolia, https://chainlist.org/chain/11155111, 浏览器 https://sepolia.etherscan.io/

可用方法
- `hint()` - 获取解题提示
- `query(bytes32 _hash)` - 提交答案获取 Flag, 该方法只能通过合约调用
- `getSolvers()` - 查看所有完成者地址

## 参考步骤
1. 创建一个智能合约来调用靶子合约的 `hint()` 方法获取解题提示
2. 根据解题提示计算答案
3. 调用靶子合约的`query()` 方法提交答案, 若答案正确, 则能够看到返回的 Flag 或者 ChallengeCompleted 事件

## 注意事项
- 靶子合约要求调用者必须是合约地址，不能直接用钱包调用
- 可以多次尝试，每次成功都会触发事件
- 与合约交互需要消耗 Gas Fee, 可以参考笔试文档来获取测试网代币 https://github.com/aliceyzhsu/crypto-techguy/blob/main/quests/get-ready.md

## 参考资料 

- [Solidity 官方文档](https://docs.soliditylang.org/)
- [Foundry 教程](https://book.getfoundry.sh/)
- [Remix IDE](https://remix.ethereum.org/)
- (欢迎任何同学补充自己学习时用到的资料)

