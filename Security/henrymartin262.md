---
timezone: UTC+8
---
# 你的名字

1. 自我介绍
   henry, 软件与微电子学院三年级网安方向，目前小白，想深入学习合约安全
2. 你认为你会完成这次共学小组吗？
   可以
3. 你感兴趣的小组
   合约安全小组
4. 你的联系方式（Wechat or Telegram）
   Wechat：bsd_crow

## Notes

<!-- Content_START -->

### 2025.11.22

#### Part I - 动手部署一个智能合约

注册metamask钱包，然后通过以下两个水龙头网站获取测试币（没有主网eth要求）

> https://cloud.google.com/application/web3/faucet/ethereum/sepolia
>
> https://faucet.metana.io/#

https://remix.ethereum.org/ 部署合约，

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract HelloWeb3 {
    event Greeting(address indexed sender, uint256 timestamp);
  
    constructor() {}

    function hello() external {
        emit Greeting(msg.sender, block.timestamp);
    }
```

然后按步骤进行操作，最后查看交易信息


![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_192540_201dbb50-6a41-43e2-a967-5ea556a69bb2.png)


![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_192548_Snipaste_2025-11-22_18-23-45.png)

#### Part II - 智能合约编写



```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// 靶子合约接口（根据题目给的方法名来写）
interface ITarget {
    function hint() external view returns (string memory);
    function query(bytes32 _hash) external returns (string memory);
    function getSolvers() external view returns (address[] memory);
}

contract Week1Solver {
    ITarget public target;

    // 保存最近一次 query 的返回结果（例如 Flag）
    string public lastResult;

    // 方便在日志里看到返回值
    event QueryResult(string result);

    constructor(address _target) {
        target = ITarget(_target);
    }

    // 调靶子合约的 hint，拿到提示
    function getHint() external view returns (string memory) {
        return target.hint();
    }

    // 帮助你在链上算 hash
    function calcHash(string memory s) external pure returns (bytes32) {
        return keccak256(abi.encodePacked(s));
    }

    // 真正提交答案的函数，接收并返回 query 的字符串结果
    function solve(bytes32 answer) external returns (string memory) {
        // 调用靶子合约，拿到返回的字符串（例如 Flag）
        string memory res = target.query(answer);

        // 存一份到状态变量，方便用 lastResult() 查看
        lastResult = res;

        // 打事件，方便在区块浏览器 / Remix Logs 里看
        emit QueryResult(res);

        // 同时作为返回值返回（在 Remix 的 decoded output 里看）
        return res;
    }

    // 直接从靶子合约读取完成者列表
    function getSolversFromTarget() external view returns (address[] memory) {
        return target.getSolvers();
    }
}
```

代码如上

![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_192346_Snipaste_2025-11-22_18-55-35.png)

返回结果如上，提示对 `PKUBlockchain` 进行keccak哈希，然后在链上算出 keccak256("PKUBlockchain")，然后把这个 bytes32 传给 query()





![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_192321_Snipaste_2025-11-22_19-20-43.png)

成功获取到flag，前往 https://sepolia.etherscan.io 查看事件信息，是否成功提交


![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_190703_Snipaste_2025-11-22_19-03-18.png)

确认

![image](https://github.com/henrymartin262/PKUBA-Colearn-25-Fall/blob/main/img//20251122_190534_Snipaste_2025-11-22_19-03-42.png)

<!-- Content_START -->

### 2025.07.11

笔记内容

### 2025.07.12

<!-- Content_END -->
