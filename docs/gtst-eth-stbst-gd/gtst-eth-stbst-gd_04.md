© 作者，独家许可给 APress Media, LLC, Springer Nature 2022。

# 4. 智能合约的单元测试

Davi Pedro Bauer（作者） Campo Bom, Rio Grande do Sul, Brazil

单元测试用于测试代码执行场景，并确保其行为符合预期。至关重要的是，单元测试允许您重构代码并进行新更改，而不会破坏现有行为。

在智能合约中，单元测试更加重要，因为一旦部署合约，就不再可能修复它，除非您部署一个新的合约。因此，将单元测试纳入您编写的所有智能合约中至关重要，寻求尽可能广泛的覆盖范围。

在本章中，您将学习如何使用 Mocha 作为测试运行器和 Chai 作为断言库编写单元测试。

在本章末尾，您将能够执行以下操作：

+   创建一个单元测试文件

+   为智能合约编写单元测试

+   编写测试断言

+   运行单元测试

+   检查单元测试结果

## 为 ERC-20 智能合约编写单元测试

Truffle 默认具有自动化测试框架，因此测试您的合约变得更加容易。该框架允许您以各种方式创建基本且易管理的测试。让我们开始编写我们的第一个单元测试。

### 创建一个新的单元测试文件

打开一个新的终端并执行以下命令：$ truffle create test erc20FixedSupply

### 为总供应合约编写测试

在文件 ERC20FixedSupply.js 中，编写一个新的测试来断言合约创建时固定供应了 1,000 枚代币。const erc20FixedSupply = artifacts.require("erc20FixedSupply");contract("erc20FixedSupply", function () {    it("应该断言为真", async function() {        let token = await erc20FixedSupply.deployed();        let name = await token.name();        assert.equal(name, 'Fixed');    });    it("应该返回总供应量为 1000", async function() {        const instance = await erc20FixedSupply.deployed();        const totalSupply = await instance.totalSupply();        assert.equal(totalSupply, 1000);    });});使用以下命令进行测试：$ truffle test --network development

确保测试能够通过。

### 为余额合约编写测试断言

在文件 ERC20FixedSupply.js 中，添加一个额外的测试来断言在两个账户之间进行新转账后余额是否正确。it("应该转账 150 FIX", async function(){    const instance = await erc20FixedSupply.deployed();    await instance.transfer(account[1], 150);    const balanceAccount0 = await instance.balanceOf(accounts[0]);    const balanceAccount1 = await instance.balanceOf(accounts[1]);    assert.equal(balanceAccount0.toNumber(), 850);    assert.equal(balanceAccount1.toNumber(), 150);});

### 运行单元测试

现在，再次执行测试。$ truffle test --network development

再次确保所有测试都通过。如果单元测试通过，会出现绿色勾号；否则，会出现红色 X 符号。

### 检查单元测试结果

确保你得到的输出与图 4-1 所示的一致。![](img/521550_1_En_4_Fig1_HTML.jpg)

V S 代码的屏幕快照显示了以下输出。合约名：e r c 20 FixedSupply。检查标记：应该断言为真，72 毫秒。检查标记：应该返回 1000 的总供应量，83 毫秒。检查标记：应该转账 150 FIX，494 毫秒，3 个通过，776 毫秒。

图 4-1

VS Code：单元测试结果成功

尝试更改一些值，比如账户余额，看看结果如何从通过变为失败，如图 4-2 所示。it("应该转账 150 FIX", async function(){    const instance = await erc20FixedSupply.deployed();    await instance.transfer("account[1]", 150);    const balanceAccount0 = await instance.balanceOf(accounts[0]);    const balanceAccount1 = await instance.balanceOf(accounts[1]);    assert.equal(balanceAccount0.toNumber(), 750);    assert.equal(balanceAccount1.toNumber(), 250);});![](img/521550_1_En_4_Fig2_HTML.jpg)

V S 代码的屏幕快照显示了以下输出。合约名：e r c 20 FixedSupply；检查标记：应该断言为真：51 毫秒；检查标记：应该返回 1000 的总供应量，51 毫秒；1，应该转账 150 FIX。下一节介绍了测试过程中发出的事件以及它们的详细解释。

图 4-2

VS Code：单元测试结果失败

## 总结

在本章中，你学习了为智能合约编写单元测试的重要性，并写出了你的第一个单元测试。

在下一章中，我们将探讨 ERC-721 代币标准以及它与 ERC-20 的区别。此外，你将学会如何按照这一标准创建和部署合约。
