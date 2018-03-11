# Bitcoin

|Resources|
|---|
|[paper](https://bitcoin.org/bitcoin.pdf)|
|[bitcoin Stack exchange](https://bitcoin.stackexchange.com)|
|[blockexplorer](https://blockchain.info/)|
|[private testnet](https://github.com/freewil/bitcoin-testnet-box)|
|[bitcoind](https://en.bitcoin.it/wiki/Bitcoind)|
|[developer doc](https://bitcoin.org/en/developer-documentation)|

# Table of contents
1. [Objective](#Objective)
2. [Types of Blockchains](#Types)
3. [Glossary](#Glossary)
   1. [Bitcoin](#btc)
   2. [Block](#block)
   3. [Merkle Tree](#merkletree)
   4. [Script](#script)
   5. [Proof of Work](#pow)
   6. [Target](#target)
   7. [Wallet](#wallet)
   8. [P2P Network](#p2pnetwork)
4. [Mathematical Functions Used](#Mathematical-Functions-Used)
5. [Bitcoine Core vs Bitcoine Unlimited](#btc-btcu)
6. [Bitcoind](#bitcoind)
6. [References](#references)

<a name="Objective"></a>
## Objective : 
*visualizing bitcoin blockchain and discussing how exactly bitcoin uses blockchain*

<a name="Types"></a>
## Types of Blockchains:
There are basically three types of Block chains:
1. Public Blockchains
2. Permissioned Blockchains
3. Private Blockchains

The terms public, permissioned, and private refer to who has the ability to be a user of, or run a node on the Blockchain. Each type of Blockchain places a different level of importance on anonymity, immutability, efficiency, and transparency.

### Public Blockchain
On a public Blockchain anyone can be a user or run a node. Public Blockchains such as Bitcoin value anonymity, immutability, and transparency over efficiency.

### Permissioned Blockchain
Permissioned Blockchains are operated by known entities such as stakeholders of a given industry. They value immutability and efficiency over anonymity and transparency. The Financial industry would use such a Blockchain to reduce the time of international payments from days to seconds.

### Private Blockchain
Private Blockchains are operated by one entity. These Blockchains value efficiency over anonymity, immutability and transparency. Their use cases are limited.


<a name="Glossary"></a>
## Glossary : 

<a name="btc"></a>
### Bitcoin : 
Bitcoin is a digital currency (also called crypto-currency).

According to Wikipedia: 

>Bitcoin is a cryptocurrency and worldwide payment system. It is the first decentralized digital currency, as the system works without a >central bank or single administrator. The network is peer-to-peer and transactions take place between users directly, without an >intermediary. These transactions are verified by network nodes through the use of cryptography and recorded in a public distributed >ledger called a blockchain

<a name="block"></a>
### Block   
Blocks are files where transactions are permanently recorded. A block records some or all of the most recent Bitcoin transactions that have not yet entered any prior blocks. Thus a block is like a page of a ledger or record book. Each time a block is ‘completed’, it gives way to the next block in the blockchain. A block is thus a permanent store of records which, once written, cannot be altered or removed. 

#### Contents of a Block 
##### Block # : 
It is a number which behaves like a counter. Every new block mined is given a Block # which is one greater than its previous block. The Block # starts from 0.Also called depth of a block in the Bitcoin Blockchain.
Count of current number of blocks can be seen [here](https://blockexplorer.com/api/status?q=getBlockCount "Count of blocks").

##### Block Structure :
| Field               | Description                                  | Size                                    |
| --------------------|:--------------------------------------------:| ---------------------------------------:|
| Magic no	          | value always 0xD9B4BEF9                      |	4 bytes                                |
| Blocksize	          | number of bytes following up to end of block |	4 bytes                                |
| Blockheader         |	consists of 6 items                          |	80 bytes                               |
| Transaction counter |	positive integer VI = VarInt                 |	1 - 9 bytes                            |
| Transactions        |	the (non empty) list of transactions         |	many transactions                      |

##### Number of Transactions: 
The absolute limit is the size of the block, which is currently hard-coded at 1,000,000 bytes. Each transaction takes up a variable amount of space, but ~250 bytes is about right for a simple transaction.

However as soon as a block is mined it is not possible to extend the block by adding in more transactions, as the proof of work has to be redone, so broadcasting it immediately is the only sensible thing to do. So the number of transactions in a block is actually a function of the number of transactions being generated over a time period and the time taken to solve a given block.

##### Height:
The number of blocks preceding a particular block on a block chain. For example, the genesis block has a height of zero because zero block preceded it.

##### Block Reward:
Every block also contains a record of which Bitcoin addresses or scripts are entitled to receive the reward. This record is known as a generation transaction, or a coinbase transaction, and is always the first transaction appearing in every block. The number of Bitcoins generated per block starts at 50 and is halved every 210,000 blocks.
Bitcoin transactions are broadcast to the network by the sender, and all peers trying to solve blocks collect the transaction records and add them to the block they are working to solve. Miners get incentive to include transactions in their blocks because of attached transaction fees.

##### Timestamp:
A node adds a timestamp as soon as it detects a new block in the network. So, it can be said that the timestamp is a rough indicator of when the block was formed by the miner.
It is possible that the timestamp of a newer block is older that the timestamp of the older block.

From bitcoin.it/wiki/Block_timestamp:

>A timestamp is accepted as valid if it is greater than the median timestamp of previous 11 blocks, and less than the network-adjusted >time + 2 hours.

##### Mined by:
Name of the miner or the mining pool which mined the block. Blocks do not need to contain any identifying factors. The miner can choose to provide a script in the coinbase of a new block that can be used to identify the source of the block, however they are not required to do so. Hence, some blocks have empty 'Mined By' field.

##### Merkle Root:
It is the hash of the root node of the particular block's Merkle Tree. For more information see [Merkle Tree](#merkletree).

##### Previous Block:
The block preceeding the current block is known as the previous block. Each block is guaranteed to come after the previous block chronologically because the previous block's hash would otherwise not be known. Because a block can only reference one previous block, it is impossible for two forked chains to merge.

##### Difficulty:
The difficulty of the mathematical problem is automatically adjusted by the network, such that it targets a goal of solving an average of 6 blocks per hour. Every 2016 blocks (solved in about two weeks), all Bitcoin clients compare the actual number created with this goal and modify the target by the percentage that it varied. The network comes to a consensus and automatically increases (or decreases) the difficulty of generating blocks.

##### Bits:

##### Size(bytes):
There was no limit on the size of Bitcoin originally but a limit of 1 MB was set later because of problem of Denial of Service Attack.
Denial of Service attack is basically huge blocks of transactions which are not possible to process with current technology.
The Bitcoin community is divided on this issue as some of them say that the block size must be increased in order to make Bitcoin competitive with other currency mediums such as Paypal while others argue that it must be kept constant so that there is less difficulty in mining the block.

![alt text](https://raw.githubusercontent.com/varadhbhatnagar/Blockchain-Beginning/bitcoinCaseStudy/caseStudies/data/blockdata.JPG)

##### Version:
The version number is a parameter to help in updating how blocks are treated by the network. As newer rules and regulations concerning blocks come into play, the block version gets updated.

![Version-History](data/versiontrend.PNG)

##### Nonce:
The "nonce" in a bitcoin block is a 32-bit (4-byte) field whose value is set so that the hash of the block will contain a run of leading zeros. The rest of the fields may not be changed, as they have a defined meaning .Any change to the block data (such as the nonce) will make the block hash completely different. Since it is infeasible to predict which combination of bits will result in the right hash, many different nonce values are tried, and the hash is recomputed for each value until a hash containing the required number of zero bits is found just like Brute Force technique.

##### Transactions:
A transaction is a transfer of Bitcoin value that is broadcast to the network and collected into blocks. Transactions are not encrypted, so it is possible to browse and view every transaction ever collected into a block. Once transactions are buried under enough confirmations they can be considered irreversible.

![Txn](data/txnformat.PNG)

This is a typical transaction having two inputs and two outputs. The two inputs on the left side are the unspent bitcoins of the given address which are being spent in this transaction. These two inputs have addresses and signatures associated with them which help in authenticating them.

The two output addresses on the right are ones to which the bitcoins from the input are sent to. Each of these addresses have a public key which is used to authenicate them. If case of change being generated in a transaction, the change amount is sent back to the sender which can be seen as there is a common address on input and output side of the transaction.

Note that BTC(Input1) + BTC(Input2) + Txn Fee = BTC(Output1) + BTC(Output 2).

#### Genesis Block   
A genesis block is the first block of a block chain. Modern versions of Bitcoin number it as block 0, though very early versions counted it as block 1. The genesis block is almost always hardcoded into the software of the applications that utilize its block chain. It is a special case in that it does not reference a previous block, and for Bitcoin and almost all of its derivatives, it produces an unspendable subsidy.

![alt text](https://raw.githubusercontent.com/varadhbhatnagar/Blockchain-Beginning/bitcoinCaseStudy/caseStudies/data/block.JPG)


<a name="merkletree"></a>
### Merkle Tree    
Merkle Tree is a tree in which every leaf node contains the hash of a data block and every non leaf node contains
a hash value which has been formed by combining the hashes of its children nodes.Typically, Merkle trees have a                 branching factor of 2, meaning that each node has up to 2 children.The root of the tree is called Merkle Root.
The leaf nodes are transactions within a block.
              
#### Need
In various distributed and peer-to-peer systems, data verification is very important. This is because the same                 data exists in multiple locations. So, if a piece of data is changed in one location, it's important that data is               changed everywhere. Data verification is used to make sure data is the same everywhere.

However, it is time consuming and computationally expensive to check the entirety of each file whenever a system               wants to verify data. So, this why Merkle trees are used. Basically, we want to limit the amount of data being                 sent over a network (like the Internet) as much as possible. So, instead of sending an entire file over the                     network, we just send a hash of the file to see if it matches.
              
#### Utility
The utility of Merkle trees are as follows:

1. Merkle Trees are tamper proof. Even if a single bit is changed in any of the leaf nodes or any non
   leaf node, the hash of its parent changes significantly proving that tampering had taken place.

2. If we want to validate a leaf node, we only need to consider one branch of the Merkle Root, the                                other can be ignored as it is not of any use here.
              
#### Use 
Currently, their main uses are in peer-to-peer networks such as Tor, Bitcoin, and Git.

#### PseudoCode
```python
d1 = dhash(a)
d2 = dhash(b)
d3 = dhash(c)
d4 = dhash(c)            // a, b, c are 3. that's an odd number, so we take the c twice

d5 = dhash(d1 concat d2)
d6 = dhash(d3 concat d4)

d7 = dhash(d5 concat d6)
```
where
```python
dhash(a) = sha256(sha256(a))
```
Note: markle tress generally uses sha256 for hashes and also RIPEMD-160 for smaller desired address like bitcoin address.

#### Complexity
![Complexity Image](data/complexity.png)

![Merkle Tree Image](data/mroot.png)

![Block0 Image](data/block0.png)

![Block1 Image](data/block1.png)

<a name="pow"></a>

### Script
A script is essentially a list of instructions recorded with each transaction that describe how the next person wanting to spend the Bitcoins being transferred can gain access to them. The script for a typical Bitcoin transfer to destination Bitcoin address D simply encumbers future spending of the bitcoins with two things: the spender must provide

1. a public key that, when hashed, yields destination address D embedded in the script, and 
2. a signature to prove ownership of the private key corresponding to the public key just provided.

Scripting provides the flexibility to change the parameters of what's needed to spend transferred Bitcoins. For example, the scripting system could be used to require two private keys, or a combination of several keys, or even no keys at all.

This is the most commonly used transaction output script. It's used to pay to a bitcoin address (a bitcoin address is a public key hash encoded in base58check)
```javascript
// create a new p2pkh paying to a specific address
var address = Address.fromString('1NaTVwXDDUJaXDQajoa9MqHhz4uTxtgK14');
var script = Script.buildPublicKeyHashOut(address);
assert(script.toString() === 'OP_DUP OP_HASH160 20 0xecae7d092947b7ee4998e254aa48900d26d2ce1d OP_EQUALVERIFY OP_CHECKSIG');
```

### Proof of Work:   
A proof of work is a piece of data which is difficult (costly, time-consuming) to produce but easy for others to verify and which satisfies certain requirements. Producing a proof of work can be a random process with low probability so that a lot of trial and error is required on average before a valid proof of work is generated.

Hashcash proofs of work are used in Bitcoin for block generation. In order for a block to be accepted by network participants, miners must complete a proof of work which covers all of the data in the block. The difficulty of this work is adjusted so as to limit the rate at which new blocks can be generated by the network to one every 10 minutes. Due to the very low probability of successful generation, this makes it unpredictable which worker computer in the network will be able to generate the next block.

<a name="target"></a>
### Target:    
The target is a 256-bit number that all Bitcoin clients share. The SHA-256 hash of a block's header must be lower than or equal to the current target for the block to be accepted by the network. The lower the target, the more difficult it is to generate a block.

For reasons of stability and low latency in transactions, the network tries to produce one block every 10 minutes. Every 2016 blocks (which should take two weeks if this goal is kept perfectly), every Bitcoin client compares the actual time it took to generate these blocks with the two week goal and modifies the target by the percentage difference. This makes the proof-of-work problem more or less difficult. A single retarget never changes the target by more than a factor of 4 either way to prevent large changes in difficulty.

### Wallet
A Bitcoin wallet is a collection of private keys but may also refer to client software used to manage those keys and to make transactions on the Bitcoin network.
According to investopedia:
> A Bitcoin wallet is a software program where Bitcoins are stored. To be technically accurate, Bitcoins are not stored anywhere; there is a private key (secret number) for every Bitcoin address that is saved in the Bitcoin wallet of the person who owns the balance. Bitcoin wallets facilitate sending and receiving Bitcoins and gives ownership of the Bitcoin balance to the user.  The Bitcoin wallet comes in many forms; desktop, mobile, web and hardware are the four main types of wallets.

You can think of a wallet as your personal interface to the Bitcoin network, similar to how your online bank account is an interface to the regular monetary system.
currently wallets is of 4 types 
1. Mobile wallets (easy to make quick payments and portable)
2. Web wallets (easy to make quick payments)
3. Desktop Wallets (offline software wallet to add security)
4. Hardware wallets (offline wallet to add security)

#### Desktop Wallets
Desktop wallets are installed on a desktop computer and provide the user with complete control over the wallet. Desktop wallets enable the user to create a Bitcoin address for sending and receiving the Bitcoins. They also allow the user to store a private key. A few known desktop wallets are Bitcoin Core, MultiBit, Armory, Hive OS X, Electrum, etc.

#### Mobile Wallets
Mobile wallets overcome the handicap of desktop wallets, as the latter are fixed in one place. Once you run the app on your smartphone, the wallet can carry out the same functions as a desktop wallet, and help you pay directly from your mobile from anywhere. Thus a mobile wallet facilitates in making payments in physical stores by using "touch-to-pay" via NFC scanning a QR code. Bitcoin Wallet, Hive Android and Mycelium Bitcoin Wallet are few of the mobile wallets. 

#### Web Wallets
As for web wallets, they allow you to use Bitcoins from anywhere, on any browser or mobile. The selection of your web wallet must be done carefully since it stores your private keys online. Coinbase and Blockchain are popular web wallet providers.

#### Hardware Wallets
Hardware wallets are most secured way to save your private keys, These devices can hold private keys electronically and facilitate payments after verifications.
hardware wallets are still limited in numbers, some of them are:-

 * [TREZOR](http://amzn.to/2nTyYwk)
 
 * [Ledger Nano S](http://amzn.to/2FUlkAn)
 
 * [keepkey](http://amzn.to/2FYnMpC)

<a name="p2pnetwork"></a>
### P2P Network
The Bitcoin network protocol allows full nodes (peers) to collaboratively maintain a peer-to-peer network for block and transaction exchange. Full nodes download and verify every block and transaction prior to relaying them to other nodes. Archival nodes are full nodes which store the entire blockchain and can serve historical blocks to other nodes. Pruned nodes are full nodes which do not store the entire blockchain.

Before a full node can validate unconfirmed transactions and recently-mined blocks, it must download and validate all blocks from block 1 (the block after the hardcoded genesis block) to the current tip of the best block chain. This is the Initial Block Download (IBD) or initial sync.

Bitcoin Core uses the IBD method any time the last block on its local best block chain has a block header time more than 24 hours in the past. Bitcoin Core 0.10.0 will also perform IBD if its local best block chain is more than 144 blocks lower than its local best header chain (that is, the local block chain is more than about 24 hours in the past).

When a miner discovers a new block, it broadcasts the new block to its peers using one of the following methods:
1. Unsolicited Block Push
2. Standard Block Relay
3. Direct Headers Announcement

read more about Block Broadcasting [here](https://bitcoin.org/en/developer-guide#block-broadcasting "Blocks Broadcasting")



<a name="Mathematical-Functions-Used"></a>
## Mathematical Functions Used:

[Elliptic Curve Digital Signal Algorithm](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm)

[Mathematical Trap Door](https://en.wikipedia.org/wiki/Trapdoor_function)

<a name="btc-btcu"></a>
## Bitcoin Core vs Bitcoin Unlimited
Hard fork - It is a change in the main rules that govern Bitcoin. Anybody who does not upgrade to the new version will be left behind.It is not Backward Compatible.

Soft fork - Added rules to Bitcoin which do not change the current rules, allowing people to upgrade to a new version while the old version still works.It is Backward Compatible.

### Bitcoin Core -
It is the current implementation of Bitcoin.A solution of to scale up from Bitcoin Core is first to add Segregated Witness which fixes transaction malleability (which is a bug in Bitcoin). This would double the number of transactions which are done in each block.
This also opens up the possibility of lightning network i.e. massive scaling on top of Bitcoin to the level of Mastercard and Visa.
Segregated witness is done using soft work i.e. some poeple would not be able to take advantage of the added features that are available.


### BTC Unlimited- 
This implmentation of Bitcoin would change the Block size limit so that miners can decide how large blocks they would like to mine.
The number of transactions would be dynamic and would (hopefully) grow at a reasonable rate to not overload limits of current computing power.
This would be done through hard fork.i.e everybody would have to upgrade to Bitcoin Unlimited.

### Concerns:
#### Bitcoin Core:
1. Code behind segregated witness is too complex and not elegant.
2. Bitcoin core is too centralized and these type of people are trying to take control. (Company called block stream has engrained into Bitcoin core).

3.Scaling is slow and Transaction Fee is rising because there is limited space for transactions. Thus, Bitcoin Core is losing users and becoming becoming less usable.
4. There has been some censorship of ideas of alternative scaling solutions.

#### Bitcoin Unlimted:
1. Code behind this is unsafe, two recent bugs have had bad effects.
2. Just raising Block size is temporary solution and still it is not quick enough to scale to Visa or Master card network.
3. Miners advocating BTC unlimited because lightning networks would cut down fee of transaction.
4. Closed source bug patch have been released and if code is not available Open Source, people would stop trusting Bitcoin.
5. Bitcoin unlimited would attack BTC Core chain and two currencies would be there simultaneously.

### Bitcoind
Bitcoin wiki states that
>bitcoind is a program that implements the Bitcoin protocol for remote procedure call (RPC) use. It is also the second Bitcoin client in the network's history. It is available under the MIT license in 32-bit and 64-bit versions for Windows, GNU/Linux-based OSes, and Mac OS X.

Bitcoind is a headless daemon, and also bundles a testing tool for the same daemon. It provides a JSON-RPC interface, allowing it to be controlled locally or remotely which makes it useful for integration with other software or in larger payment systems. Various commands are made available by the API.

To use locally, first start the program in daemon mode:

`bitcoind -daemon`

Then you can execute API commands, e.g.:

`bitcoin-cli getinfo`
`bitcoin-cli listtransactions`

To stop the bitcoin daemon, execute:

`bitcoin-cli stop`

<a name="references"></a>
## References    

### Video References:
https://www.youtube.com/watch?v=VkWiTvPnTcY

https://www.youtube.com/watch?v=gUwXCt1qkBU

https://www.youtube.com/watch?v=Lx9zgZCMqXE

https://www.youtube.com/watch?v=RmGEuriu1u8

### Documents: 
https://brilliant.org/wiki/merkle-tree/

Block (Bitcoin Block) https://www.investopedia.com/terms/b/block-bitcoin-block.asp

https://bitcoin.org/en/developer-guide

https://coindesk.com

https://tradeblock.com

https://en.bitcoin.it/wiki

https://medium.com/@BrettNoyes/public-permissioned-and-private-blockchains-3c32965e33c9

https://www.cryptocompare.com/coins/guides/what-is-the-block-size-limit/



