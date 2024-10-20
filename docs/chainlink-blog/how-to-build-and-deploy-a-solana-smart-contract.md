# 如何构建和部署 Solana 智能合同

> 原文：<https://blog.chain.link/how-to-build-and-deploy-a-solana-smart-contract/>

如果你想学习如何开发 Solana [智能合同](https://chain.link/education/smart-contracts)和程序，那么你来对地方了。

Solana 是一个新兴的高性能、无许可的区块链，它提供快速、廉价和可扩展的交易，并支持使用 Rust、C++和 C 编程语言构建的智能合约。

在这篇技术文章中，我们将通过 Solana Devnet 集群上的智能合同编写、部署和交互的例子，以及如何在您的 Solana 智能合同中使用 Chainlink 价格提要。

## Solana 的架构和编程模型

Solana 是一款高性能区块链，每秒能够处理数千个事务，阻塞时间低于每秒。它通过拜占庭容错(BFT)共识机制来实现这一点，该机制利用了一种新的创新加密函数，称为 [历史证明](https://medium.com/solana-labs/proof-of-history-a-clock-for-blockchain-cf47a61a9274) 。

### 历史的证明

历史证明(PoH)通过使用高频 [可验证延迟函数](https://eprint.iacr.org/2018/601.pdf) ，或 VDF，建立事件(在本例中为交易)随时间的可加密验证顺序。本质上，这意味着 PoH 就像一个密码时钟，帮助网络在时间和事件顺序上达成一致，而不必等待来自其他节点的消息。就像一个 [古水钟](https://en.wikipedia.org/wiki/Water_clock) 可以通过观察水位上升来记录时间的流逝一样，历史的连续输出证明了不断散列的区块链状态给出了事件随时间推移的可验证顺序。

这有助于提高网络性能，因为它允许对有序事件进行并行处理，这与传统的区块链场景相反，在传统场景中，单个进程会验证并将所有事务捆绑到下一个块中。

一个简单的类比是想象一个 100 块的大拼图。在正常情况下，一个或多个人需要一定的时间来完成这个难题。但是想象一下，如果事先所有的拼图块都印上了与它们的位置相对应的数字，从拼图的左上到右下，并按顺序排成一行。因为拼图块的确切顺序和它们在拼图中的位置是预先知道的，所以通过让多个人各专注于一个部分，可以更快地解决拼图。这就是随着时间的推移拥有可证实的事件序列对共识机制的影响；它允许将处理分解成多个并行的过程。

### 智能合同架构

Solana 提供了一种与传统的 EVM 区块链不同的智能合同模式。在传统的基于 EVM 的链中，契约代码/逻辑和状态被组合成在链上部署的单个契约。使用 Solana，智能契约(或 [程序](https://docs.solana.com/developing/on-chain-programs/overview) )是只读的或无状态的，只包含程序逻辑。部署后，智能合同可以通过外部 [账户](https://docs.solana.com/developing/programming-model/accounts) 进行交互。与程序交互的帐户存储与程序交互相关的数据。这创建了状态(帐户)和契约逻辑(程序)的逻辑分离。这是索拉纳和 EVM 智能合约的关键区别。以太坊上的账户和索拉纳上的账户不一样。Solana 帐户可以存储数据(包括钱包信息)，这与以太坊帐户相反，以太坊帐户是对人们钱包的引用。

除此之外，Solana 还提供了一个 CLI 和[JSON RPC API](https://docs.solana.com/developing/clients/jsonrpc-api)，分散式应用程序可以使用它们与 Solana 区块链进行交互。他们也可以使用现有的[SDK](http://https//www.solana.com/developers)中的一个，它允许客户端与区块链和索拉纳程序对话。

![High-level representation of the Solana development workflow. Source: Solana documentation](img/0ae7ca04d9753420d4e9f838b2ecbbc8.png)

<figcaption id="caption-attachment-2425" class="wp-caption-text">High-level representation of the Solana development workflow. Source: [Solana documentation](https://solana.com/news/getting-started-with-solana-development)</figcaption>



## 部署您的第一份 Solana 智能合同

[https://www.youtube.com/embed/7l1P3xzr7Jo?feature=oembed](https://www.youtube.com/embed/7l1P3xzr7Jo?feature=oembed)

在本节中，您将创建并部署您的第一个“hello world”Solana 程序，该程序用 [Rust](https://www.rust-lang.org/) 编写。

### 要求

在继续之前，应安装以下软件:

*   [NodeJS v14 以上&NPMT3】](https://nodejs.org/)
*   最新稳定 [生锈](https://rustup.rs/) 打造
*   [索拉纳 CLI](https://docs.solana.com/cli/install-solana-cli-tools) v1.7.11 或更高版本
*   [去](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 去

### hello world 程序

[hello world 程序](https://github.com/solana-labs/example-helloworld/blob/master/src/program-rust/src/lib.rs) 是一个智能合约，它将输出打印到控制台，并计算给定帐户调用该程序的次数，将次数存储在链上。让我们把代码分成几个独立的部分。

第一部分定义了一些标准的 Solana 程序参数，并定义了程序的入口点(“process_instruction”函数)。除此之外，它还使用 [borsh](https://borsh.io/) 来序列化和反序列化传递给部署程序的参数。

```
use borsh::{BorshDeserialize, BorshSerialize};
use solana_program::{
    account_info::{next_account_info, AccountInfo},
    entrypoint,
    entrypoint::ProgramResult,
    msg,
    program_error::ProgramError,
    pubkey::Pubkey,
};

/// Define the type of state stored in accounts
#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct GreetingAccount {
    /// number of greetings
    pub counter: u32,
}

// Declare and export the program's entrypoint
entrypoint!(process_instruction);

```

process_instruction 函数接受 program_id 和 accountInfo，program _ id 是程序部署到的公钥，account info 是要向其问好的帐户。

```
pub fn process_instruction(
    program_id: &Pubkey, // Public key of the account the hello world program was loaded into
    accounts: &[AccountInfo], // The account to say hello to
    _instruction_data: &[u8], // Ignored, all helloworld instructions are hellos

```

程序结果是程序的主要逻辑所在。在这种情况下，它只是打印一条消息，然后通过循环“accounts”来选择帐户。然而，在我们的例子中，将只有一个帐户。

```
    ) -> ProgramResult {
    msg!("Hello World Rust program entrypoint");

    // Iterating accounts is safer then indexing
    let accounts_iter = &mut accounts.iter();

    // Get the account to say hello to
    let account = next_account_info(accounts_iter)?;

```

接下来，程序检查该帐户是否有权修改指定帐户的数据。

```
    // The account must be owned by the program in order to modify its data
    if account.owner != program_id {
        msg!("Greeted account does not have the correct program id");
        return Err(ProgramError::IncorrectProgramId);
    }

```

最后，该函数获取现有账户的存储号码，将该值加 1，写回结果，并显示一条消息。

```
    // Increment and store the number of times the account has been greeted
    let mut greeting_account = GreetingAccount::try_from_slice(&account.data.borrow())?;
    greeting_account.counter += 1;
    greeting_account.serialize(&mut &mut account.data.borrow_mut()[..])?;

    msg!("Greeted {} time(s)!", greeting_account.counter);

    Ok(())

```

### 部署程序

第一步是克隆存储库。

```
git clone https://github.com/solana-labs/example-helloworld
cd example-helloworld

```

一旦完成，你就可以将当前环境设置为 [devnet](https://docs.solana.com/clusters#devnet) 。这是 Solana 开发人员编写和测试智能合同的测试网络。

```
 solana config set --url https://api.devnet.solana.com

```

接下来，您需要为您的帐户创建一个新的 [密钥对](https://docs.solana.com/terminology#keypair) 。这是与 Solana devnet 上部署的程序(智能合同)进行交互所必需的。请注意: [这是一个不安全的存储密钥的方法](https://docs.solana.com/wallet-guide/cli#file-system-wallet-security) ，只能用于演示目的。出于安全原因，系统会提示您输入密码。

```
 solana-keygen new --force

```

现在您已经创建了一个帐户，您可以使用 [airdrop 程序](https://docs.solana.com/cli/transfer-tokens) 获得一些 SOL 代币。您将需要一些 lamports(SOL 令牌的一部分)来部署您的智能合约。此命令要求将 SOL 令牌存入您新生成的帐户:

```
 solana airdrop 2 

```

现在，您已经准备好构建 hello world 程序了。您可以通过运行下面的命令来构建它

```
npm run build:program-rust

```

![compiling the program](img/57f39609cbba99860e208b7b3dd946d4.png)

<figcaption id="caption-attachment-2421" class="wp-caption-text">Compiling the program</figcaption>



一旦程序构建完成，您就可以将它部署到 devnet。前面命令的输出将给出您需要运行的命令，但它应该类似于下面的内容:

```
 solana program deploy dist/program/helloworld.so

```

最终结果是，您已经成功地将 hello world 程序部署到 devnet，并分配了一个程序 Id。然后可以在[Solana Devnet explorer](https://explorer.solana.com/?cluster=devnet)上查看。

![Deploying the program](img/b226c9aaf49e846e299f130ab4d71b51.png)

<figcaption id="caption-attachment-2422" class="wp-caption-text">Deploying the program</figcaption>



![Viewing the deployed program on the Devnet explorer](img/f82622872b9d2b025f64f9736adcaa3c.png)

<figcaption id="caption-attachment-2423" class="wp-caption-text">Viewing the deployed program on the [Devnet explorer](https://explorer.solana.com/?cluster=devnet)</figcaption>



### 与部署的程序交互

为了与部署的程序进行交互，hello-world 存储库中包含了一个 [简单客户端](https://github.com/solana-labs/example-helloworld/tree/master/src/client) 。这个客户端是使用[Solana web 3 . js SDK](https://github.com/solana-labs/solana-web3.js)和[Solana RPC API](https://docs.solana.com/developing/clients/jsonrpc-api)用类型脚本编写的。

#### 客户端

客户端入口点是 [main.ts](https://github.com/solana-labs/example-helloworld/blob/master/src/client/main.ts) 文件，它以特定的顺序执行许多任务，其中大部分任务都包含在[hello _ world . ts](https://github.com/solana-labs/example-helloworld/blob/master/src/client/hello_world.ts)文件中。

首先，客户端通过调用“建立连接”函数建立与集群的连接

```
export async function establishConnection(): Promise {
  const rpcUrl = await getRpcUrl();
  connection = new Connection(rpcUrl, 'confirmed');
  const version = await connection.getVersion();
  console.log('Connection to cluster established:', rpcUrl, version);
}

```

然后，它调用“establishPayer”函数来确保有一个帐户可用于支付交易，并在需要时创建一个帐户。

```
export async function establishPayer(): Promise {
  let fees = 0;
  if (!payer) {
    const {feeCalculator} = await connection.getRecentBlockhash();

    // Calculate the cost to fund the greeter account
    fees += await connection.getMinimumBalanceForRentExemption(GREETING_SIZE);

    // Calculate the cost of sending transactions
    fees += feeCalculator.lamportsPerSignature * 100; // wag

    payer = await getPayer();
  }

```

客户端然后调用‘check program’函数，该函数从 *加载已部署程序的密钥对。/dist/program/hello world-key pair . JSON*并使用密钥对的公钥来获取程序帐户。如果程序不存在，客户端会停止运行，并显示一个错误。如果程序确实存在，它将创建一个新的帐户，将该程序指定为其所有者，以存储程序状态，在本例中是程序已经执行的次数。

```
 export async function checkProgram(): Promise {
  // Read program id from keypair file
  try {
    const programKeypair = await createKeypairFromFile(PROGRAM_KEYPAIR_PATH);
    programId = programKeypair.publicKey;
  } catch (err) {
    const errMsg = (err as Error).message;
    throw new Error(
      `Failed to read program keypair at '${PROGRAM_KEYPAIR_PATH}' due to error: ${errMsg}. Program may need to be deployed with \`solana program deploy dist/program/helloworld.so\``,
    );
  }

  // Check if the program has been deployed
  const programInfo = await connection.getAccountInfo(programId);
  if (programInfo === null) {
    if (fs.existsSync(PROGRAM_SO_PATH)) {
      throw new Error(
        'Program needs to be deployed with `solana program deploy dist/program/helloworld.so`',
      );
    } else {
      throw new Error('Program needs to be built and deployed');
    }
  } else if (!programInfo.executable) {
    throw new Error(`Program is not executable`);
  }
  console.log(`Using program ${programId.toBase58()}`);

  // Derive the address (public key) of a greeting account from the program so that it's easy to find later.
  const GREETING_SEED = 'hello';
  greetedPubkey = await PublicKey.createWithSeed(
    payer.publicKey,
    GREETING_SEED,
    programId,
  );

```

然后，客户端通过调用“sayHello”函数建立并向程序发送一个“hello”事务。该事务包含一条指令，该指令包含要调用的 helloworld 程序帐户的公钥，以及客户端希望与之打招呼的帐户。每当客户端对某个帐户执行此交易时，程序都会在目标帐户的数据存储中增加一个计数。

```

  export async function sayHello(): Promise {
  console.log('Saying hello to', greetedPubkey.toBase58());
  const instruction = new TransactionInstruction({
    keys: [{pubkey: greetedPubkey, isSigner: false, isWritable: true}],
    programId,
    data: Buffer.alloc(0), // All instructions are hellos
  });
  await sendAndConfirmTransaction(
    connection,
    new Transaction().add(instruction),
    [payer],
  );
}

```

最后，客户端通过调用‘report greetings’ 查询账户数据，以检索账户当前被 sayHello 交易调用的次数

```
 export async function reportGreetings(): Promise {
  const accountInfo = await connection.getAccountInfo(greetedPubkey);
  if (accountInfo === null) {
    throw 'Error: cannot find the greeted account';
  }
  const greeting = borsh.deserialize(
    GreetingSchema,
    GreetingAccount,
    accountInfo.data,
  );
  console.log(
    greetedPubkey.toBase58(),
    'has been greeted',
    greeting.counter,
    'time(s)',
  );

```

#### 运行客户端

在运行客户端从您部署的程序中读取数据之前，您需要安装客户端依赖项。

```
npm install

```

完成后，您就可以启动客户端了。

```
npm run start

```

您应该会看到显示您的程序成功执行的输出，它应该会显示该帐户被问候的次数。随后的运行应该会增加这个数字。

![Starting the Hello World client to interact with the deployed program](img/6a3628869bef60a093b41541ccdbc7f0.png)

<figcaption id="caption-attachment-2424" class="wp-caption-text">Starting the Hello World client to interact with the deployed program</figcaption>



祝贺您，您已经在 devnet 网络上部署了 Solana 智能合同并与之进行了互动！现在我们将深入到另一个 Solana 程序和客户端的例子，除了这次我们将使用 Chainlink 价格提要。

## 索拉纳上链价格

索拉纳 上的 DeFi 应用生态系统正在加速成长。为了支持基本的 DeFi 机制和执行关键的链上功能，如以公平的市场价格发放贷款或清算抵押不足的头寸，这些 dApps 需要访问高度可靠和高质量的市场数据。

Solana [在 Solana Devnet 上集成了 Chainlink Price Feeds](https://www.prnewswire.com/news-releases/chainlink-price-feeds-now-live-on-the-solana-devnet-301362197.html) ，为开发者提供高度分散、高质量的 高速 价格参考数据更新，用于构建 [混合智能合约](https://blog.chain.link/hybrid-smart-contracts-explained/) 。

结合 Solana 每秒支持高达 65，000 笔交易的能力及其极低的交易费用，[chain link Price Feeds](https://data.chain.link/)有潜力增强 DeFi 协议基础设施，在交易执行和风险管理质量方面可与传统金融系统竞争。

在接下来的 [代码示例](https://github.com/smartcontractkit/solana-starter-kit) 中，我们将部署一个 Solana 程序并与之交互，该程序使用 Solana devnet 集群上的 Chainlink 价格提要。

### 要求

*   [NodeJS v14 以上&NPMT3】](https://nodejs.org/)
*   最新稳定 [生锈](https://rustup.rs/) 打造
*   [索拉纳 CLI](https://docs.solana.com/cli/install-solana-cli-tools) v1.7.11 或更高版本
*   [去](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) 去

### chain link Solana 入门套件

[Solana Starter Kit](https://github.com/smartcontractkit/solana-starter-kit)是一个预打包的存储库，它包含一个智能契约，该契约简单地连接到 devnet 上的 Chainlink Price Feed 帐户，并检索和存储指定价格对 [的最新价格](https://docs.chain.link/docs/solana/data-feeds-solana/) 到一个帐户中，然后由离线客户端读取。初学者工具包使用 [锚框架](https://github.com/project-serum/anchor) ，该框架有助于抽象在 Solana 上构建智能合同的一些复杂性。

Solana 上的 Chainlink 价格馈送都使用一个程序，每个单独的价格馈送都是一个单独的帐户，使用该程序存储价格更新。这个演示的工作方式是一个离线客户端将一个帐户传递给在线程序，然后在线程序获取指定价格提要的最新价格，并将该值存储在传递的帐户中。最后，离线客户端从账户中读取价格数据。

第一节 [智能契约](https://github.com/smartcontractkit/solana-starter-kit/blob/main/programs/chainlink_solana_demo/src/lib.rs) 由正常包含和声明使用的锚框架组成。它还声明了锚 所要求的节目 ID [。除此之外，还定义了一个](https://book.anchor-lang.com/chapter_3/high-level_overview.html) [结构](https://doc.rust-lang.org/book/ch05-01-defining-structs.html) 用于将价格反馈答案存储到传入的帐户中，以及一个“fmt”函数用于格式化检索到的价格数据。

```
use anchor_lang::prelude::*;
use anchor_lang::solana_program::system_program;

use chainlink_solana as chainlink;

declare_id!("JC16qi56dgcLoaTVe4BvnCoDL6FhH5NtahA7jmWZFdqm");

#[account]
pub struct Decimal {
    pub value: i128,
    pub decimals: u32,
}

impl Decimal {
    pub fn new(value: i128, decimals: u32) -> Self {
        Decimal { value, decimals }
    }
}

impl std::fmt::Display for Decimal {
    fn fmt(&self, f: &mut std::fmt::Formatter<'_>) -> std::fmt::Result {
        let mut scaled_val = self.value.to_string();
        if scaled_val.len() <= self.decimals as usize {
            scaled_val.insert_str(
                0,
                &vec!["0"; self.decimals as usize - scaled_val.len()].join(""),
            );
            scaled_val.insert_str(0, "0.");
        } else {
            scaled_val.insert(scaled_val.len() - self.decimals as usize, '.');
        }
        f.write_str(&scaled_val)
    }
}

```

接下来，程序声明一个“chain link _ Solana _ demo`[模块](https://doc.rust-lang.org/rust-by-example/mod.html) 用于获取价格数据，该模块包含“执行”功能。

“执行”功能是程序的一部分，包含智能合同的主要逻辑。通过调用从 GitHub 通过[cargo . toml](https://github.com/smartcontractkit/solana-starter-kit/blob/main/Cargo.toml)文件导入的[chain link-Solana package](https://github.com/smartcontractkit/chainlink-solana)中的‘latest _ round _ data’函数，从指定的 [进给地址](https://docs.chain.link/docs/solana-price-feeds/) 中检索最新的回合数据。该函数通过格式化和存储传递给程序的指定帐户的价格，并将结果写入程序输出来完成。

```
#[program]
pub mod chainlink_solana_demo {
    use super::*;
        pub fn execute(ctx: Context) -> ProgramResult  {
        let round = chainlink::latest_round_data(
            ctx.accounts.chainlink_program.to_account_info(),
            ctx.accounts.chainlink_feed.to_account_info(),
        )?;

        let description = chainlink::description(
            ctx.accounts.chainlink_program.to_account_info(),
            ctx.accounts.chainlink_feed.to_account_info(),
        )?;

        let decimals = chainlink::decimals(
            ctx.accounts.chainlink_program.to_account_info(),
            ctx.accounts.chainlink_feed.to_account_info(),
        )?;

        // Set the account value
        let decimal: &mut Account = &mut ctx.accounts.decimal;
        decimal.value=round.answer;
        decimal.decimals=u32::from(decimals);

        // Also print the value to the program output
        let decimal_print = Decimal::new(round.answer, u32::from(decimals));
        msg!("{} price is {}", description, decimal_print);
        Ok(())
    }

```

## 部署程序

第一步是克隆存储库。

```
git clone https://github.com/smartcontractkit/solana-starter-kit
cd solana-starter-kit

```

完成后，您就可以安装所需的依赖项，包括 Anchor 框架。

```
npm install

```

**关于[苹果 M1](https://en.wikipedia.org/wiki/Apple_M1) 芯片组**的注意事项:您将需要执行额外的步骤来从源代码手动安装 Anchor 框架，因为 NPM 软件包目前仅支持 x86_64 芯片组，请运行以下命令来手动安装:

```
cargo install --git https://github.com/project-serum/anchor --tag v0.20.1 anchor-cli --locked
```

接下来，您需要为您的帐户创建一个新的 [密钥对](https://docs.solana.com/terminology#keypair) 。这是与 Solana devnet 集群上部署的程序(智能合同)进行交互所必需的。同样， [这是一个不安全的方法](https://docs.solana.com/wallet-guide/cli#file-system-wallet-security) 用于存储密钥，应该只用于演示目的。出于安全原因，系统会提示您输入密码。

```
solana-keygen new -o id.json

```

现在您已经创建了一个帐户，您可以使用 [airdrop 程序](https://docs.solana.com/cli/transfer-tokens) 获得一些 SOL 代币。您将需要一些 lamports(SOL 令牌的一部分)来部署您的程序。此命令为您新生成的帐户请求 SOL 令牌。我们将需要调用两次，因为 Devnet 龙头被限制为 2 SOL，而我们大约需要 4 SOL。

```
solana airdrop 2 $(solana-keygen pubkey ./id.json) --url https://api.devnet.solana.com && solana airdrop 2 $(solana-keygen pubkey ./id.json) --url https://api.devnet.solana.com

```

您现在已经准备好使用 [锚框架](https://book.anchor-lang.com/chapter_1/introduction.html) 构建 Chainlink Solana 演示程序了！

```
anchor build

```

![Building the program with Anchor](img/6ccb2e62404bdbc89d8a9748b48bc563.png)

<figcaption id="caption-attachment-3293" class="wp-caption-text">Building the program with Anchor</figcaption>



构建过程为你的程序账户生成密钥对。在部署程序之前，必须将这个公钥添加到 lib.rs 文件中，因为使用 Anchor 的程序需要这个公钥。为此，您需要从。Anchor 使用以下命令生成的/target/deploy/chain link _ Solana _ demo-key pair . JSON 文件:

```
solana address -k ./target/deploy/chainlink_solana_demo-keypair.json

```

下一步是编辑 lib.rs 文件并替换 declare_id 中的 keypair！()用上一步得到的值定义:

```
declare_id!("JC16qi56dgcLoaTVe4BvnCoDL6FhH5NtahA7jmWZFdqm");
```

接下来，你还需要将获得的程序 ID 值插入到 chainlink_solana_demo devnet 定义中的 Anchor.toml 文件中

```
[programs.devnet]
chainlink_solana_demo = "JC16qi56dgcLoaTVe4BvnCoDL6FhH5NtahA7jmWZFdqm"

```

最后，因为您用生成的程序 ID 更新了源代码，所以您需要重新构建程序，然后它可以部署到 devnet

```
anchor build
anchor deploy --provider.cluster devnet

```

![Deploying the program with Anchor](img/1791b99cd24b02b4cfcc9bc19ca17a32.png)

<figcaption id="caption-attachment-3294" class="wp-caption-text">Deploying the program with Anchor</figcaption>



一旦您成功部署了程序，终端输出将指定程序的程序 ID，它应该与您插入到 lib.rs 文件和 Anchor.toml 文件中的值相匹配。再次注意这个程序 ID，因为在执行客户机时需要它。然后可以在[Solana Devnet explorer](https://explorer.solana.com/?cluster=devnet)上查看。

![Building the program with Anchor](img/70fb9a0066dba62b85c9ca40aac4a4c0.png)

<figcaption id="caption-attachment-3291" class="wp-caption-text">Viewing the deployed program on the Solana Devnet explorer</figcaption>



### 与部署的程序交互

为了与部署的程序进行交互，Chainlink Solana 演示库包含一个用 JavaScript 编写的 [客户端](https://github.com/smartcontractkit/solana-starter-kit/blob/main/client.js) ，使用 [锚框架](https://book.anchor-lang.com/chapter_1/introduction.html) 和[Solana web 3 API](https://solana-labs.github.io/solana-web3.js)。

#### 客户端

客户端是一个 JavaScript 脚本，它接受两个参数，一个部署的程序 ID，一个 [价格馈送帐户地址](https://docs.chain.link/docs/solana/data-feeds-solana/) 。然后，它创建一个到已部署程序的连接，并传入指定的价格提要帐户和一个帐户来存储检索到的价格数据。一旦链上程序执行完成，它就从传入程序的帐户中读取价格数据。

首先，客户端使用 Anchor 建立与集群的连接，并设置一些必需的参数，如引入命令行参数和设置默认值:

```
const args = require('minimist')(process.argv.slice(2));

// Initialize Anchor and provider
const anchor = require("@project-serum/anchor");
const provider = anchor.Provider.env();
// Configure the cluster.
anchor.setProvider(provider);

const CHAINLINK_PROGRAM_ID = "HEvSKofvBgfaexv23kMabbYqxasxU3mQ4ibBMEmJWHny";
const DIVISOR = 100000000;

// Data feed account address
// Default is SOL / USD
const default_feed = "HgTtcbcmp5BeThax5AU8vg4VwK79qAvAKKFMs8txMLW6";
const CHAINLINK_FEED = args['feed'] || default_feed;

```

在此之后，定义客户端的主要功能。这是完成上述所有工作的函数。首先，它使用锚框架连接到我们部署的程序。然后，它生成一个新帐户，并调用部署程序中的“执行”函数，传入以下详细信息:

*   为存储价格数据而创建的账户
*   运行客户端的用户账户(支付交易费用)
*   指定价格馈送账户地址
*   devnet 上链接价格的程序 ID。这是一个不需要修改的静态值
*   索拉纳 [系统程序](https://docs.solana.com/developing/runtime-facilities/programs#system-program) 账号地址。同样，这个值是静态的

```
async function main() {
  // Read the generated IDL.
  const idl = JSON.parse(
    require("fs").readFileSync("./target/idl/chainlink_solana_demo.json", "utf8")
  );

  // Address of the deployed program.
  const programId = new anchor.web3.PublicKey(args['program']);

  // Generate the program client from IDL.
  const program = new anchor.Program(idl, programId);

  //create an account to store the price data
  const priceFeedAccount = anchor.web3.Keypair.generate();

  console.log('priceFeedAccount public key: ' + priceFeedAccount.publicKey);
  console.log('user public key: ' + provider.wallet.publicKey);

  // Execute the RPC.
  let tx = await program.rpc.execute({
    accounts: {
      decimal: priceFeedAccount.publicKey,
      user: provider.wallet.publicKey,
      chainlinkFeed: CHAINLINK_FEED,
      chainlinkProgram: CHAINLINK_PROGRAM_ID,
      systemProgram: anchor.web3.SystemProgram.programId
    },
    options: { commitment: "confirmed" },
    signers: [priceFeedAccount],
  });

```

然后，客户端等待得到一个确认的交易，然后将程序输出到控制台上。这将显示有关交易的信息，包括链上程序的打印输出。最后，程序从传入程序的 priceFeed 帐户中读取价格数据，然后将值输出到控制台。

```
console.log("Fetching transaction logs...");
  let t = await provider.connection.getConfirmedTransaction(tx, "confirmed");
  console.log(t.meta.logMessages);
  // #endregion main

  // Fetch the account details of the account containing the price data
  const latestPrice = await program.account.decimal.fetch(priceFeedAccount.publicKey);
  console.log('Price Is: ' + latestPrice.value / DIVISOR)

```

#### 运行客户端

第一步是设置锚点环境变量。锚框架需要这些来确定使用哪个提供者，以及使用哪个钱包来与部署的程序进行交互。在本例中，我们将值设置为默认的 devnet 提供者 URL，以及我们之前创建的 wallet:

```
export ANCHOR_PROVIDER_URL='https://api.devnet.solana.com'
export ANCHOR_WALLET='./id.json'

```

完成后，我们就可以运行 JavaScript 客户端了。确保使用–program 标志传递从前面步骤中获得的程序 ID，该标志链接到包含拥有该程序的帐户的 json 文件。我们还需要传入我们希望查询的链接提要地址。这可以从[chain link Solana Feeds 页面](https://docs.chain.link/docs/solana/data-feeds-solana/) 中获取，如果不指定值，该值将默认为 devnet SOL/USD feed 地址。在本例中，我们显式地指定了 SOL/USD 提要，以展示提要参数是如何工作的:

```
node client.js --program $(solana address -k ./target/deploy/chainlink_solana_demo-keypair.json) -–feed  HgTtcbcmp5BeThax5AU8vg4VwK79qAvAKKFMs8txMLW6

```

您应该看到显示客户端成功执行的输出，它应该显示来自指定价格提要的最新价格，存储在新帐户中:

![running-anchor-chainlink-client](img/d14abf992147f6dde2d949dd0facfebf.png)

<figcaption id="caption-attachment-3290" class="wp-caption-text">Executing the client</figcaption>



## 总结

Solana 为构建智能合同和分散应用提供了高速、低成本、可扩展的区块链。通过利用 Solana 智能合约和 Chainlink 价格馈送，开发人员可以利用 Chainlink 价格馈送提供的高质量数据和 Solana 区块链上的高速更新，创建快速、可扩展的 DeFi 应用程序。

要了解更多 Chainlink 技术教程，请查看 Chainlink 官方 YouTube 上的 [工程视频教程播放列表](https://www.youtube.com/playlist?list=PLVP9aGDn-X0SPHromvpiGvoNDpH7YErmf) ，并访问 Chainlink 文档，网址为[docs . chain . link](https://docs.chain.link/)。 讨论一个整合， [联系专家](https://chainlinkcommunity.typeform.com/to/OYQO67EF?page=announcement) 。