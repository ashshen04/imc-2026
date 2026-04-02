# IMC Prosperity 4 — Trading Bot

Algorithmic trading strategies for [IMC Prosperity 4](https://prosperity.imc.com/), a simulated market competition running **April 14–30, 2026**.

- **Format**: 5 rounds (Round 0 is tutorial/practice)
- **Each round**: 1 algorithmic challenge + 1 manual challenge
- **Currency**: SeaShells (virtual)
- **Prize pool**: $50,000 USD

## Structure

```
imc-2026/
├── trader.py          # Main submission file (Trader class)
├── datamodel.py       # Provided datamodel (TradingState, Order, etc.)
├── backtest/          # Backtesting utilities and historical data
└── strategies/        # Strategy modules per product
```

## Trader API

Your submission must define a `Trader` class with a single `run` method:

```python
from datamodel import Order, TradingState

class Trader:
    def run(self, state: TradingState) -> dict[str, list[Order]]:
        result = {}
        # your logic here
        return result
```

`run()` is called every iteration. It receives the current `TradingState` and must return a dict mapping product symbols to a list of `Order`s.

### Key data model fields

| Object | Fields |
|---|---|
| `TradingState` | `timestamp`, `listings`, `order_depths`, `own_trades`, `market_trades`, `position`, `observations` |
| `OrderDepth` | `buy_orders: Dict[price, qty]`, `sell_orders: Dict[price, qty]` |
| `Order(symbol, price, qty)` | `qty > 0` = buy, `qty < 0` = sell |
| `Trade` | `symbol`, `price`, `quantity`, `buyer`, `seller`, `timestamp` |

### Position limits

Each product has a hard position limit (e.g. ±20). If any submitted order would breach the limit when fully filled, **all orders for that product are cancelled for that iteration**.

## Products by Round

| Round | Products |
|---|---|
| 0 (Tutorial) | RAINFOREST_RESIN, KELP, SQUID_INK |
| 1–4 | Revealed at round start |

## Resources

- [Prosperity 4 Wiki](https://imc-prosperity.notion.site/prosperity-4-wiki)
- [Tutorial Round Simulator / Practice](https://imc-prosperity.notion.site/tutorial-round-simulator-practice)
- [Official site](https://prosperity.imc.com/)
