# Bitcoin Transactions

Docs: [Bitcoin Sv](https://wiki.bitcoinsv.io/index.php/Bitcoin_Transactions)

## Consistency

1. **Version Number**: This field indicates the version of the transaction format, used in the interpretation of the transaction.
2. **Locktime**: The time at which the transaction can be considered valid; the transaction cannot be included in a block before this time.
3. **Inputs**: Reference previous transactions (outputs) from which the bitcoins are being sent.
4. **Outputs**: The destinations for the bitcoins and their respective amounts.

### Observations

1. Inputs must include a reference to an output from a previous transaction, thus preventing the double-spending problem.
2. Outputs include a value and an address to which the bitcoins are being transferred. It is still possible to create outputs that are not linked to a specific address—they become lost in the blockchain; additionally, if an output does not have an associated public key or digital signature, it may be considered 'free', allowing anyone to use it, as there is no control over the ownership of the bitcoins.

## Main Functionality

Transfer of custody.

## Ways to Create a Transaction

1. **Payment Channel**
   - **Payment Channel**: A solution that allows parties to make off-chain transactions (lower fees and greater efficiency).
   - **nLocktime and nSequence**: These are fields in the transaction that control when and how the transactions can be spent.
   - **Example**: Imagine Alice and Bob are at a park and decide to play a game of dice. They agree to play 10 rounds and create a payment channel with 10 BTC. After each round, they simply note who won, without making transactions. At the end, Alice won 6 times and Bob 4. They make a single transaction to the network, where Alice receives 6 BTC and Bob receives 4 BTC, saving on fees and time.

2. **Bitcoin Network**
   - Direct transmission from a node to a block


## Transactions are not encrypted
It is possible to browse and view every transaction ever collected into a block.

## Validation of Transactions:
1. **Transmission of the Transaction**
2. **Basic Verification:**
   1. If the inputs refer to valid and unspent transactions (UTXOs).
   2. If the transaction is well-formed.
   3. If the digital signatures correspond to the public keys.
3. **Propagation in the Network**
4. **Confirmation by the Majority of Block-Creating Nodes:**
   1. They place the transaction in a "pool of pending transactions."
   2. Mining process for inclusion of transactions in the block; the order is based on miners' consensus.
5. **Inclusion in a Block:** 
   If the transaction is in a block, then it is considered valid by the network.

## Formation of a TXID - Transaction ID:
1. **Serialization:** 
   1. The exact format in which the transaction needs to be for the BVM to understand and process it.
   2. Standardized sequence of bytes: version, inputs, outputs, locktime.
2. **Double SHA-256 Hash:**
   1. The first hash generates a 32-byte or 64-character hexadecimal result.

## Behavior of Outputs and Inputs in a Transaction:
1. **Outputs:**
   1. _ScriptPubKeys_ or puzzle script or locking script: contain logic (script) that defines how the bitcoins can be spent.
2. **Inputs:** 
   1. _ScriptSig_ or unlocking script: valid solution for the ScriptPubKey of some output.
3. **Relation:**
   1. ScriptSig must satisfy the "condition" defined by the ScriptPubKey for the custody transfer of bitcoin to occur.
   2. Most common is a ScriptPubKey that requires a public key and a digital signature to unlock the funds.

## Serialized Bitcoin Transaction

### Elements

| Field        | Description                                                                                 | Size               |
|--------------|---------------------------------------------------------------------------------------------|--------------------|
| **Version no**   | Indicates the version of the transaction format.                              | 4 bytes            |
| **In-counter**   | A positive integer that represents the number of inputs, encoded as a VarInt (variable length integer). | 1 - 9 bytes        |
| **List of inputs** | A list of input structures, each with variable length based on the number of inputs (`<in-counter>`).  | Variable           |
| **Out-counter**  | A positive integer that represents the number of outputs, also encoded as a VarInt.       | 1 - 9 bytes        |
| **List of outputs** | A list of output structures, each with variable length based on the number of outputs (`<out-counter>`). | Variable           |
| **nLocktime** | The block height* or timestamp when the transaction is final. | 4 bytes            |

_*: represents the block's position in the blockchain. Ex: genesis block has block height of 0._

### Format of a Transaction Input (TXIN)

| Field                     | Description                                                                         | Size               |
|----------------------------|-------------------------------------------------------------------------------------|--------------------|
| **Previous Transaction hash** | The TXID* of the transaction where the referenced output was created. | 32 bytes           |
| **Previous Txout-index**      | Index of the output in the previous transaction (a non-negative integer).            | 4 bytes            |
| **scriptSig length**        | Length of the scriptSig**, encoded as a VarInt (variable length integer). | 1 - 9 bytes        |
| **scriptSig**   | The scriptSig that provides a valid solution to the previous output's locking script. | `<in-scriptSig length>` bytes |
| **Input Finalizer** |      The input is final when nSequence = 0xFFFFFFFF. | 4 bytes            |

_TXID*: acronym Transaction ID_   
_scriptSig**: AKA input script_   
_Input Finalizer***: AKA Sequence_no_   

### Format of a Transaction Output (TXOUT)

| Field                    | Description                                                                           | Size                |
|---------------------------|---------------------------------------------------------------------------------------|---------------------|
| **value**                 | Non-negative integer representing the number of satoshis to be transferred.            | 8 bytes             |
| **scriptPubKey length**    | Length of the scriptPubKey*, encoded as a VarInt (variable length integer). | 1 - 9 bytes         |
| **scriptPubKey** | Defines the conditions under which the output can be spent. | `<scriptPubKey length>` bytes |

_scriptPubKey*: AKA Txout-script_  

**About the scriptPubKey part:**
1. The puzzle is created, which is usually a digital signature. It doesn't necessarily have to be a digital signature, it could be something like a simple addition operation or even left open(mostly for educational purposes).   
2. At this point, it is also possible to include the recipient's address.

**About the changes:**   
Whenever an input is larger than the value to be sent, it is important to provide a change output so that the remaining value is properly allocated. 

For example, if the user has an input of 0.05 BTC and wants to send only 0.02 BTC to someone, the transaction will have two outputs:

- One output of 0.02 BTC to the recipient.
- One output of 0.03 BTC (the change) back to the user.

### Notes:
1. **Numbers are expressed in Hexadecimal**.
2. **TXID is expressed in Little Endian**.
3. **Transaction values are expressed in Satoshis** (HEX, as per item 1.).
4. **Miner fee**: The difference between the total of the outputs and the total of the inputs, included indirectly in the transaction.
