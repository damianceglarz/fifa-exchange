# FBM API

## Get trade
### POST /fbm-request
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  platform: { type: String },
  maximumBuyOutPrice: { type: Number },
  stock : { type: number }
  hash: { type: String }
}
</pre>
* user: your username in our system
* platform: ```xbox``` or ```ps4```
* maximumBuyOutPrice: this is the maximum price of card what you can buy 
* stock: total user stock
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5(user.SECRET_WORD)




#### Response Body (JSON)
<pre>
{
  code: { type: Number },
  transactionID: { type: Number },
  tradeID: { type: Number },
  assetID: { type: Number }, 
  startPrice: { type: Number },
  coinAmount: { type: Number }, 
</pre>

* code: response code
* transactionID: the assigned transaction ID from our system
* tradeID: the trade ID from the EA transfer market
* assetID: the ID of the player
* playerName: the name of the player  
* startPrice: bidding start price
* coinAmount: buy now price  

## Update Status
### POST /fbm-status
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  transactionID: { type: Number },
  status: { type: String }, 
  hash: { type: String }
}
</pre>

* user: your username in our system
* transactionID: the assigned transaction ID in our system
* status: ```bought``` or ```cancel``` 
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5(user.SECRET_WORD)

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
### POST /fbm-price
#### Request Body (JSON)

<pre>
{
  user: { type: String },
  platform: { type: String },
  hash: { type: String }
}
</pre>

* user: your username in our system
* platform: ```xbox``` or  ```ps4``` 
* hash: MD5 hash of the concatenated values + SECRET_WORD
  * md5( user.SECRET_WORD )

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