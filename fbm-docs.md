# FBM API

## Get trade
### POST /fbm-request/
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  platform: { type: String },
  maximumBuyOutPrice: { type: Number },
  stock : { type: number },
  timestamp: { type: Number },
  hash: { type: String },
  ignoreHash: {type: array}
}
</pre>
* user: your username in our system
* platform: ```xbox``` or ```ps4```
* maximumBuyOutPrice: this is the maximum price of card what you can buy 
* stock: total user available coins for sell
* timestamp: unix timestamp
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5(user.timestamp.SECRET_WORD)
* ignoreHash: array of hashed FUT ACCOUNT emails which can't be used to buy given card 




#### Response Body (JSON)
<pre>
{
  code: { type: Number },
  transactionID: { type: Number },
  tradeID: { type: Number },
  assetID: { type: Number }, 
  resourceID: { type: Number }, 
  startPrice: { type: Number },
  coinAmount: { type: Number }, 
</pre>

* code: response code
* transactionID: the assigned transaction ID from our system
* tradeID: the trade ID from the EA transfer market
* resourceID: resource ID of the card
* assetID: the ID of the player
* playerName: the name of the player  
* startPrice: bidding start price
* coinAmount: buy now price  

## Update Status
### POST /fbm-status/
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  transactionID: { type: Number },
  status: { type: String }, 
  timestamp: { type: Number },
  hash: { type: String },
  emailHash: { type: String },
}
</pre>

* user: your username in our system
* transactionID: the assigned transaction ID in our system
* status: ```bought``` or ```cancel``` 
* timestamp: unix timestamp
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5(user.timestamp.SECRET_WORD)
* emailHash: md5 of FUT ACCOUNT email which were used to buy a card 

#### Response Body (JSON)
<pre>
{
  code: { type: Number },
  status: { type: Bool }
}
</pre>

* code: response code
* status: true/false

## Price info
### POST /fbm-price/
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  platform: { type: String },
  timestamp: { type: Number }
  hash: { type: String }
}
</pre>

* user: your username in our system
* platform: ```xbox``` or  ```ps4``` 
* timestamp: unix timestamp
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5(user.timestamp.SECRET_WORD)

#### Response Body (JSON)
<pre>
{
  code: { type: Number },
  platform: { type: String }, 
  price: { type: Number },
  currency: { type: String }
}
</pre>

* code: response code
* platform: ```xbox``` or  ```ps4``` 
* price: price
* currency: ```EUR```

## Errors
#### Error Response Body (JSON)
<pre>
{
  code: { type: Number },
  error: { type: String }
}
</pre>

## Response codes
| Response Code | Description |
| --- | --- |
| 200 | success |
| 400 | bad request |
| 403 | permission denied |
| 404 | trade not found | 
