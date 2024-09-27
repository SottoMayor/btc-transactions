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

