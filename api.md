# IC Explorer API Documentation

## Overview
This documentation describes the REST API endpoints for IC Explorer, providing functionality for querying transaction history and token holdings on the Internet Computer blockchain. The API supports detailed transaction tracking, token holder information, and user token balance queries.

## API Endpoints Table of Contents

### 1. Transaction List Query
- **Endpoint**: `POST /api/tx/list`
- **Purpose**: Retrieve paginated transaction history with filtering options
- **Key Features**:
  - Transaction filtering by time range, category, and token
  - Support for multiple transaction types
  - Detailed transaction information including token transfers and swaps

### 2. Token Holder Query
- **Endpoint**: `POST /api/holder/token`
- **Purpose**: Get token holder information for specific tokens
- **Key Features**:
  - Paginated holder list
  - Token balance and USD value
  - Holder details including account information

### 3. User Token List Query
- **Endpoint**: `POST /api/holder/user`
- **Purpose**: Retrieve token holdings for specific users
- **Key Features**:
  - Query by principal, accountId, or accountTextual
  - Token balance and USD value information
  - Detailed token holding information

---


### 1. Transaction List Query

**Endpoint**: `https://open-api.icexplorer.io/api/tx/list`

**Method**: POST

**Request Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | Integer | Yes | Page number, starts from 1 |
| size | Integer | Yes | Number of records per page |
| beginTime | Long | No | Start time, timestamp |
| endTime | Long | No | End time, timestamp |
| category | String | No | Transaction category, like: SWAP,TOKEN,STAKE,FARM |
| token0LedgerId | String | No | Token0 ledgerId,if you want to query by token ledgerId, you can set this parameter |
| token1LedgerId | String | No | Token1 ledgerId |
| txTypes | List<String> | No | Transaction types, like: transfer,approve,transferFrom,mint,burn,swap,stake,unstake,claim,harvest |
| principal | String | No | Principal |
| accountId | String | No | AccountId |
| accountTextual | String | No | AccountTextual |

**Response Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| statusCode | Integer | Response code (600: Success) |
| message | String | Response message |
| data | PageInfo<TransactionResponse> | Response data of transaction list |
|- pageNum | Integer | Page number |
|- pageSize | Integer | Number of records per page |
|- size | Integer | Number of records currently on this page |
|- pages | Integer | Total number of pages |
|- total | Long | Total number of records |
|- list | Array<TransactionResponse> | List of transactions |
|&nbsp;&nbsp;&nbsp;&nbsp;-- category | String | Transaction category |
|&nbsp;&nbsp;&nbsp;&nbsp;-- source | String | Transaction source |
|&nbsp;&nbsp;&nbsp;&nbsp;-- sourceCanister | String | Transaction source canister |
|&nbsp;&nbsp;&nbsp;&nbsp;-- op | String | Transaction type |
|&nbsp;&nbsp;&nbsp;&nbsp;-- fromOwner | String | Transaction from owner |
|&nbsp;&nbsp;&nbsp;&nbsp;-- fromSubaccount | String | Transaction from subaccount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- fromAccountId | String | Transaction from accountId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- fromAlias | String | Transaction from alias |
|&nbsp;&nbsp;&nbsp;&nbsp;-- fromAccountTextual | String | Transaction from accountTextual |
|&nbsp;&nbsp;&nbsp;&nbsp;-- toOwner | String | Transaction to owner |
|&nbsp;&nbsp;&nbsp;&nbsp;-- toSubaccount | String | Transaction to subaccount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- toAccountId | String | Transaction to accountId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- toAlias | String | Transaction to alias |
|&nbsp;&nbsp;&nbsp;&nbsp;-- toAccountTextual | String | Transaction to accountTextual |
|&nbsp;&nbsp;&nbsp;&nbsp;-- spenderOwner | String | Transaction spender owner |
|&nbsp;&nbsp;&nbsp;&nbsp;-- spenderSubaccount | String | Transaction spender subaccount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- spenderAccountId | String | Transaction spender accountId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- spenderAlias | String | Transaction spender alias |
|&nbsp;&nbsp;&nbsp;&nbsp;-- spenderAccountTextual | String | Transaction spender accountTextual |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0LedgerId | String | Transaction token0 ledgerId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0Amount | BigDecimal | Transaction token0 amount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0Decimal | Integer | Transaction token0 decimal |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0Fee | BigDecimal | Transaction token0 fee |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0TxMemo | String | Transaction token0 txMemo |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0TxHash | String | Transaction token0 txHash |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0TxIndex | Long | Transaction token0 txIndex |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0TxTime | Date | Transaction token0 txTime |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0Value | BigDecimal | Transaction token0 value |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token0Symbol | String | Transaction token0 symbol |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1LedgerId | String | Transaction token1 ledgerId,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1Amount | BigDecimal | Transaction token1 amount,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1Decimal | Integer | Transaction token1 decimal,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1Fee | BigDecimal | Transaction token1 fee,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1TxMemo | String | Transaction token1 txMemo,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1TxHash | String | Transaction token1 txHash,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1TxIndex | Integer | Transaction token1 txIndex,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1TxTime | Date | Transaction token1 txTime,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1Value | BigDecimal | Transaction token1 value,if category is SWAP,this field will have valid data |
|&nbsp;&nbsp;&nbsp;&nbsp;-- token1Symbol | String | Transaction token1 symbol,if category is SWAP,this field will have valid data |

**Request Example**:
```json
{
    "page": 1,
    "size": 10,
    "beginTime": 1725507471000,
    "endTime": 1725517471000,
    "txTypes": ["swap","transfer"],
    "category": "SWAP",
    "token0LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
    "principal": "angxa-baaaa-aaaag-qcvnq-cai"
//    "accountId": "37f5f4aec58b4afd98d710579376b1fb48b748e9292aa918e805e93bda153209",
//    "accountTextual": "angxa-baaaa-aaaag-qcvnq-cai-zzmja7y.1d203dada1410292196ab797295332706e4ecc6c26f3f5754509242cc8020000"
}
```

**Response Example**:
```json
{
    "statusCode": 600,
    "message": "success",
    "data": {
        "pageNum": 1,
        "pageSize": 10,
        "size": 10,
        "pages": 1,
        "total": 10,
        "list": [
            {
                "category": "TOKEN",
                "source": "IC",
                "sourceCanister": "ss2fx-dyaaa-aaaar-qacoq-cai",
                "op": "transfer",
                "fromOwner": "angxa-baaaa-aaaag-qcvnq-cai",
                "fromSubaccount": "1d203dada1410292196ab797295332706e4ecc6c26f3f5754509242cc8020000",
                "fromAccountId": "37f5f4aec58b4afd98d710579376b1fb48b748e9292aa918e805e93bda153209",
                "fromAccountTextual": "angxa-baaaa-aaaag-qcvnq-cai-zzmja7y.1d203dada1410292196ab797295332706e4ecc6c26f3f5754509242cc8020000",
                "toOwner": "angxa-baaaa-aaaag-qcvnq-cai",
                "toSubaccount": "0000000000000000000000000000000000000000000000000000000000000000",
                "toAccountId": "df0104537832781dc8ed6f68298bb68edf788e2d03a81c47332f3981caa6646d",
                "toAlias": "ICPSwap:ICP/ckETH",
                "toAccountTextual": "angxa-baaaa-aaaag-qcvnq-cai",
                "token0LedgerId": "ss2fx-dyaaa-aaaar-qacoq-cai",
                "token0Amount": "0.2614484204970286",
                "token0Decimal": 18,
                "token0Fee": "0.0000020000000000",
                "token0TxMemo": "0000000000028ad9",
                "token0TxIndex": "644702",
                "token0TxTime": 1725517471000,
                "token0Value": "634.7190689445146827",
                "token0Symbol": "ckETH"
            },
            {
                "category": "TOKEN",
                "source": "IC",
                "sourceCanister": "ryjl3-tyaaa-aaaaa-aaaba-cai",
                "op": "transfer",
                "fromOwner": "angxa-baaaa-aaaag-qcvnq-cai",
                "fromSubaccount": "0000000000000000000000000000000000000000000000000000000000000000",
                "fromAccountId": "df0104537832781dc8ed6f68298bb68edf788e2d03a81c47332f3981caa6646d",
                "fromAlias": "ICPSwap:ICP/ckETH",
                "fromAccountTextual": "angxa-baaaa-aaaag-qcvnq-cai",
                "toOwner": "dwx4w-plydf-jxgs5-uncbu-mfyds-5vjzm-oohax-gmvja-cypv7-tmbt4-dqe",
                "toSubaccount": "0000000000000000000000000000000000000000000000000000000000000000",
                "toAccountId": "4ec84f148280c743948b2f54911bbcdcbc6996169f20b52eafd03544d03453fa",
                "toAccountTextual": "dwx4w-plydf-jxgs5-uncbu-mfyds-5vjzm-oohax-gmvja-cypv7-tmbt4-dqe",
                "token0LedgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
                "token0Amount": "1.7912313900000000",
                "token0Decimal": 8,
                "token0Fee": "0.0001000000000000",
                "token0TxMemo": "0000000000028ad8",
                "token0TxHash": "7a9ec23bed6dc769e6241b576c22e7a30fbeb6ce731dd2005727ad3d9863635d",
                "token0TxIndex": "13808370",
                "token0TxTime": 1725517465000,
                "token0Value": "13.3960638668193121",
                "token0Symbol": "ICP"
            }
        ]
    }
}
```
### Token Holder Query

**Endpoint**: `https://open-api.icexplorer.io/api/holder/token`

**Method**: POST

**Request Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | Integer | Yes | Page number, starts from 1 |
| size | Integer | Yes | Number of records per page |
| ledgerId | String | Yes | Token ledgerId |
| isDesc | Boolean | No | Whether to sort in descending order, default is true |

**Response Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| statusCode | Integer | Response code (600: Success) |
| message | String | Response message |
| data | PageInfo<TokenHolderResponse> | Response data of token holder list |
|- pageNum | Integer | Page number |
|- pageSize | Integer | Number of records per page |
|- size | Integer | Number of records currently on this page |
|- pages | Integer | Total number of pages |
|- total | Long | Total number of records |
|- list | Array<TokenHolderResponse> | List of token holders |
|&nbsp;&nbsp;&nbsp;&nbsp;-- ledgerId | String | Token ledgerId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- symbol | String | Token symbol |
|&nbsp;&nbsp;&nbsp;&nbsp;-- totalSupply | BigDecimal | Token total supply |
|&nbsp;&nbsp;&nbsp;&nbsp;-- owner | String | Token owner |
|&nbsp;&nbsp;&nbsp;&nbsp;-- subaccount | String | Token subaccount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- accountId | String | Token accountId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- alias | String | Token alias |
|&nbsp;&nbsp;&nbsp;&nbsp;-- amount | BigDecimal | Token amount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- tokenDecimal | Integer | Token decimal |
|&nbsp;&nbsp;&nbsp;&nbsp;-- snapshotTime | Date | Token snapshot time |
|&nbsp;&nbsp;&nbsp;&nbsp;-- valueUSD | BigDecimal | Token value in USD |

**Request Example**:
```json
{
    "page": 1,
    "size": 10,
    "ledgerId": "zfcdd-tqaaa-aaaaq-aaaga-cai",
    "isDesc": true
}
```
**Response Example**:
```json
{
    "statusCode": 600,
    "message": "success",
    "data": {
        "pageNum": 1,
        "pageSize": 10,
        "size": 10,
        "pages": 1,
        "total": 10,
        "list": [
            {
                "ledgerId": "zfcdd-tqaaa-aaaaq-aaaga-cai",
                "symbol": "DKP",
                "totalSupply": "7999999882.1639400000000000",
                "owner": "zqfso-syaaa-aaaaq-aaafq-cai",
                "subaccount": "f513314523830ed270c65c4fa2bd6473b2bba3e4faf91b0e0782bf21c2e4ab25",
                "accountId": "b089182699492a3013ac39e20f630d19a2023fa87987a427afa94dc81cf6e5fd",
                "amount": "4008888888.8783044400000000",
                "tokenDecimal": 8,
                "snapshotTime": 1722888531000,
                "valueUSD": "13847824.711074549461003200000000"
            },
            {
                "ledgerId": "zfcdd-tqaaa-aaaaq-aaaga-cai",
                "symbol": "DKP",
                "totalSupply": "7999999787.2979400000000000",
                "owner": "zqfso-syaaa-aaaaq-aaafq-cai",
                "subaccount": "cec2145a750fd4a472b2a021f6dff1e4a907299700062a0a02bc1ea65ca29258",
                "accountId": "e369c0b9f637401784e0978eceb149f6e988365e1d427bb0cede82a72e375cde",
                "amount": "371342774.3114135100000000",
                "tokenDecimal": 8,
                "snapshotTime": 1731945699000,
                "valueUSD": "1282721.918448429459322800000000"
            }
        ]
    }
}
```

### User Token List Query

**Endpoint**: `https://open-api.icexplorer.io/api/holder/user`

**Method**: POST

**Request Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | Integer | Yes | Page number, starts from 1 |
| size | Integer | Yes | Number of records per page |
| principal | String | No | Principal |
| accountId | String | No | AccountId |
| accountTextual | String | No | AccountTextual |
| isDesc | Boolean | No | Whether to sort in descending order, default is true |

**Response Parameters**:
| Parameter | Type | Description |
|-----------|------|-------------|
| statusCode | Integer | Response code (600: Success) |
| message | String | Response message |
| data | PageInfo<TokenHolderResponse> | Response data of token holder list |
|- pageNum | Integer | Page number |
|- pageSize | Integer | Number of records per page |
|- size | Integer | Number of records currently on this page |
|- pages | Integer | Total number of pages |
|- total | Long | Total number of records |
|- list | Array<TokenHolderResponse> | List of token holders |
|&nbsp;&nbsp;&nbsp;&nbsp;-- ledgerId | String | Token ledgerId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- symbol | String | Token symbol |
|&nbsp;&nbsp;&nbsp;&nbsp;-- totalSupply | BigDecimal | Token total supply |
|&nbsp;&nbsp;&nbsp;&nbsp;-- owner | String | Token owner |
|&nbsp;&nbsp;&nbsp;&nbsp;-- subaccount | String | Token subaccount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- accountId | String | Token accountId |
|&nbsp;&nbsp;&nbsp;&nbsp;-- alias | String | Token alias |
|&nbsp;&nbsp;&nbsp;&nbsp;-- amount | BigDecimal | Token amount |
|&nbsp;&nbsp;&nbsp;&nbsp;-- tokenDecimal | Integer | Token decimal |
|&nbsp;&nbsp;&nbsp;&nbsp;-- snapshotTime | Date | Token snapshot time |
|&nbsp;&nbsp;&nbsp;&nbsp;-- valueUSD | BigDecimal | Token value in USD |

**Request Example**:
```json
{
    "page": 1,
    "size": 10,
    "principal": "angxa-baaaa-aaaag-qcvnq-cai",
    "isDesc": true
}
```

**Response Example**:
```json
{
    "statusCode": 600,
    "message": "success",
    "data": {
        "pageNum": 1,
        "pageSize": 10,
        "size": 3,
        "pages": 1,
        "total": 3,
        "list": [
            {
            "ledgerId": "ryjl3-tyaaa-aaaaa-aaaba-cai",
            "symbol": "ICP",
            "totalSupply": "525622960.1603181200000000",
            "owner": "zqfso-syaaa-aaaaq-aaafq-cai",
            "subaccount": "0000000000000000000000000000000000000000000000000000000000000000",
            "accountId": "7765cb3b0431c7043e400e1953d3ed683bf206dfd07f166db5cd5d76089a11e7",
            "amount": "27209.4396645500000000",
            "tokenDecimal": 8,
            "snapshotTime": 1732285020000,
            "valueUSD": "333225.638492291827711000000000"
        },
        {
            "ledgerId": "4c4fd-caaaa-aaaaq-aaa3a-cai",
            "symbol": "GHOST",
            "totalSupply": "9249324418.1235980800000000",
            "owner": "zqfso-syaaa-aaaaq-aaafq-cai",
            "subaccount": "0000000000000000000000000000000000000000000000000000000000000000",
            "accountId": "7765cb3b0431c7043e400e1953d3ed683bf206dfd07f166db5cd5d76089a11e7",
            "amount": "200.0000000000000000",
            "tokenDecimal": 8,
            "snapshotTime": 1722890055000,
            "valueUSD": "0.052774000000000000000000"
        },
        {
            "ledgerId": "ca6gz-lqaaa-aaaaq-aacwa-cai",
            "symbol": "ICS",
            "totalSupply": "993293856.0225607100000000",
            "owner": "zqfso-syaaa-aaaaq-aaafq-cai",
            "subaccount": "0000000000000000000000000000000000000000000000000000000000000000",
            "accountId": "7765cb3b0431c7043e400e1953d3ed683bf206dfd07f166db5cd5d76089a11e7",
            "amount": "2.9100000000000000",
            "tokenDecimal": 8,
            "snapshotTime": 1722919810000,
            "valueUSD": "0.050383769100000000000000"
        }
        ]
    }
}
```