# Overview

Until Quorum 2.7.0 any node in Quorum network can alter the state of a contract deployed in the network even though it never had the contract byte code. Privacy enhancement feature is to prevent such 'non-party' interaction. This is done by the introduction of `ACOTH` which is short for "Affected Contract's Original Transaction's encrypted payload Hash". The `ACOTH` will be the proof going forward that the node is party to the transaction that created that contract and a non-party node will never have the `ACOTH` preventing it to alter the state. There are two flavours of privacy enhancement implemention ie., a) Counter party protection  and b) Private state validation.

## Counter Party Protection (PP)

This implementation doesn't allow non-party interaction on a private contract but allows state deviation i.e., it will allow nodes to maintain different state through private transaction to 'self' or 'subset of nodes'. 

## Private State Validation (PSV)

This implementation further prevents nodes from state deviation by failing private transactions to 'self' or 'subset of nodes' by sharing the list of recipients among all nodes which is validated against all subsequent transactions (default mode only sending node knows the list of recipients). 

## Key Enhancements

### Privacy Flag

A new additional parameter `PrivacyFlag` in all Quorum `send` API methods , being passed from the client to enable new privacy enhancements. This flag is an unsigned integer with the following values: 1 for PP transaction and 3 for PSV transaction. If the flag is missing or zero, the transaction is assumed to be a 'non-privacy enhanced' standard transaction. 

### Privacy Metadata and Privacy Metadata Trie

Privacy Metadata is a new structure introduced in Quorum. It is saved in the quorum DB in the privacy metadata trie (which is linked to the private state - via root hash mappings). Privacy Metadata has the ACOTH and privacyFlag.

Privacy Metadata Trie is a parallel trie that stores the privacy metadata (and whatever extra data we may need) for the private contracts and is linked to the private state by root hash mappings. The records in the trie would be keyed by the contract account address (exactly the same as the contract accounts trie).

Each contract(account) that is created as 'PP' or 'PSV' would have such a structure created and attached to private state trie as it is essential in performing checks on future transactions affection those contracts.




