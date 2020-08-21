# Privacy Enhancement  APIs
## APIs
### `getContractPrivacyMetadata` 
The api to query the Privacy Metadata for a contract account address
#### Parameter
* contract address

#### Returns
* `creationTxHash`: ACOTH
* `privacyFlag`: unsigned integer with `1` for PP, `3` for PSV contracts (default value is `0`).

#### Examples

```jshelllanguage tab="JSON RPC"
// Request
curl -X POST http://127.0.0.1:22001 --data '{"jsonrpc":"2.0","method":"getContractPrivacyMetadata","params":["0x1349f3e1b8d71effb47b840594ff27da7e603d17"],"id":15}' --header "Content-Type: application/json"

// Response
{"jsonrpc":"2.0","id":10,"result":"0xceffe8051d098920ac84e33b8a05c48180ed9b26581a6a06ce9874a1bf1502bd"}
```

```javascript tab="geth console"
> quorumExtension.extendContract("0x9aff347f193ca4560276c3322193224dcdbbe578", "BULeR8JyUWhiuuCMU/HLA0Q5pzkYT+cHII3ZKBey3Bo=", "0xed9d02e382b34818e88b88a309c7fe71e65f419d",{from: "0xca843569e3427144cead5e4d5999a3d0ccf92b8e", privateFor:["BULeR8JyUWhiuuCMU/HLA0Q5pzkYT+cHII3ZKBey3Bo="]})

"0x9e0101dd215281b33989b3ae093147e9009353bb63f531490409a628c6e87310"
```
