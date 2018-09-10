
  
# [sscjs](https://github.com/harpagon210/sscjs) 

Light javascript library to interact with the JSON RPC server of [a Steem Smart Contracts node](https://github.com/harpagon210/steemsmartcontracts)

Installation
------------

### Via npm

For node.js or the browser with [browserify](https://github.com/substack/node-browserify) or [webpack](https://github.com/webpack/webpack).

```
npm install sscjs
```

### From a cdn

From the [unpkg](https://unpkg.com) cdn:

```html
<script src="https://unpkg.com/sscjs/dist/ssc.min.js"></script>
```

See [unpkg.com](https://unpkg.com) for more information.


Usage
-----

### In the browser
This library requires the [axios library](https://github.com/axios/axios)

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script src="https://unpkg.com/sscjs/dist/ssc.min.js"></script>
<script>
    const ssc = new SSC('https://steemsmartcontracts.tk:5000');
    ssc.getLatestBlockInfo((err, result) => {
		console.log(err, result);
	});
</script>
```

### In node.js

```javascript
const SSC = require('ssc');

const ssc = new SSC('https://steemsmartcontracts.tk:5000');
ssc.stream((err, res) => {
	console.log(err, res);
});
```

Available methods
-----

```javascript
/**

* Get the information of a contract (owner, source code, etc...)

* @param  {String}  contract contract name

* @param  {Function}  callback callback called if passed

* @returns  {Promise<JSON>} returns a promise if no callback passed

*/

getContractInfo(contract, callback  =  null)

// example
ssc.getContractInfo('account', (err, result) => {
	console.log(err, result);
	/*
	{
	    "name": "account",
	    "owner": "harpagon",
	    "code": "...source code of the contract...",
	    "tables": [
	        "account_accounts"
	    ],
	    "meta": {
	        "revision": 0,
	        "created": 1536012789812,
	        "version": 0
	    },
	    "$loki": 1
	}
	*/
})
```

```javascript
/**

* retrieve a record from the table of a contract

* @param  {String}  contract contract name

* @param  {String}  table table name

* @param  {JSON}  query query to perform on the table

* @param  {Function}  callback callback called if passed

* @returns  {Promise<JSON>} returns a promise if no callback passed

*/

findOneInTable(contract, table, query, callback  =  null)

// example
ssc.findOneInTable(
	'account', 
	'accounts', 
	{ 
		id:  'harpagon' 
	}, (err, result) => {

	console.log(err, result);
	/*
	{
	    "id": "harpagon",
	    "meta": {
	        "revision": 0,
	        "created": 1536012984753,
	        "version": 0
	    },
	    "$loki": 1
	}
	*/
})
```

```javascript
/**

* retrieve records from the table of a contract

* @param  {String}  contract contract name

* @param  {String}  table table name

* @param  {JSON}  query query to perform on the table

* @param  {Function}  callback callback called if passed

* @returns  {Promise<JSON>} returns a promise if no callback passed

*/

findInTable(contract, table, query, callback  =  null)

// example
ssc.findInTable('account', 'accounts', { }, (err, result) => {
	console.log(err, result);
	/*
	[
	    {
	        "id": "harpagon",
	        "meta": {
	            "revision": 0,
	            "created": 1536012984753,
	            "version": 0
	        },
	        "$loki": 1
	    },
	    {
	        "id": "smmarkettoken",
	        "meta": {
	            "revision": 0,
	            "created": 1536460107491,
	            "version": 0
	        },
	        "$loki": 2
	    }
	]
	*/
})
```

```javascript
/**

* retrieve the latest block info of the sidechain

* @param  {Function}  callback callback called if passed

* @returns  {Promise<JSON>} returns a promise if no callback passed

*/

getLatestBlockInfo(callback  =  null)

// example
ssc.getLatestBlockInfo((err, result) => {
	console.log(err, result);
	/*
	{
	    "blockNumber": 12,
	    "refSteemBlockNumber": 25797141,
	    "previousHash": "9389c132270c7335b806a43bd063110fe3868015f96db80470bef2f48f1c2fcb",
	    "timestamp": "2018-09-09T02: 48: 48",
	    "transactions": [
	        {
	            "refSteemBlockNumber": 25797141,
	            "transactionId": "b299d24be543cd50369dbc83cf6ce10e2e8abc9b",
	            "sender": "smmarkettoken",
	            "contract": "smmkt",
	            "action": "updateBeneficiaries",
	            "payload": {
	                "beneficiaries": [
	                    "harpagon"
	                ],
	                "isSignedWithActiveKey": true
	            },
	            "hash": "ac33d2fcaf2d72477483ab1f2ed4bf3bb077cdb55d5371aa896e8f3fd034e6fd",
	            "logs": "{}"
	        }
	    ],
	    "hash": "e97e4b9a88b4ac5b8ed5f7806738052d565662eec962a0c0bbd171672a4a54d4",
	    "merkleRoot": "2f1221ae1938bc24f3ed593e8c57ea41882fedc5d31de21da9c9bd613360f3a6"
	}
	*/
})
```


```javascript
/**

* retrieve the specified block info of the sidechain

* @param  {Number}  blockNumber contract name

* @param  {Function}  callback callback called if passed

* @returns  {Promise<JSON>} returns a promise if no callback passed

*/

getBlockInfo(blockNumber, callback  =  null)

// example
ssc.getBlockInfo(12, (err, result) => {
	console.log(err, result);
	/*
	{
	    "blockNumber": 12,
	    "refSteemBlockNumber": 25797141,
	    "previousHash": "9389c132270c7335b806a43bd063110fe3868015f96db80470bef2f48f1c2fcb",
	    "timestamp": "2018-09-09T02: 48: 48",
	    "transactions": [
	        {
	            "refSteemBlockNumber": 25797141,
	            "transactionId": "b299d24be543cd50369dbc83cf6ce10e2e8abc9b",
	            "sender": "smmarkettoken",
	            "contract": "smmkt",
	            "action": "updateBeneficiaries",
	            "payload": {
	                "beneficiaries": [
	                    "harpagon"
	                ],
	                "isSignedWithActiveKey": true
	            },
	            "hash": "ac33d2fcaf2d72477483ab1f2ed4bf3bb077cdb55d5371aa896e8f3fd034e6fd",
	            "logs": "{}"
	        }
	    ],
	    "hash": "e97e4b9a88b4ac5b8ed5f7806738052d565662eec962a0c0bbd171672a4a54d4",
	    "merkleRoot": "2f1221ae1938bc24f3ed593e8c57ea41882fedc5d31de21da9c9bd613360f3a6"
	}
	*/
})
```

```javascript
/**

* stream part of the sidechain

* @param  {Number}  startBlock the first block to retrieve

* @param  {Number}  endBlock if passed the stream will stop after the block is retrieved

* @param  {Function}  callback callback called everytime a block is retrieved

* @param  {Number}  pollingTime polling time, default 1 sec

*/

streamFromTo(startBlock, endBlock  =  null, callback, pollingTime  =  1000)

// example
ssc.streamFromTo(0, 12, (err, result) => {
	console.log(err, result);
	/*
	{
	    "blockNumber": 12,
	    "refSteemBlockNumber": 25797141,
	    "previousHash": "9389c132270c7335b806a43bd063110fe3868015f96db80470bef2f48f1c2fcb",
	    "timestamp": "2018-09-09T02: 48: 48",
	    "transactions": [
	        {
	            "refSteemBlockNumber": 25797141,
	            "transactionId": "b299d24be543cd50369dbc83cf6ce10e2e8abc9b",
	            "sender": "smmarkettoken",
	            "contract": "smmkt",
	            "action": "updateBeneficiaries",
	            "payload": {
	                "beneficiaries": [
	                    "harpagon"
	                ],
	                "isSignedWithActiveKey": true
	            },
	            "hash": "ac33d2fcaf2d72477483ab1f2ed4bf3bb077cdb55d5371aa896e8f3fd034e6fd",
	            "logs": "{}"
	        }
	    ],
	    "hash": "e97e4b9a88b4ac5b8ed5f7806738052d565662eec962a0c0bbd171672a4a54d4",
	    "merkleRoot": "2f1221ae1938bc24f3ed593e8c57ea41882fedc5d31de21da9c9bd613360f3a6"
	}
	*/
})
```

```javascript
/**

* stream the sidechain (starting from the latest block produced)

* @param  {Function}  callback callback called everytime a block is retrieved

* @param  {Number}  pollingTime polling time, default 1 sec

*/

stream(callback, pollingTime  =  1000)

// example
ssc.stream((err, result) => {
	console.log(err, result);
	/*
	{
	    "blockNumber": 12,
	    "refSteemBlockNumber": 25797141,
	    "previousHash": "9389c132270c7335b806a43bd063110fe3868015f96db80470bef2f48f1c2fcb",
	    "timestamp": "2018-09-09T02: 48: 48",
	    "transactions": [
	        {
	            "refSteemBlockNumber": 25797141,
	            "transactionId": "b299d24be543cd50369dbc83cf6ce10e2e8abc9b",
	            "sender": "smmarkettoken",
	            "contract": "smmkt",
	            "action": "updateBeneficiaries",
	            "payload": {
	                "beneficiaries": [
	                    "harpagon"
	                ],
	                "isSignedWithActiveKey": true
	            },
	            "hash": "ac33d2fcaf2d72477483ab1f2ed4bf3bb077cdb55d5371aa896e8f3fd034e6fd",
	            "logs": "{}"
	        }
	    ],
	    "hash": "e97e4b9a88b4ac5b8ed5f7806738052d565662eec962a0c0bbd171672a4a54d4",
	    "merkleRoot": "2f1221ae1938bc24f3ed593e8c57ea41882fedc5d31de21da9c9bd613360f3a6"
	}
	*/
})
```