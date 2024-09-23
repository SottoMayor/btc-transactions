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
