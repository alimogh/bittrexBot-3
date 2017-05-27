# bittrexBot
This is an experimental bot for trading against the bittrex exchange

#DISCLAIMER

###I am not responsible for anything done with this bot. You use it at your own risk. There are no warranties or guarantees expressed or implied. You assume all responsibility and liability.


##Flow

The bot walks through the following:

* Checks for the existence of any orders in your orderbook. If both a buy and sell exist the flow ends and the bot will wait for the next cycle. 
* Checks for multiple orders. If there are, it will remove the last order(s)
* If either a buy or sell order are absent in your orderbook, the bot assumes your last order was within the bounds of the market and prepares to place a new buy/sell at the configured percentage above / below that order price
Example: if the last order in your orderbook was a sell for .0001000, the bot will prepare a new sell of .000104 (if 4% is configured) and a buy of .000096
* Assuming a new order set is needed, it will remove remaining orders for the token
* Place a new order set with the volume percentage configured

##Configuration

####Note: An api key will need to be created with "Trade Market" permissions

* apiKey - api key
* apiSecret - api key secret
* trade - the base token used for exchange
* currency - the token ticker to be traded
* valuePercent - the difference in the buy / sell price of the order placed
* volumePercent - how many tokens are traded during a transaction
* extCoinBalance - off exchange token count
* checkInterval - how often the bot will check for orders

####Example file 

```json
{
  "apiKey": "34234898u9rghk",
  "apiSecret": "238ryfiuahskuqh4ri",
  "trade": "BTC",
  "currency": "WAVES",
  "valuePercent": 4,
  "volumePercent": 3,
  "extCoinBalance": 0,
  "checkInterval": 30
}
```
__the config file MUST be named botConfig.json__

##Usage
The bot is designed to trade a single token at a time. It's recommended to run it in the docker container. 
The docker image can be found at __jufkes/bittrexBot__ (currently private until i get it ironed out...sorry)

To run:
docker run -d --name <name> -v /path/to/config/file:/opt/bittrexBot/config jufkes/bittrexbot:latest

