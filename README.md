# 🧪 cq-backtester
### Vectorized Backtesting Engine for Crypto Trading  
Part of the **CryptoQuantAI** Ecosystem

`cq-backtester` provides a fast, flexible, and production-ready **vectorized backtesting engine** designed for  
algorithmic crypto trading, quantitative research, and AI/ML-based strategy evaluation.

It integrates seamlessly with:
- cq-ohlcv (market data)
- cq-indicators (technical indicators)
- cq-trader (live execution)
- cq-aimodels (AI prediction models)

---

## 🚀 Features

- ✅ Vectorized backtesting (no slow loops)  
- ✅ Built-in position management (long, short, flat)  
- ✅ Leverage support (1x → 100x)  
- ✅ Stop loss / take profit / trailing stop  
- ✅ Fees, slippage, maker/taker models  
- ✅ Trade log export (CSV/JSON)  
- ✅ Equity curve, drawdown, PnL metrics  
- ✅ Strategy class for reusable strategies  
- ✅ Compatible with pandas, polars, cudf  

---

## 📦 Installation

```bash
pip install cq-backtester
```

---

## 💡 Quick Start

```python
from cq_backtester import Backtester
from cq_ohlcv import OHLCV

df = OHLCV("BTCUSDT", "5m").load()

bt = Backtester(df, initial_balance=10000, leverage=5)

# Example strategy: EMA cross
bt.ema_cross(fast=9, slow=21)

results = bt.run()

print(results.summary())
```

---

## ✅ Strategy Class Example

```python
from cq_backtester import Strategy

class EMACross(Strategy):
    def generate_signals(self, df):
        df['ema_fast'] = df.close.ewm(span=9).mean()
        df['ema_slow'] = df.close.ewm(span=21).mean()
        df['signal'] = (df.ema_fast > df.ema_slow).astype(int)
        return df
```

Run:

```python
bt = Backtester(df, strategy=EMACross())
results = bt.run()
```

---

## 📊 Metrics Provided

- Total Return  
- Win Rate  
- Max Drawdown  
- Sharpe Ratio  
- Sortino Ratio  
- Equity Curve  
- Trade Count  
- Avg Win / Avg Loss  
- Profit Factor  

---

## 📁 Folder Structure

```
cq-backtester/
│
├── cq_backtester/
│   ├── __init__.py
│   ├── backtester.py
│   ├── strategy.py
│   ├── metrics.py
│   ├── trade_log.py
│   │
│   ├── utils/
│   │   ├── math.py
│   │   ├── performance.py
│   │   ├── position.py
│   │   ├── fees.py
│
├── tests/
├── examples/
└── README.md
```

---

## 📅 Roadmap

- ✅ Add vectorized trailing-stop  
- ✅ Full futures support  
- ⏳ Portfolio-level backtesting  
- ⏳ Walk-forward optimization  
- ⏳ Genetic strategy search  

---

## 🤝 Contributing

Guidelines:
- Use type hints  
- Format with Black  
- Add unit tests  
- Keep strategies simple & modular  

---

## ⚖️ License

MIT License

---

## 👨‍💻 Maintained By

CryptoQuantAI Development Team
