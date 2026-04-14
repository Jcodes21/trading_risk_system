A java springboot backend system that presents market data, allows users to book trades, which updates user's position, evaluates users risk exposure , recalculates p and l. Backend Testing done using something like postman. Front end UI layer added later.

## App flow
Trade → Position → Risk → P&L

## Repo:
trade-risk-system

## Tech stack/Dependencies
Backend: Java Spring Boot
Database: Postgresql
ORM: JPA with hibernate

## Endpoints/File system
View / Screen
Endpoint
Backend package / class responsible

Market View
GET /marketdata
marketdata/MarketDataController → MarketDataService

Instrument Detail View
GET /marketdata/{instrument}
marketdata/MarketDataController → MarketDataService

Trade Entry View
POST /trades
trade/TradeController → TradeService → TradeRepository

Trades List View
GET /trades
trade/TradeController → TradeService → TradeRepository

Trade Detail View
GET /trades/{id}
trade/TradeController → TradeService → TradeRepository

Cancel Trade Action
DELETE /trades/{id}
trade/TradeController → TradeService → TradeRepository

Positions View
GET /positions
position/PositionController → PositionService

Instrument Position View
GET /positions/{instrument}
position/PositionController → PositionService

Risk Overview View
GET /risk
risk/RiskController → RiskService

User Risk View
GET /risk/{userId}
risk/RiskController → RiskService

Set Risk Limit View/Admin Action
POST /risk/limits
risk/RiskController → RiskService → RiskLimitRepository

Risk Breaches View
GET /risk/breaches
risk/RiskController → RiskService

P&L Overview View
GET /pnl
pnl/PnLController → PnLService

User P&L View
GET /pnl/{userId}
pnl/PnLController → PnLService

Instrument P&L View
GET /pnl/instrument/{instrument}
pnl/PnLController → PnLService

Users View
GET /users
user/UserController → UserService → UserRepository

User Detail View
GET /users/{id}
user/UserController → UserService → UserRepository

Create User View/Admin Action
POST /users
user/UserController → UserService → UserRepository

Your core first version should just be:
View / Screen
Endpoint
Backend package / class responsible

Market View
GET /marketdata
marketdata/MarketDataController → MarketDataService

Trade Entry View
POST /trades
trade/TradeController → TradeService → TradeRepository

Trades List View
GET /trades
trade/TradeController → TradeService → TradeRepository

Positions View
GET /positions
position/PositionController → PositionService

Risk Overview View
GET /risk
risk/RiskController → RiskService

P&L Overview View
GET /pnl
pnl/PnLController → PnLService

And the simple request flow is:
View
→ Controller
→ Service
→ Repository/DB
→ Response back

Example:
Trade Entry View
→ POST /trades
→ TradeController
→ TradeService
→ TradeRepository
→ database save
→ response returned

## Database
MVP*Market data will be hard coded initially

Instrument table
Id
Symbol
String Name
Type
Exchange
Currency
Created at

Trade table
id - PK
instrument id
side = BUY or SELL
Price
quantity
timestamp
userid - FK user table

Risk limit table
id unique
Userid FK user table
Instrument id FK instrument table
Max exposure
Created at

user table
id - PK
Name
email
password
organisationid - FK organization table
role
Created at timestamp

Organisation table
Organisation id - PK
Created at
