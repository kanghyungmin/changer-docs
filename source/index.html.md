--- 

title: Changer Pro API 

language_tabs: 
   - javascript

toc_footers: 
  #  - <a href='#'>Sign Up for a Developer Key</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

**Version:** 1.0.0 

Welcome to the Changer API!

Changer offers a REST API to access market data, manage your account, and create orders.

# Authentication
```javascript
const jwt = require('jsonwebtoken')

const payload = {
    accessKey: '<access_key>',
    nonce: '<Random String>',
  };
const jwtToken = jwt.sign(payload, '<secret_key>');
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "token": "<token>"
}
```

Changer uses API keys to grant access.  
You can create API keys to contact <help@changer.io>.   
Then, you can get a API keys which consists of a access key(`access_key`) and a secret key(`secret_key`).

As a next step, you should generate a jwt token with API keys by referring to the example code. 
The token should be included in most API requests to the server in the Authorization header that looks like the following:

`Authorization: Bearer <token>`
# REST Endpoints
| Endpoint | Description |
| :----: | :----------- |<Align>
| Production | https://api.changer.io |
| Sandbox | [Contact Us](help@changer.io) | 

# Account Management
## Get Account Balance

```javascript
const request = require('request');

const options = {
  'method': 'GET',
  'url': "https://api.changer.io/v1/balances",
  'headers': {
    'Authorization': 'Bearer <token>',
    'Content-Type': 'application/json'
  }
};

request(options, function (error:any, response: any) { 
  if (error) throw new Error(error);
  console.log(response);
});
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "totalCount": 2,
  "balances": [
    {
      "available": "0.71",
      "locked": "0",
      "currency": "btc"
    },
    {
      "available": "1.25",
      "locked": "0",
      "currency": "eth"
    }
  ]
}
```
<!-- **Summary:**  -->


### Description
Show all balance for each pair

### HTTP Request 
`GET /v1/balances` 

# Market Data

## Get Pairs
```javascript
const request = require('request');
const options = {
  'method': 'GET',
  'url': "https://api.changer.io/v1/common/market",
  'headers': {
    'Authorization': 'Bearer <token>',
    'Content-Type': 'application/json'
  }
};

request(options, function (error:any, response: any) { 
  if (error) throw new Error(error);
  console.log(response.body);
});
```
> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "markets": [
    {
      "baseCurrency": {
        "name": "xrp",
        "id": "5cdaab544fee8b2a6dd64e98"
      },
      "quoteCurrency": {
        "name": "usdt",
        "id": "5cdaab544fee8b2a6dd64e7c"
      },
      "id": "5cdaaca62a13dc2b280b573b"
    },
    {
      "baseCurrency": {
        "name": "eos",
        "id": "5cdaab544fee8b2a6dd64e81"
      },
      "quoteCurrency": {
        "name": "btc",
        "id": "5cdaab544fee8b2a6dd64e7d"
      },
      "id": "5cdaab544fee8b2a6dd64e7d"
    }
  ]
}
```

### Description 
Get all pairs to trade
### HTTP Request 
`GET /v1/common/market` 

## Get Quote Information
```javascript
const request = require('request');
const options = {
  'method': 'GET',
  'url': "https://api.changer.io/v1/changer/quote?ticker=BTC_USDT&quantity=10",
  'headers': {
    'Authorization': 'Bearer <token>',
    'Content-Type': 'application/json'
  }
};

request(options, function (error:any, response: any) { 
  if (error) throw new Error(error);
  console.log(response.body);
});

```
> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "origin": "cumberland",
  "quote": {
    "requestId": "BTC_USDT:USDT:100-20438244-879e-4bc3-b523-3d04def0bdf8\"",
    "responseId": {
      "version": 1,
      "id": "a5a3dca3-36f6-4d1a-b43f-c87327285754"
    },
    "quoteData": {
      "ticker": "BTC_USDT",
      "currency": "USDT",
      "buy": {
        "quantity": 0.0052108,
        "price": 19190.9,
        "amount": 100
      },
      "sell": {
        "quantity": 0.00520289,
        "price": 19220.1,
        "amount": 100
      }
    }
  }
}
```
### Description 
Get a quote information.

### HTTP Request 
`GET /v1/changer/quote` 

### Parameters

| Name | Location | Description | Required | Type |
| :----: | :----------: | :----------- | :--------: | :----: |<Align>
| ticker | query | ticker name | Yes | string |
| quantity | query | trade volume | Yes | string |


# Orders
## Place a Order
```javascript
const request = require('request');
const reqBody = JSON.stringify({
  "ticker": "btc_usdt",
  "quantity": "1",
  "action": "sell",
  "version": 4,
  "id": "06b3a147-831c-462f-b24a-439cfa510373"
  })
const options = {
  'method': 'post',
  'body': reqBody,
  'url': "https://api.changer.io/v1/changer/trade",
  'headers': {
    'Authorization': 'Bearer <token>',
    'Content-Type': 'application/json'
  }
};

request(options, function (error:any, response: any) { 
  if (error) throw new Error(error);
  console.log(response.body);
});
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "tradeId": "61f0cdb923681d5232e31812",
  "data": {
    "price": "37258",
    "quantity": "1",
    "amount": "37258",
    "action": "sell",
    "quoteOrigin": "b2c2",
    "executedData": {
      "tradeId": "25712e0b-062c-4cd4-84b1-5c1bc3c05598",
      "ticker": "BTC_USDT",
      "currency": "BTC",
      "action": "sell",
      "amount": "37258.00000000",
      "quantity": "1.0000000000",
      "price": "37258.00000000",
      "origin": "b2c2"
    }
  }
}
```
### Description
Place a order.

### HTTP Request 
`POST /v1/changer/trade` 

### Parameters

| Name | Location | Description | Required | Type |
| :----: | :----------: | :----------- | :--------: | :----: |<Align>
| ticker | body | ticker name | Yes | string |
| quantity | body | trade volume | Yes | string |
| action | body | buy or sell | Yes | string |

## Get Trade Lists
```javascript
const request = require('request');
const options = {
  'method': 'GET',
  'url': "https://api.changer.io/v1/changer/trades?start=0&length=10&type=trade",
  'headers': {
    'Authorization': 'Bearer <token>',
    'Content-Type': 'application/json'
  }
};
request(options, function (error:any, response: any) { 
  if (error) throw new Error(error);
  console.log(response.body);
});
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok",
  "totalCount": 1,
  "trades": [
    {
      "type": "0.71",
      "status": "0",
      "market": {
        "name": "btc_usdt",
        "id": "5cdaaca62a13dc2b280b572d"
      },
      "side": "buy",
      "price": "33521.6",
      "volume": "0.00298315",
      "amount": "100",
      "info": {
        "tradeId": "5bed8498-aec6-4800-b921-1ad9aeb74dcf",
        "action": "BUY",
        "ticker": "BTC_USDT",
        "currency": "USDT",
        "quantity": 0.00300771,
        "price": 33247.9,
        "amount": 100,
        "origin": "cumberland"
      },
      "createdAt": 1611556149091,
      "updatedAt": 1611556149091,
      "readableCreatedAt": "2021-01-25 15:29:09",
      "readableUpdatedAt": "2021-01-25 15:29:09",
      "id": "600e6535fe0d4b2b1322344b"
    }
  ]
}
```
### Description
Get trade lists

### HTTP Request 
`GET /v1/changer/trades` 

### Parameters

| Name | Locattion | Description | Required | Type |
| :----: | :----------: | :-------------------------- | :--------: | :-----: |<Align>
| start | query | the strat index to bring in the tradeing list. For example, '0' is the latest trade | Yes | string |
| length | query | the number of items to be taken sequentially form the start index  | Yes | string |
| type | query | As a trading type. It is one of the three among trade, liqudation, and settlement.   | Yes | string |