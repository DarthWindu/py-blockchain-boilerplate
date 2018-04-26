# py-blockchain-template
A simple template to host local blockchains

# Blockchain API

**Default Node API Base**: `[node ip]:5000`

## GET

### /mine

 - Mines new block and returns new block
 - Success Response code: `200`
Response Structure: 
```python
response = {

'message': "new Block Forged",

'index': block['index'],

'transactions': block['transactions'],

'proof': block['proof'],

'previous_hash': block['previous_hash'],

}
```

### /chain

 - Returns chain as JSON
 - Success Response Code: `200`
Response Structure:
```python
response = {

'chain': blockchain.chain,

'length': len(blockchain.chain),

}
```
### /nodes/resolve

 - Resolves conflicts among nodes and determines which chain is authoritative
 - Returns authoritative chain and message to indicate whether the node's chain was replaced
 - Success Code: `200`
Response Structure:
```python
response = {

'message': 'Message String',

'chain': blockchain.chain

}
```

## POST

### /transactions/new
*makes a new transaction*

Parameter JSON requirements: 
```python 
# sender/recipient addresses and <int> amount exchanged
required = ['sender', 'recipient', 'amount']
```
Error Code: `400`

Returns message indicating which block TX will be added to (success code `201`).
Response Structure: 
```python
response = {
    'message': f'Transaction will be added to Block {index}'
}
```

### /nodes/register
*Registers new nodes to the blockchain network*

Parameter JSON Requirements:
```python
# List of node addresses to register
nodes = values.get('nodes')
```
Error Code: `400`
Success Code: `201`
Response Structure:
```python
response = {

'message': 'New nodes have been added',

'total_nodes': list(blockchain.nodes),

}
```
