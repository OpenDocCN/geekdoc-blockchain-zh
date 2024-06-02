© 作者（们），独家许可给 APress Media，LLC，Springer Nature 2022J. T. George 介绍区块链应用程序[`doi.org/10.1007/978-1-4842-7480-4_8`](https://doi.org/10.1007/978-1-4842-7480-4_8)

# 8. 区块链项目的共识算法

约瑟夫·塔钦·乔治^(1  )(1) 意大利罗马

这个项目是用 Python 编写的基本区块链。它是一组区块，这些区块以不可修改的方式链接在一起，随着更多的区块加入到区块链中，存储在其中的信息变得越来越难以修改。

PoW（工作证明）算法用于挖掘这个区块链中的每个区块。它的目的是找到满足特定条件的所有数据保存在区块中的哈希。为此，每个区块都有一个名为 nonce 的可变数据，必须修改直到发现所需的哈希。

例如，比特币中所需的哈希需要前 *X* 位为零。X 的数量决定了挖矿的难度（X 越大，难度越大）。在这个区块链中，X 是区块链的一个属性，可以在其构造函数中设置。然而，这取决于支持比特币和其他大多数货币网络的节点的挖矿能力。

## 8.1 启动项目

该项目有一个依赖项，称为 hashlib，用于保护哈希和消息摘要 import hashlib。

要运行该项目，打开终端并键入以下命令：python3 project1.py

使用 Create Transaction 方法 生成交易。所需输入包括发送地址、接收地址和 FDCs（物联网中的联合数据协作）的数量。创建交易后，使用 Mine Pending Transactions 函数将其添加到区块链中。作为参数，此方法需要区块的矿工地址，即未来将获得奖励的地址。您还可以使用 Show Address Balance 方法，并将要验证的地址名称作为参数，以检查每个地址的余额。

## 8.2 Python 代码

列出 8-1 显示了 TransactionProject.py Python 文件。python 文件 TransactionProject.py 将帮助我们执行以下任务：

1.  1.

    在区块链中创建交易

1.  2.

    交易的挖掘

1.  3.

    验证交易

1.  4.

    在区块链中创建区块

*import datetime**import hashlib**from pprint import pprint**class Transaction(object):*      *"""Transaction 类*      *"""*      *def __init__(self, fromAddress, toAddress, amount):*            *self.fromAddress = fromAddress*            *self.toAddress = toAddress*            *self.amount = amount**class Block(object):*      *"""Block 类*      *"""*      *def __init__(self, timestamp, transactions, previousHash=""):*            *self.timestamp = timestamp*            *self.transactions = transactions*            *self.previousHash = previousHash*            *self.nonce = 0*            *self.hash = self.calculateHash()*      *def calculateHash(self):*            *info = str(self.timestamp) + str(self.transactions) + str(self.previousHash) + str(self.nonce)*            *return hashlib.sha256(info.encode('utf-8')).hexdigest()*      *# 工作量证明算法*      *def mineBlock(self, difficulty):*            *self.hash = self.calculateHash()*            *while(self.hash[:difficulty] != "0"*difficulty):*                  *self.nonce += 1*                  *self.hash = self.calculateHash()**class BlockChain(object):*      *"""Blockchain 类*      *"""*      *def __init__(self):*            *self.chain = [self.createGenesisBlock()]*            *self.difficulty = 4*            *self.pendingTransactions = []*            *self.miningReward = 100*      *def createGenesisBlock(self):*            *return* *Block**("20/03/2018", [], "0")*      *def getLatestBlock(self):*            *return self.chain[-1]*      *def minePendingTransactions(self, miningRewardAddress):*            *newBlock =* *Block**(datetime.datetime.now(), self.pendingTransactions)*            *newBlock.previousHash = self.getLatestBlock().hash*            *# 在这里可以检查交易是否有效*            *print("挖矿中...")*            *newBlock.mineBlock(self.difficulty)*            *print("挖矿完成，区块哈希值:", newBlock.hash)*            *print("区块成功挖矿完成。")*            *self.chain.append(newBlock)*            *self.pendingTransactions = [Transaction(None, miningRewardAddress, self.miningReward)]*      *def createTransaction(self, transaction):*            *self.pendingTransactions.append(transaction)*      *def getBalanceOfAddress(self, address):*            *balance = 0*            *for block in self.chain:*                  *for transaction in block.transactions:*                        *if transaction.fromAddress == address:*                              *balance -= transaction.amount*                        *if transaction.toAddress == address:*                              *balance += transaction.amount*            *return balance*      *def isBlockChainValid(self):*            *for previousBlock, block in zip(self.chain, self.chain[1:]):*                  *if block.hash != block.calculateHash():*                        *return False*                  *if block.previousHash != previousBlock.hash:*                        *return False*            *return True*      *def showBlockChain(self):*            *print("区块链：fedecoin\n")*            *for block in self.chain:*                  *print("区块")*                  *print("时间戳:", block.timestamp)*                  *pprint("交易:", block.transactions)*                  *print("上一个区块哈希值:", block.previousHash)*                  *print("区块哈希值:", block.hash, "\n")*      *def showAddressBalance(self, address):*            *print(address, "的余额:", self.getBalanceOfAddress(address))**fedecoin = BlockChain()**fedecoin.createTransaction(Transaction("address1", "address2", 100))**fedecoin.createTransaction(Transaction("address2", "address1", 50))**fedecoin.minePendingTransactions("fede_address")**fedecoin.createTransaction(Transaction("address1", "address3", 100))**fedecoin.createTransaction(Transaction("address2", "address1", 50))**fedecoin.minePendingTransactions("fede_address")**fedecoin.showAddressBalance("fede_address")**print("fedecoin 是否有效？", fedecoin.isBlockChainValid())**fedecoin.chain[1].transactions = Transaction("address1", "address2", 1000)**print("fedecoin 是否有效？", fedecoin.isBlockChainValid())**fedecoin.chain[1].calculateHash()**print("fedecoin 是否有效？", fedecoin.isBlockChainValid())*Listing 8-1

TransactionProject.py

## 8.3 示例 2：在 Python 中使用 Flask

我们利用 Python Flask 框架创建了这个区块链应用程序。以下是此应用程序的要求。*Python 3.0+**Flask 和 requests**用于安装**pip install Flask == 0.122 requests==2.18.4*以下是步骤：

1.  1.

    实施一个基本的工作证明。

1.  2.

    为区块链创建 API 接口。

1.  3.

    构建一个区块链矿工。

1.  4.

    使用区块链进行交互。

### 8.3.1 步骤 1：创建一个简单的工作证明

PoW（工作证明）的目标是提供一个解决问题的数字。必须难以追踪到这个数字，但是网络上的任何其他人都应该能够验证它。由于这个数字由加密签名组成，在其他地方提供错误的情况下，将被拒绝访问。 PoW 方法允许您发送资金而无需信任任何人或任何机构，因为区块链只关心加密签名。这是 PoW 的基础。

比特币基于 PoW。8-2 列举了一个示例。*from hashlib import sha256**x = 10**y = 0  # 我们还不知道 y 应该是多少...**while sha256(f'{x*y}'.encode()).hexdigest()[-1] != "0":*    *y += 1**printf('The solution is y = {y}')* *@staticmethod*    *def hash(block: Dict[str, Any]) -> str:*        *"""*        *创建一个区块的 SHA-256 哈希值*        *:param block: 区块*        *"""*        *# 我们必须确保字典是有序的，否则哈希值会不一致*        *block_string = json.dumps(block, sort_keys=True).encode()*        *return hashlib.sha256(block_string).hexdigest()*            *def proof_of_work(self, last_proof: int) -> int:*        *"""*        *简单的工作量证明算法：*         *- 找到一个数字 0'，使得 hash(00') 包含 4 个前导零，其中 0 是前一个 0'*         *- 0 是上一个证明，0' 是新的证明*        *"""*        *proof = 0*        *while self.valid_proof(last_proof, proof) is False:*            *proof += 1*        *return proof*    *@staticmethod*    *def valid_proof(last_proof: int, proof: int) -> bool:*        *"""*        *验证证明*        *:param last_proof: 上一个证明*        *:param proof: 当前证明*        *:return: 如果正确返回 True，否则返回 False*        *"""*        *guess = f'{last_proof}{proof}'.encode()*        *guess_hash = hashlib.sha256(guess).hexdigest()*        *return guess_hash[:4] == "0000"*列表 8-2

ProofOfWork.py

### 8.3.2 第 2 步：为区块链创建 API 端点

将 8-3 中所示的代码放在 Python 文件的末尾。然后你的文件将成为一个 API 端点，由于这段代码。这将使您能够使用 Postman 在您的区块链中传输和接收请求。*class Blockchain(object):**# 实例化我们的节点**app = Flask(__name__)**# 为本节点生成全局唯一地址**node_identifier = str(uuid4()).replace('-', '')**# 实例化区块链**blockchain = Blockchain()**@app.route('/mine', methods=['**GET**'])**def mine():*    *return "我们将挖掘一个新的区块"*@app.route('/transactions/new', methods=['POST'])**def new_transaction():*    *return "我们将添加一个新的交易"*@app.route('/chain', methods=['**GET**'])**def full_chain():*    *response = {*        *'chain': blockchain.chain,*        *'length': len(blockchain.chain),*    *}*    *return jsonify(response), 200**if __name__ == '__main__':*    *app.run(host='0.0.0.0', port=5000)**@app.route('/transactions/new', methods=['POST'])**def new_transaction():*    *values = request.get_json()*    *# 检查 POST 数据中是否有必需字段*    *required = ['sender', 'recipient', 'amount']*    *if not all(k in values for k in required):*        *return '缺少值', 400*    *# 创建新的交易*    *index = blockchain.new_transaction(values['sender'], values['recipient'], values['amount'])*    *response = {'message': f'交易将被添加到区块 {index}'}*    *return jsonify(response), 201*Listing 8-3

Apiendpoint.py

### 8.3.3 第 3 步：创建区块链矿工

列出的代码将为您的服务器建立一个矿工，该矿工将挖掘交易并将其添加到区块链块中。 使用此代码与您的 IDE（Eclipse 或 PyCharm）帮助。*@app.route('/mine', methods=['**GET**'])**def mine():*    *last_block = blockchain.last_block*    *last_proof = last_block['proof']*    *proof = blockchain.proof_of_work(last_proof)*    *blockchain.new_transaction(*        *sender="0",*        *recipient=node_identifier,*        *amount=1,*    *)*    *block = blockchain.new_block(proof=proof, previous_hash=0)*    *response = {*        *'message': "New Block Forged",*        *'index': block['index'],*        *'transactions': block['transactions'],*        *'proof': block['proof'],*    *}*    *return jsonify(response), 200*Listing 8-4

Miner.py

### 8.3.4 步骤 4：运行您的区块链项目

确保服务器正常运行，使用以下 IP 和端口地址：![../images/520777_1_En_8_Chapter/520777_1_En_8_Figa_HTML.jpg](img/520777_1_En_8_Figa_HTML.jpg)

（要退出，请按 Ctrl+C。）现在启动 Postman 并查找屏幕顶部的搜索栏。确保 GET 按钮在其左侧被选中。

然后将此地址输入地址栏：![../images/520777_1_En_8_Chapter/520777_1_En_8_Figb_HTML.jpg](img/520777_1_En_8_Figb_HTML.jpg)

## 8.4 复习问题

1.  1.

    “只有在 51% 的攻击成功时才会产生孤立块。” 这个说法正确还是不正确？

1.  2.区块链中的账本是用来做什么的？

    1.  a.

        用于标识所有者。

    1.  b.

        用于标识所拥有的对象。

    1.  c.

        用于标识所有者和对象之间的映射。

    1.  d.

        用于标识所有者的名称。

1.  3.以下哪种方法是保留比特币的最常见方法？

    1.  a.

        The pocket

    1.  b.

        The wallet

    1.  c.

        The box

    1.  d.

        The stack

1.  4.区块链块的结构是什么？

    1.  a.

        交易数据

    1.  b.

        Hash point

    1.  c.

        时间戳

    1.  d.

        所有这些

1.  5.

    “在比特币的情况下，经过 10 分钟，最新交易将被创建成一个新的区块。”这个说法正确还是不正确？

## 8.5 复习答案

1.  1.

    答案：不正确，这仅限于区块链。

1.  2.

    答案：C，所有者和对象之间的映射。

1.  3.

    答案：B，钱包。

1.  4.

    答案：D，所有这些。

1.  5.

    答案：正确。

## 8.6 总结

本章提供了两个例子，说明了共识算法。这些例子是用 Python 语言提供的。这些例子还有助于说明区块链的 PoW 系统。借助这些例子，您可以根据自己的需求构建应用程序。

当您思考区块链技术时，您需要了解分布式系统管理，因为区块链技术广泛应用于分布式系统中。本书的主要目的是在分布式系统中实现区块链。下一章将介绍分布式系统中的时间管理。
