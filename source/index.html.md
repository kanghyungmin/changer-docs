--- 

title: Changer Pro API 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

**Version:** 1.0.0 

# /V1/BALANCES
## ***GET*** 

**Summary:** 

**Description:** show all balance for each pair

### HTTP Request 
`***GET*** /v1/balances` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | List all balances. |
| 401 | Unauthorized |

# /V1/CHANGER/QUOTE
## ***GET*** 

**Summary:** 

**Description:** Get a quote for a input pair.

### HTTP Request 
`***GET*** /v1/changer/quote` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| ticker | query | a pair to get a quote | Yes |  |
| quantity | query | quantity to sell or buy | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | item created |
| 401 | Unauthorized |

# /V1/CHANGER/TRADE
## ***POST*** 

**Summary:** 

**Description:** Place a order.

### HTTP Request 
`***POST*** /v1/changer/trade` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | item created |
| 401 | Unauthorized |

# /V1/CHANGER/TRADES
## ***GET*** 

**Summary:** 

**Description:** Get trade lists

### HTTP Request 
`***GET*** /v1/changer/trades` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| start | query | a pair to get a quote | Yes |  |
| length | query | quantity to sell or buy | Yes |  |
| type | query | quantity to sell or buy | Yes |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | trade succes |
| 401 | Unauthorized |

# /V1/COMMON/MARKET
## ***GET*** 

**Summary:** 

**Description:** show all pairs

### HTTP Request 
`***GET*** /v1/common/market` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | List all pairs to trade. |
| 401 | Unauthorized |

# /V1/COMMON/TOKEN
## ***POST*** 

**Summary:** 

**Description:** Generate a bearer token.

### HTTP Request 
`***POST*** /v1/common/token` 

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Get a bearer token. |

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
