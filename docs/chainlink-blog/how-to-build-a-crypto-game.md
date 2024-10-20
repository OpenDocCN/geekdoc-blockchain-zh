# 如何建立一个加密游戏

> 原文：<https://blog.chain.link/how-to-build-a-crypto-game/>

这个技术教程将教你如何在以太坊 Goerli 测试网络上构建和部署一个全栈 dApp 加密游戏。您将构建的游戏存储了区块链上的测验问题及其答案。答案通过 `keccak256` 散列，因此您可以验证答案而无需泄露。 `Keccak256` 是单向加密哈希函数，不能反向解码。这意味着检查答案是否正确的方法将是提供一个猜测并散列它。如果两个哈希值匹配，您的答案是正确的。

本教程将使用:

*   [坚实度](https://docs.soliditylang.org/)
*   [戈利](https://goerli.net/)
*   [铸造厂](https://github.com/foundry-rs/foundry)
*   [](https://kit.svelte.dev/)

你可以在下面查看涵盖整个过程的视频教程，在这里访问包含游戏[的 GitHub repo。](https://github.com/smartcontractkit/smart-contract-examples/tree/main/quiz-game)

[https://www.youtube.com/embed/niqxn57vx9k?feature=oembed](https://www.youtube.com/embed/niqxn57vx9k?feature=oembed)

## 准备就绪

### 获得戈利以太

如果你以前没有用过 Goerli，去 [Chainlink Labs 水龙头](https://faucets.chain.link/) 获取一些 testnet ETH。

### 安装铸造车间

在本教程中，您将使用 Foundry 来构建、测试和部署您的 Solidity。你可以在 [Foundry GitHub 上找到说明。](https://github.com/foundry-rs/foundry#installation)

### 初始化项目

在您的终端中输入以下内容:

```
❯ Development mkdir QuizGame
❯ Development cd QuizGame
❯ QuizGame forge init foundry
Initializing /Users/rg/Development/QuizGame/foundry...
Installing ds-test in "/Users/rg/Development/QuizGame/foundry/lib/ds-test", (url: https://github.com/dapphub/ds-test, tag: None)
 Installed ds-test
 Initialized forge project.
❯ Development cd foundry
❯ foundry (main) ✔
```

### 创建您的第一个测试

初始化项目后，Foundry 会在 src 目录下为您创建一个基本合同和测试。

```
❯ src (main) ✔ tree
.
├── Contract.sol
└── test
 └── Contract.t.sol

1 directory, 2 files
```

这些提供了铸造文件结构的基本概念。您可以删除 Contract.sol 和 Contract.t.sol，因为您将创建您的合同和测试。

```
❯ src (main) ✔ rm Contract.sol test/Contract.t.sol
```

在测试目录下创建 QuizGame.t.sol。基本骨架应该是这样的。

```
foundry/src/test/QuizGame.t.sol

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "ds-test/test.sol";
import "../QuizGame.sol";
 interface CheatCodes {
 function deal(address, uint256) external;
}

contract QuizTest is DSTest {
 function setUp() public {}
 function testExample() public {
 assertTrue(true);
 }
}
```

这将允许你通过 forge 测试来确保一切正常。如果您运行测试，它将会由于 QuizGame 合同不可用而失败。这就开始了测试驱动的开发周期:编写测试，看着它失败，修复测试，看着它通过，然后编写另一个失败的测试。在修复失败的测试之前，您可能会看到类似的错误。恭喜你，你的测试不出所料的失败了！

```
Error: 
 0: Compiler run failed
 ParserError: Source "/Users/rg/Development/QuizGame/src/QuizGame.sol" not found: File not found.
 --> /Users/rg/Development/QuizGame/src/test/QuizGame.t.sol:6:1:
 |
 6 | import "../QuizGame.sol";
 | ^^^^^^^^^^^^^^^^^^^^^^^^^
```

在 src 目录下新建一个名为 QuizGame.sol 的文件。

```
foundry/src/QuizGame.sol

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

contract QuizGame {}
```

此时，您的测试应该通过了。

```
❯ src (main) ✘ forge test
[⠢] Compiling...
[⠆] Compiling 2 files with 0.8.13
[⠰] Solc finished in 37.90ms
Compiler run successful

Running 1 test for src/test/QuizGame.t.sol:QuizTest
[PASS] testExample() (gas: 190)
Test result: ok. 1 passed; 0 failed; finished in 1.31ms

❯ src (main) ✘
```

## 创建测验

现在你已经有了游戏合约和测试的框架，你可以编写你的第一个实际测试了。虽然看起来可能不是一个测验，但是您将添加到 setup()函数中的步骤将确保您可以创建一个测验。创建后，您可以检查测验是否正确存储了问题和答案。

```
foundry/src/test/QuizGame.t.sol

contract QuizTest is DSTest {
 QuizGame public game;

    function setUp() public {
 // The salt means pre-generated dictionaries are not valid
 bytes32 salt = bytes32("123123123");
 // Store the answer to the question
 string memory answer = "42";
 // Store the question
 string
 memory question = "What is the answer to life, the universe, and everything?";
 // Store the hashed correct answer
 bytes32 hashedAnswer = keccak256(abi.encodePacked(salt, answer));
 // Create a new game with the question and hashed answer
 game = new QuizGame(question, hashedAnswer);
 emit log(game.question());
 }

 function testExample() public {
 assertTrue(true);
 }
}
```

要通过测试，请更新您的合同。

```
foundry/src/QuizGame.sol

contract QuizGame {
 // The salt means pre-generated dictionaries are not valid this can be
 // changed to any value you want
 bytes32 public salt = bytes32("123123123");
 // Store the answer to the question
 bytes32 public hashedAnswer;
 // Store the question
 string public question;

    // Create the quiz contract with the passed in question and answer
 constructor(string memory _question, bytes32 _hashedAnswer) {
 // Store the hashed answer
 hashedAnswer = _hashedAnswer;
 // Store the question
 question = _question;
 }
}
```

在这一点上，你的契约将存储一个问题和答案，但它没有做太多其他的事情。

## 为任何答案创建测试

一旦你设置了一个问题，你将需要检查玩家提供的猜测是否与存储在测验合同中的答案相匹配。您需要创建一个您知道会失败的测试。我们认为失败是成功的，因为猜测的答案是不正确的。

```
foundry/src/test/QuizGame.t.sol

function testQuizFail() public {
 // This will fail, that mean you need to catch the failure to 'pass' the test
 try game.guess("33") {
 assertTrue(false);
 } catch {
 assertTrue(true);
 }
}
```

这个测试意味着你需要创建一个函数来接受猜测。该功能的一部分是让玩家猜测，并将其与存储的散列答案进行比较。

```
foundry/src/QuizGame.sol

function guess(string calldata answer) public {
 // Check if the answer is correct
 require(
 keccak256(abi.encodePacked(salt, answer)) == hashedAnswer,
 "Incorrect answer"
 );
}
```

这个猜测功能将检查答案是否正确，仅此而已。如果答案是正确的，什么也不会发生。为了给正确的猜测提供奖励，您必须将 ETH 发送到合同并支付给正确的玩家。

## 欺骗交易

Foundry 提供了一套工具来操纵区块链的状态。这些“作弊代码”可以在《铸造之书》中找到。

您将使用的特定作弊代码是 deal，它将允许您为指定的地址设置余额。在协定之外创建一个接口。

```
foundry/src/test/QuizGame.t.sol 
interface CheatCodes {
 function deal(address, uint256) external;
}
```

在契约内，你需要使用这个欺骗代码来创建一个常量欺骗。

```
foundry/src/test/QuizGame.t.sol

contract QuizTest is DSTest {
 CheatCodes constant cheats = CheatCodes(HEVM_ADDRESS);
.
.
.
```

这将允许您创建一个新的测试，向合同发送一些 ETH，然后提交一个正确的答案。

```
foundry/src/test/QuizGame.t.sol

function testQuizPass() public {
 // Get the current balance of this contract
 uint256 beginBalance = address(this).balance;
 // Fund the contract
 cheats.deal(address(game), 10000);
 // Guess the correct answer
 game.guess("42");
 // Check balance after the guess is 10000 more than before
 assertEq(address(this).balance, beginBalance + 10000);
}
```

我们的目标是通过测验的正确答案来支付测试合同的费用。为此，您需要创建一个 fallback()和 receive()函数。

```
foundry/src/test/QuizGame.t.sol

fallback() external payable {}

receive() external payable {}
```

## 回答问题

当一个问题被正确回答时，合同应该把它的余额转移给猜测者。

```
foundry/src/QuizGame.sol

function guess(string calldata answer) public {
 require(
 keccak256(abi.encodePacked(salt, answer)) == hashedAnswer,
 "Incorrect answer"
 );
 // If the contract has a balance, and the answer is correct,
 if (address(this).balance > 0) {
 // send the balance to the guesser
 (bool sent, bytes memory data) = payable(msg.sender).call{value: address(this).balance}("");
 }
}
fallback() external payable {
}

receive() external payable {
}
```

妙极了！此时，您已经有了一份完全有效的测验合同。在开始前端工作之前，还有几个步骤来完成可靠性工作。首先，您需要在 QuizGame 契约中创建一些事件。

## 添加事件

事件将允许你监听契约状态的变化。对于测验，您需要为测验的资金和正确猜测创建一个事件。

在契约的顶部，添加这两个事件。在之后添加它们

```
string public quesiton;

```

```
foundry/src/QuizGame.sol

event QuizFunded(uint256 balance);
event AnswerGuessed();
```

在猜测函数的末尾，加上:

```
emit AnswerGuessed();
```

将以下内容添加到回退和接收功能中，添加:

```
emit QuizFunded(address(this).balance);
```

## 创建工厂

你的问答游戏的最后一块拼图是工厂。工厂合同到底是什么？工厂合同是创建一组其他合同并跟踪它们的合同。您将需要为工厂、合同和测试创建两个新文件。

```
foundry/src/test/QuizFactory.t.sol

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "ds-test/test.sol";
import "../QuizFactory.sol";

contract QuizFactoryTest is DSTest {
 QuizFactory public factory;

 function setUp() public {
 factory = new QuizFactory();
 }
}

```

```
foundry/src/QuizFactory.sol

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "./QuizGame.sol";
 contract QuizFactory {
 constructor() {}
}
```

这个基本工厂还需要一些额外的东西。首先，您应该添加一个测试来测试通过工厂创建的测验。

## 从工厂创建测验

第一步是添加一个测试，根据工厂合同创建一个测验。

```
foundry/src/test/QuizFactory.t.sol

function testCreateQuiz() public {
 // Set Answer
 string memory answer = "42";
 // Set Question
 string
 memory question = "What is the answer to life, the universe, and everything?";
 // Set Hashed Answer
 bytes32 salt = bytes32("123123123");
 bytes32 hashedAnswer = keccak256(abi.encodePacked(salt, answer));
 // Create a new quiz with the question and hashed answer
 factory.createQuiz(question, hashedAnswer);
 // Get the new quiz
 QuizGame quiz = factory.quizzes(0);
 // Check the question
 assertEq(
 keccak256(abi.encodePacked(quiz.question())),
 keccak256(abi.encodePacked(question))
 );
}
```

这项测试需要几样东西。首先，一个 `createQuiz` 功能。它还希望您有一种方法来引用工厂合同中的测验。您将需要创建一个 QuizGames 数组，该数组将公开提供。

在您的 QuizFactory 合同顶部设置阵列。有一个活动也不错。当你开始构建前端，你未来的自己会感谢你。

```
foundry/src/QuizFactory.sol

QuizGame[] public quizzes;
event QuizCreated(QuizGame indexed quiz, address indexed creator);
```

现在你可以构建 createQuiz 函数

```
foundry/src/QuizFactory.sol

function createQuiz(string memory _question, bytes32 _answer) public {
 // Create a new quiz
 QuizGame quiz = new QuizGame(_question, _answer);
 // Add it to the list of quizzes
 quizzes.push(quiz);
 // Emit the event
 emit QuizCreated(quiz, msg.sender);
}
```

您可以添加测验，返回工厂创建的所有测验会很有帮助。

```
foundry/src/test/QuizFactory.t.sol

function testCountquizzes() public {
 // Set Answer
 string memory answer = "42";
 // Set Question
 string
 memory question = "What is the answer to life, the universe, and everything?";
 // Set Hashed Answer
 bytes32 salt = bytes32("123123123");
 bytes32 hashedAnswer = keccak256(abi.encodePacked(salt, answer));
 // Create two new quizzes
 factory.createQuiz(question, hashedAnswer);
 factory.createQuiz(question, hashedAnswer);
 // Get all the quizzes
 QuizGame[] memory quizzes = factory.getQuizzes();
 // Check the number of quizzes
 assertEq(quizzes.length, 2);
}
```

该测试检查返回的测验数量是否符合您的预期。您需要创建函数 getQuizzes，它应该返回一个 QuizGames 数组

```
foundry/src/test/QuizFactory.sol

function getQuizzes() public view returns (QuizGame[] memory col) {
 // Calculate number of quizzes
 uint256 size = quizzes.length;
 // Create a new array for the quizzes
 col = new QuizGame[](size);
 // Copy the quizzes to the new array
 for (uint256 i = 0; i < size; i++) {
 col[i] = quizzes[i];
 }
 // Return the array
 return col;
}
```

## 合同完成！

你做到了！合同已准备好部署！您可以使用这个脚本来部署它。将其保存在项目的根目录下。

```
deploy.sh

#!/usr/bin/env bash

# Read the RPC URL
echo Enter Your RPC URL:
echo Example: "https://eth-goerli.alchemyapi.io/v2//XXXXXXXXXX"
read -s rpc

# Read the contract name
echo Which contract do you want to deploy \(eg Greeter\)?
read contract

forge create ./src/${contract}.sol:${contract} -i --rpc-url $rpc
```

这将允许您将您的合同部署到 Goerli，所有这些都是读取变量，而不显示您在命令行上键入的内容。这将确保您的私钥不会存储在您的命令行历史中。

运行 deploy.sh 后，您应该会看到您的合同部署到了哪里。在下一节构建前端时，您将需要这个地址。

```
Deployer: 0x0000000000000000000000000000000000000000
Deployed to: 0x1234567890123456789012345678901234567890
Transaction hash: 0x1234567890123456789012345678901234567890594be2f670606ada53412aaa
```

## 苗条安装

初始化苗条很简单。要看说明，可以前往 [苗条主页](https://kit.svelte.dev/) 。对于本教程，您应该使用以下内容。这将在 Svelte 目录中创建一个 SvelteKit 框架项目。

```
❯ QuizGame (main) ✘ npm init svelte svelte
Need to install the following packages:
 create-svelte
Ok to proceed? (y) y
create-svelte version 2.0.0-next.139
Welcome to SvelteKit!
This is beta software; expect bugs and missing features.
Problems? Open an issue on https://github.com/sveltejs/kit/issues if none exists already.
✔ Which Svelte app template? › Skeleton project
✔ Add type checking? › None
✔ Add ESLint for code linting? … Yes
✔ Add Prettier for code formatting? … Yes
✔ Add Playwright for browser testing? … No
Your project is ready!
✔ ESLint
 https://github.com/sveltejs/eslint-plugin-svelte3
✔ Prettier
 https://prettier.io/docs/en/options.html
 https://github.com/sveltejs/prettier-plugin-svelte#options

Install community-maintained integrations:
 https://github.com/svelte-add/svelte-adders

Next steps:
 1: cd svelte
 2: npm install (or pnpm install, etc)
 3: git init && git add -A && git commit -m "Initial commit" (optional)
 4: npm run dev -- --open
To close the dev server, hit Ctrl-C
 Stuck? Visit us at https://svelte.dev/chat
❯ QuizGame (main) ✘ cd svelte
```

你还需要在项目中添加醚

```
❯ svelte (main) ✘ npm install ethers
added 43 packages, and audited 180 packages in 1s
51 packages are looking for funding
 run `npm fund` for details
found 0 vulnerabilities
```

你应该能够启动服务器并看到下面的页面。

```
npm run dev -- --open
```

![Screenshot of SvelteKit](img/ccdbd94912348787675e1a789f19154a.png)

## 连接您的钱包

你将需要在 `svelte/src/lib` 目录下创建一个组件，你还将需要创建这个 `lib` 目录。为了开始并确保一切正常，现在在组件中创建一个按钮。

```
svelte/src/lib/WalletConnect.svelte

<button>Attach Wallet</button>
```

然后在 `svelte/src/routes/index.svelte` 内，就可以导入这个新组件了。在完全充实组件之前，确保组件被正确导入是一个很好的实践。它还允许您在通过热重装构建组件时看到增量更改。

```
svelte/src/routes/index.svelte

<script>
 import WalletConnect from '$lib/WalletConnect.svelte';
</script>

<h1>My Quiz</h1>

<WalletConnect />
```

这将为您的页面提供以下更改。

![Svelte My Quiz](img/b281f04c067bde01e5fd9fb99c2ad4b2.png)

一旦这个工作正常，我们就可以构建其余的组件了。我以后不会演示这些步骤，但是请记住在导入组件之前创建它们。

为了在组件之间传递契约和钱包，您需要创建一个存储它们的地方。您可以创建一个 `web3Props` 对象来保存这些信息。

```
svelte/src/lib/WalletConnect.svelte

<script>
 import { ethers } from 'ethers';
 // place holder for the properties we will be passing between components
 export let web3Props = { provider: null, signer: null, account: null, chainId: null };
 // connect the wallet
 async function connectWallet() {
 // get the provider, this time without ethereum object
 let provider = new ethers.providers.Web3Provider(window.ethereum, 'any');
 // prompt user for account connections
 await provider.send('eth_requestAccounts', []);
 // get the signer
 const signer = provider.getSigner();
 // get the account address
 const account = await signer.getAddress();
 // get the chainId
 const chainId = await signer.getChainId();
 // update the props
 web3Props = { signer, provider, chainId, account };
 }
</script>

<button on:click={connectWallet}>Attach Wallet</button>
```

组件更新后，你需要将 index.svelte 中的道具传递给组件。

```
svelte/src/routes/index.svelte

<script>
 import WalletConnect from '$lib/WalletConnect.svelte';

    export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null
 };
</script>

<h1>My Quiz</h1>
{#if !web3Props.account}
 <WalletConnect bind:web3Props />
{:else}
 😎
{/if}
```

![Attach Wallet](img/a11355ce0db869a12d1d26ffa6c188b0.png)

## 创建测验

您已经连接了您的钱包！现在，您可以继续与测验工厂交互来创建问题。

第一步是将两份合同的 ABI 带过来。当通过 Forge 为测试或部署编译合同时，会创建一个包含 ABI 的 JSON 版本的文件；

`out/QuizFactory.sol/QuizFactory.json` 和 `out/QuizGame.sol/QuizGame.json` 都是在铸造目录下创建的。在 `svelte/src` 中新建一个目录，命名为 `contracts` ，将两个文件复制到那里。这些将允许您与契约的已部署版本进行交互。

一旦两个 JSON 文件都保存到新的合同目录中，您就可以创建一个组件来添加测验。

```
svelte/src/lib/AddQuestion.svelte

<script>
 // ethers allows you to interact with the Ethereum blockchain
 import { ethers } from 'ethers';
 // web3Props holds the properties of the web3 provider
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null,
 contract: null
 };
 // values for the quiz factory contract
 $: question = '';
 $: answer = '';
 $: encryptedAnswer = null;
 async function encryptAnswer() {
 // encrypt the answer using the same salt as the contract
 encryptedAnswer = ethers.utils.keccak256(
 ethers.utils.solidityPack(
 ['bytes32', 'string'],
 [ethers.utils.formatBytes32String('123123123'), answer]
 )
 );
 // use the factory contract to create a new quiz
 web3Props.contract.createQuiz(question, encryptedAnswer);
 }
</script>


  question: 
 <!-- bind lets changes to question update the value of the variable  -->
 <input bind:value={question} />
 <br />
  answer: 
 <input bind:value={answer} />
 <br />
 <!-- On click, run the encryptedAnswer function -->
 <button on:click={encryptAnswer}> Add Question </button>

 <!-- Scoped CSS -->
<style>
 .wrapper {
 overflow: hidden;
 position: relative;
 margin-bottom: 1rem;
 padding: 20px;
 border-radius: 15px;
 width: 33%;
 box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.3);
 }
 .input-label {
 display: inline-block;
 width: 15%;
 }
</style>
```

您需要确保您已经将该组件添加到了 `index.svelte`

```
svelte/src/routes/index.svelte

<script>
 import WalletConnect from '$lib/WalletConnect.svelte';

    // NEW
 import AddQuestion from '$lib/AddQuestion.svelte';
 import contractAbi from '../contracts/QuizFactory.json';
 const contractAddr = "<YOUR CONTRACT ADDRESS HERE>;

    export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null
 };
</script>

<h1>My Quiz</h1>
{#if !web3Props.account}
 <WalletConnect bind:web3Props />
{:else}
<!-- NEW -->
 <AddQuestion {web3Props} />
{/if}
```

**请注意:** 您需要上面“合同完成”部分记录的合同地址。这将是 `contractAddr` 的值。

将新值添加到 `index.svelte` 中的 WalletConnect 组件

```
<WalletConnect bind:web3Props {contractAddr} {contractAbi} />
```

将它们添加到组件本身。

```
svelte/src/lib/WalletConnect.svelte

<script>
 import { ethers } from 'ethers';
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null,
 // new prop
 contract: null
 };
 // new variable for the contract address
 export let contractAddr = '';
 // new variable for the contract ABI
 export let contractAbi = { abi: null };

 async function connectWallet() {
 let provider = new ethers.providers.Web3Provider(window.ethereum, 'any');
 await provider.send('eth_requestAccounts', []);
 const signer = provider.getSigner();
 const account = await signer.getAddress();
 const chainId = await signer.getChainId();
 // new contract variable
 const contract = new ethers.Contract(contractAddr, contractAbi.abi, signer);
 // new value for contract
 web3Props = { signer, provider, chainId, account, contract };
 }
</script>
 <button on:click={connectWallet}>Attach Wallet</button>
```

## 显示一个问题

继续补充一个问题。这将使用 `quizFactory` 契约创建一个新的 `quizGame` 。一旦你确认了交易，就可以看到测试了。您需要构建一个问题组件。该组件将显示一个问题。您将重用这个组件来显示所有的问题。

```
svelte/src/lib/Question.svelte

<script>
 import { ethers } from 'ethers';
 // import the single quiz game contract
 import contractAbi from '../contracts/QuizGame.json';
 // place holders for variables
 let answer = null;
 let funding = null;
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null,
 contract: null
 };
 export let questionAddr = null;
 $: question = null;
 $: value = null;
 // funded will determine what CSS and functionality is available
 $: funded = value > 0 ? 'question-funded' : 'question-not-funded';
 let qContract = null;
 async function getQuestion() {
 // get the question contract
 qContract = new ethers.Contract(questionAddr, contractAbi.abi, web3Props.signer);
 // get the question
 question = await qContract.question();
 // get the value of a correct answer
 value = Number(ethers.utils.formatEther(await web3Props.provider.getBalance(questionAddr)));
 // listen for funding
 qContract.on('QuizFunded', (balance) => {
 console.log('QuizFunded', balance);
 value = Number(ethers.utils.formatEther(balance));
 });
 // listen for correct answers
 qContract.on('AnswerGuessed', () => {
 getQuestion();
 });
 }
  // submit a guess to the contract
 async function submitGuess() {
 await qContract.guess(answer);
 }
  // fund the quesiton
 async function fund() {
 web3Props.signer.sendTransaction({
 to: questionAddr,
  value: ethers.utils.parseEther(funding)
 });
 funding = null;
 }
 // run the getQuestion function
 getQuestion();
</script>

<!-- Based on the funding change the CSS class -->

 
 {question}
 
 
 {value} ETH
 
 <input type="text" bind:value={answer} />
 <!-- If the question has no value, disable it -->
 <button on:click={submitGuess} disabled={value <= 0}>Submit Answer</button>
 <br />
 <input type="text" bind:value={funding} />
 <button on:click={fund}>Fund</button>


<style>
 .question-funded {
 background: #4ee44e;
 }
 .question-not-funded {
 background: #ffb6c1;
 }
 .qwrap {
 overflow: hidden;
 position: relative;
 color: white;
 margin-bottom: 1rem;
 padding: 20px;
 border-radius: 15px;
 width: 50%;
 box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.3);
 }
 .question {
 font-size: 2em;
 }
</style>
```

将您的新组件添加到 index.svelte

```
svelte/src/routes/index.svelte

<script>
 import WalletConnect from '$lib/WalletConnect.svelte';
 import AddQuestion from '$lib/AddQuestion.svelte';
 import contractAbi from '../contracts/QuizFactory.json';
 // NEW
 import Question from '$lib/Question.svelte';
 const contractAddr = '0xe7608e790a0ac33014fdeaef9c8bf0c37bf443f0';
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null
 };
</script>

<h1>My Quiz</h1>
{#if !web3Props.account}
 <WalletConnect bind:web3Props {contractAddr} {contractAbi} />
{:else}
 <AddQuestion {web3Props} />
 <!-- NEW -->
 <Question {web3Props} />
{/if}
```

此时，您应该看到以下内容。

![null ETH](img/651ce2948a5fc7014c6e437fc3fe7a9d.png)

这是因为没有传入合同地址。如果你愿意，你可以传入地址，或者继续获取所有的测验。

## 所有测验问题

祝贺你，你已经到达了最后一步！

一旦你有了一个单独的测验组件，你可以恢复你对 `index.svelte` 所做的更改。您将添加一个新组件: `AllQuestions` 。继续创建它。

```
svelte/src/lib/AllQustions.svelte

<script>
 // import your question component
 import Question from './Question.svelte';
 // variables for the contract
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null,
 contract: null
 };
 $: questions = null;
 // get ALL of the questions
 async function getQuestions() {
 questions = await web3Props.contract.getQuizes();
 // listen for new questions
 web3Props.contract.on('QuizCreated', (addr) => {
 console.log('QuizCreated', addr);
 getQuestions();
 });
 }
 getQuestions();
</script>

<!-- If there are questions -->
{#if questions}
 
 <!-- Loop through the questions -->
 {#each questions as questionAddr}
 <!-- Render the question component -->
 <Question {questionAddr} {web3Props} />
 {/each}
 
{/if}

<style>
 .question-wrapper {
 display: flex;
 flex-direction: column;
 justify-content: center;
 align-items: center;
 }
</style>
```

更新 `index.svelte` 使用 AllQuestions

```
svelte/src/routes/index.svelte

<script>
 import WalletConnect from '$lib/WalletConnect.svelte';
 import AddQuestion from '$lib/AddQuestion.svelte';
 import contractAbi from '../contracts/QuizFactory.json';
 // NEW
 import AllQuestions from '$lib/AllQuestions.svelte';
 const contractAddr = '0xe7608e790a0ac33014fdeaef9c8bf0c37bf443f0';
 export let web3Props = {
 provider: null,
 signer: null,
 account: null,
 chainId: null
 };
</script>

<h1>My Quiz</h1>
{#if !web3Props.account}
 <WalletConnect bind:web3Props {contractAddr} {contractAbi} />
{:else}
 <AddQuestion {web3Props} />
 <!-- NEW -->
 <br />
 <br />
 <AllQuestions {web3Props} />
{/if}
```

现在，您所有的测验问题都显示出来了！

![Quiz Answer](img/dd5f2469ee8e7435336ec20dedc0e1f3.png)

在这里，你可以添加更多的测验问题或资助现有的问题。一旦得到资助，你将能够回答他们。

![What is the answer?](img/f6623d7ceaa631965d7834ec082c4f7a.png)

## 摘要

在本教程中，我们已经使用测试驱动开发创建了一组契约，允许我们存储区块链上测验问题的散列答案。这些答案以安全的方式存储，防止参与者作弊。我们还使用参与者的钱包将一个 SvelteKit 前端连接到区块链，并允许他们添加和回答问题。

从这里你可以建立更完整的测验部分，或者在前端的显示上工作。一个巧妙的想法是使用[chain link Automation](https://chain.link/automation)来限制回答问题的时间窗口，或者允许多个“赢家”在最后分享奖金。

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。要讨论集成，[联系专家。](https://chainlinkcommunity.typeform.com/to/OYQO67EF)T15】