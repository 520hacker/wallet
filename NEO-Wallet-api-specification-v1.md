# NEO Wallet API Specification
Github: http://www.github.com/neo-specification/wallet
version: v1

## API List
| API                                   | description                              |
| ------------------------------------- | ---------------------------------------- |
| get_net                               | Get current blockchain network.          |
| get_api_list                          | Get support api list.                    |
| block/get_height                      | Get current block height.                |
| address/get_balances                  | Get balances of asset belongs to **address**. |
| address/get_unspent                   | Get unspent UTXO of **asset** belongs to **address**. |
| address/get_claims                    | Get claims detail of **address**.        |
| transaction/get_raw_transaction       | Get transaction raw data by **txid**.    |
| transaction/make_transfer_transaction | Make transfer transaction and get unsigned transaction raw data. |
| transaction/make_claims_transaction   | Make claim transaction and get unsigned transaction raw data. |
| transaction/validate_transaction      | Send unsigned transfer transaction and return detail of it. |
| transaction/send_sign_transaction     | Send transaction with signature and publickey. |
| transaction/send_raw_transaction      | Send raw transaction to blockchain network. |

## API Reference
- ### get_net
  **GET** /{version}/get_net

  description:
  Get current blockchain network.

  paramer:
  	none
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	  	"net":"testnet"
  	  }
  	}

- ### get_api_list
  **GET** /{version}/get_api_list

  description:
  Get support api list.

  paramer:
  	none
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{[
  	      "getnet",
  	      "getapilist",
  	      "getheight",
  	      "getrawtransaction",
  	      ...
  	  ]}
  	}

- ### get_height
  **GET** /{version}/block/get_height

  description:
  Get current block height.

  paramer:
  	none
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	  	"height":100001
  	  }
  	}

- ### get_raw_transaction
  **GET** /{version}/transaction/get_raw_transaction/**{txid}**

  description:
  Get transaction raw data by **txid**.

  paramer:
  	hash
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{[
  	  	"400000455b7b226c616e67223a227a682d434e222c226e616d65223a22e5b08fe89a81e882a1227d2c7b226c616e67223a22656e222c226e616d65223a22416e745368617265227d5d0000c16ff28623000000da1745e9b549bd0bfa1a569971c77eba30cd5a4b00000000"
  	  ]}
  	}


- ### get_balances
  **GET** /{version}/address/get_balances/**{address}**

  description:
  Get balances of asset belongs to **address**.

  paramer:
  	address
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	      [{
  	          "assetid":"c56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b",
  	          "assetname":"\u5c0f\u8681\u80a1",
  	          "balance":"500",
  	      },
  	      {
  	          "assetid":"602c79718b16e442de58778e148d0b1084e3b2dffd5de6b7b16cee7969282de7",
  	          "assetname":"\u5c0f\u8681\u5e01",
  	          "balance":"915.19047136",
  	      }]
  	   }
  	}

- ### get_unspent
  **GET** /{version}/address/get_unspent/**{address}**/**{assetid}**

  description:
  Get unspent UTXO of **asset** belongs to **address**.

  paramer:
  	address,assetid
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	      [{
  	          "txid":"e974fdd75191bd73cfcc73e98ac08aed4d92381ffdbb994b5395ffcb608430db",
  	          "index":0,
  	          "value":"499",
  	      },
  	      {
  	          "txid":"083f28db850438d7f4c45d6970fd3b7ae9aeaeaa11cabef9bfc8a30dd634e6ed",
  	          "index":2,
  	          "value":"1",
  	      }]
  	   }
  	}

- ### get_claims
  **GET** /{version}/address/get_claims/**{address}**

  description:
  Get claims detail of **address**.

  paramer:
  	address
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	          "assetid":"602c79718b16e442de58778e148d0b1084e3b2dffd5de6b7b16cee7969282de7",
  	          "amount":"0.0736",
  	          "claims":[{
  	              "txid":"d7ef0bf14e66ae15e4077addce6e4ca50394375314f68fae7aa7259bcb52f90a",
  	              "index":0,
  	              "claim":"0.0736",
  	          }]
  	   }
  	}


- ###make_transfer_transaction
  **POST** /{version}/transaction/make_transfer_transaction

  description:
  Make transfer transaction and get unsigned transaction raw data.

  example paramer:
  	{
  		"assetid":"c56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b"
  		"amount":"100"
  		"todddress":"AGX8Xw1HbWGFwozH4tH1ej14FXVdkeTTau"
  		"fromaddress":"AQSqZUpRbf5KpxtATT5NFTLE2rE4Cd2MJq"
  	}
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{[
  	              "800000019577a388c0ddb61c722bba492062fe006cda3491e14248a68f096939528b34b80000029b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc500e40b5402000000082e502f35ec5cf8cc1209d0de00c550578911a79b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc50054e4b2280000005f1f7caef4c5712fe63d09d81979ab7b36b6eda1"
  	  ]}
  	}

- ###validate_transaction
  **POST** /{version}/transaction/validate_transaction

  description:
  Send unsigned transfer transaction and return detail of it.

  example paramer:
  	{[
  		"800000019577a388c0ddb61c722bba492062fe006cda3491e14248a68f096939528b34b80000029b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc500e40b5402000000082e502f35ec5cf8cc1209d0de00c550578911a79b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc50054e4b2280000005f1f7caef4c5712fe63d09d81979ab7b36b6eda1"
  	]}
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{
  	  	"type":"ContractTransaction",
  	      "version":0,
  	      "payload":{},
  	      "attributes":[],
  	      "input":[
  	      	{
  	          	"txid":"9577a388c0ddb61c722bba492062fe006cda3491e14248a68f096939528b34b8",
  	              "vout":0
  	          }
  	      ],
  	      "output":[
  	      	{
  	          	"index":0,
  	          	"assetid":"c56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b",
  	              "value":"100",
  	              "address":"AGX8Xw1HbWGFwozH4tH1ej14FXVdkeTTau"
  	          },
  	          {
  	          	"index":1,
  	          	"assetid":"c56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b",
  	              "value":"1748",
  	              "address":"AQSqZUpRbf5KpxtATT5NFTLE2rE4Cd2MJq"
  	          }
  	      ]
  	   }
  	}

- ###make_claims_transaction
  **POST** /{version}/transaction/make_claims_transaction

  description:
  Make claim transaction and get unsigned transaction raw data.

  example paramer:
  	{
  	  "address":"AGX8Xw1HbWGFwozH4tH1ej14FXVdkeTTau"
  	}
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{[
  	              "0200010af952cb9b25a77aae8ff61453379403a54c6ecedd7a07e415ae664ef10befd70000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60004e700000000000082e502f35ec5cf8cc1209d0de00c550578911a7",
  	  ]}
  	}

- ###send_sign_transaction
  **POST** /{version}/transaction/send_sign_transaction

  description:
  Send transaction with signature and publickey, let API server make and send the transaction to blockchain network.

  example paramer:
  	{  "unsigned":"0200010af952cb9b25a77aae8ff61453379403a54c6ecedd7a07e415ae664ef10befd70000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60004e700000000000082e502f35ec5cf8cc1209d0de00c550578911a7",  "signature":"f456bf28dcab2f0e237e21dd16c46b160e62b5349b2b1248dd4bbee4653146270470bface4e02e3e4593a3db33d51053526d002b42eae89c616391c59de7d3b3",  "publickey":"039fbb47841f7338c0c654addd6225995642b5b6d492413563f7f8755ba83c0ecd"
  	}
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":{[
  				"0200010af952cb9b25a77aae8ff61453379403a54c6ecedd7a07e415ae664ef10befd70000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60004e700000000000082e502f35ec5cf8cc1209d0de00c550578911a7014140f456bf28dcab2f0e237e21dd16c46b160e62b5349b2b1248dd4bbee4653146270470bface4e02e3e4593a3db33d51053526d002b42eae89c616391c59de7d3b32321039fbb47841f7338c0c654addd6225995642b5b6d492413563f7f8755ba83c0ecdac"
  	   ]}
  	}

- ###send_raw_transaction
  **POST** /{version}/transaction/send_raw_transaction

  description:
  Send raw transaction to blockchain network.

  example paramer:
  	{[
  	"0200010af952cb9b25a77aae8ff61453379403a54c6ecedd7a07e415ae664ef10befd70000000001e72d286979ee6cb1b7e65dfddfb2e384100b8d148e7758de42e4168b71792c60004e700000000000082e502f35ec5cf8cc1209d0de00c550578911a7014140f456bf28dcab2f0e237e21dd16c46b160e62b5349b2b1248dd4bbee4653146270470bface4e02e3e4593a3db33d51053526d002b42eae89c616391c59de7d3b32321039fbb47841f7338c0c654addd6225995642b5b6d492413563f7f8755ba83c0ecdac"
  	]}
  example return:
  	{
  	  "code":200,
  	  "message":"OK",
  	  "result":"success"
  	}

## Response code
    200  : OK
    400  : Bad Request
    404  : NOT FOUND
    500  : Internal Server Error

## NEO Wallet Specification Standardization Committee
- http://www.otcgo.cn
- http://www.antchain.xyz
- http://www.neowallet.net
- NEO dun
