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

### Main Functionality

The main functionality is the transfer of custody.

