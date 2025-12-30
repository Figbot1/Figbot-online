# Figbot-Online: Democratic AI Trading System

<div align="center">

![Figbot-Online](https://img.shields.io/badge/Figbot--Online-AI%20Trading%20System-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)

A revolutionary democratic AI trading system powered by multiple machine learning models voting on asset price predictions across multiple timeframes.

[Features](#features) • [Architecture](#architecture) • [Installation](#installation) • [Usage](#usage) • [Configuration](#configuration)

</div>

---

## Overview

**Figbot-Online** is an innovative trading system that implements a "democratic" approach to AI-powered market predictions. Rather than relying on a single model or algorithm, Figbot-Online uses an ensemble of diverse machine learning models that collectively vote on price movements for various assets across different timeframes.

This approach reduces overfitting, improves prediction robustness, and provides a more balanced perspective on market movements by combining the strengths of multiple AI models with different architectures and training methodologies.

### Key Philosophy

> "Wisdom of the crowd" applied to machine learning. By aggregating predictions from multiple AI models with different perspectives on market data, we achieve more reliable and consistent trading signals.

---

## Features

### 🤖 Multiple AI Models
- **Ensemble Learning**: Combines predictions from diverse neural network architectures
- **Model Diversity**: LSTM, Transformer, GRU, and CNN-based models for different data perspectives
- **Continuous Learning**: Models are regularly retrained on new market data
- **Model Versioning**: Track and compare performance across model iterations

### 🗳️ Democratic Voting System
- **Consensus Mechanism**: Models vote on price direction predictions
- **Weighted Voting**: Model votes weighted by recent prediction accuracy
- **Confidence Scores**: Confidence levels attached to predictions for risk management
- **Customizable Thresholds**: Configure consensus requirements per strategy

### ⏱️ Multi-Timeframe Analysis
- **Multiple Timeframes**: Analyze assets across 5-minute, 15-minute, 1-hour, 4-hour, and daily intervals
- **Timeframe Consensus**: Vote aggregation across different timeframes
- **Hierarchical Decision Making**: Combine short-term and long-term signals
- **Timeframe Weighting**: Apply different weights to different timeframes

### 💱 Asset Coverage
- **Cryptocurrencies**: Full support for major crypto pairs (BTC, ETH, etc.)
- **Forex Pairs**: Support for major currency pairs
- **Stocks**: Integration with equity markets
- **Commodities**: Support for major commodity pairs
- **Extensible**: Easy to add new asset classes

### 📊 Advanced Features
- **Real-time Processing**: Live market data streaming and prediction
- **Backtesting Engine**: Historical performance validation
- **Risk Management**: Position sizing and stop-loss integration
- **Performance Metrics**: Detailed statistics and monitoring
- **API Interface**: RESTful API for integration with trading platforms
- **Dashboard**: Real-time visualization of predictions and voting results

---

## Architecture

### System Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Market Data Ingestion                    │
│          (WebSocket/REST APIs, Real-time feeds)             │
└────────────────────────────┬────────────────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  Data Pipeline  │
                    │  (Cleaning,     │
                    │  Validation)    │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ▼                    ▼                    ▼
   ┌──────────┐         ┌──────────┐        ┌──────────┐
   │  Model 1 │         │  Model 2 │        │  Model N │
   │  (LSTM)  │         │ (Trans.) │        │  (CNN)   │
   │          │         │          │        │          │
   └────┬─────┘         └────┬─────┘        └────┬─────┘
        │                    │                    │
        │  Prediction (Buy/  │  Prediction (Buy/ │ Prediction
        │  Sell/Hold, Conf)  │  Sell/Hold, Conf) │ (Buy/Sell/Hold)
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                    ┌────────▼──────────┐
                    │ Democratic Voting │
                    │ Engine            │
                    │ • Vote Tallying   │
                    │ • Consensus Check │
                    │ • Confidence Calc │
                    └────────┬──────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ▼                    ▼                    ▼
   ┌──────────┐         ┌──────────┐        ┌──────────┐
   │ Signal   │         │  Risk    │        │  Trade  │
   │Generator │         │ Manager  │        │Executor  │
   └────┬─────┘         └────┬─────┘        └────┬─────┘
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                    ┌────────▼──────────┐
                    │  Trading Action   │
                    │  (Market/Limit)   │
                    └────────┬──────────┘
                             │
                    ┌────────▼──────────┐
                    │  Performance      │
                    │  Monitoring &     │
                    │  Metrics          │
                    └───────────────────┘
```

### Component Description

#### 1. **Data Pipeline**
- Ingests real-time and historical market data from multiple sources
- Performs data cleaning, normalization, and validation
- Handles missing values and outliers
- Manages feature engineering for ML models

#### 2. **AI Models (Ensemble)**
Each model is independently trained and maintains its own:
- **Input Processing**: Standardized market data preparation
- **Prediction Layer**: Outputs price direction and confidence
- **Accuracy Tracking**: Recent performance metrics

**Model Types:**
- **LSTM Models**: Capture long-term dependencies in price data
- **Transformer Models**: Attention-based architecture for pattern recognition
- **GRU Models**: Lightweight recurrent architecture
- **CNN Models**: Detect local patterns and technical formations

#### 3. **Democratic Voting Engine**
Core component that aggregates model predictions:
- **Vote Collection**: Gathers predictions from all models
- **Weighting System**: Applies weights based on model accuracy
- **Consensus Threshold**: Determines required agreement level
- **Confidence Scoring**: Calculates overall prediction confidence
- **Conflict Resolution**: Handles split votes with fallback strategies

#### 4. **Signal Generation**
- Generates trading signals based on voting results
- Applies additional technical indicators for confirmation
- Filters low-confidence signals
- Attaches risk scores to signals

#### 5. **Risk Management**
- Calculates position sizes based on account risk
- Sets stop-loss and take-profit levels
- Manages portfolio exposure
- Monitors drawdown limits

#### 6. **Trade Execution**
- Executes trades based on generated signals
- Supports market and limit orders
- Handles order management and fulfillment
- Tracks order status

#### 7. **Performance Monitoring**
- Tracks prediction accuracy per model
- Monitors overall system performance
- Logs all decisions and outcomes
- Generates performance reports

---

## How It Works

### Step 1: Data Collection
```
Market Data → Multiple Feeds → Unified Data Stream
```
Real-time market data is collected from multiple sources and standardized into a unified format.

### Step 2: Feature Engineering
```
Raw Data → Technical Indicators → Model Features
```
Market data is transformed into features that AI models can understand:
- Price movements (returns, volatility)
- Technical indicators (RSI, MACD, Bollinger Bands, etc.)
- Volume metrics
- Market microstructure data

### Step 3: Individual Model Predictions
```
Features → Model 1 → Prediction 1 (Buy/Sell/Hold, Confidence: 0.85)
Features → Model 2 → Prediction 2 (Buy/Sell/Hold, Confidence: 0.72)
Features → Model 3 → Prediction 3 (Buy/Sell/Hold, Confidence: 0.91)
Features → Model N → Prediction N (Buy/Sell/Hold, Confidence: 0.68)
```

Each model independently predicts the likely price direction and confidence in its prediction.

### Step 4: Democratic Voting
```
Votes + Model Weights + Thresholds → Consensus Decision
```

**Example Vote Aggregation:**
```
Model 1 (Weight: 0.95): BUY   (Confidence: 0.85)
Model 2 (Weight: 0.78): HOLD  (Confidence: 0.72)
Model 3 (Weight: 0.91): BUY   (Confidence: 0.91)
Model 4 (Weight: 0.82): BUY   (Confidence: 0.68)
────────────────────────────────────
Consensus: BUY with 79% agreement
Final Confidence: 0.79
```

**Voting Rules:**
- Each model gets one vote
- Votes are weighted by recent model accuracy
- Consensus threshold must be met (default: 60% agreement)
- Final confidence = weighted average of model confidences
- If no consensus: signal is suppressed or marked as NEUTRAL

### Step 5: Signal Generation & Filtering
```
Consensus Decision → Technical Confirmation → Risk Check → Trading Signal
```

- Apply technical indicator confirmation filters
- Check risk management constraints
- Verify position sizing limits
- Generate final trading signal with metadata

### Step 6: Risk Management
```
Trading Signal → Position Sizing → Stop-Loss/Take-Profit → Order
```

- Calculate position size based on account risk and market volatility
- Determine stop-loss levels based on support/resistance
- Set take-profit targets based on risk-reward ratio
- Check portfolio exposure limits

### Step 7: Trade Execution & Monitoring
```
Order → Market Execution → Position Monitoring → Performance Tracking
```

- Execute trades via connected brokers
- Monitor open positions in real-time
- Update performance metrics
- Adjust positions based on market conditions

---

## Multi-Timeframe Voting Strategy

Figbot-Online uses a hierarchical timeframe approach:

### Timeframe Levels

```
5-Minute Frame    → Short-term momentum
15-Minute Frame   → Intraday trends
1-Hour Frame      → Short-term support/resistance
4-Hour Frame      → Medium-term direction
Daily Frame       → Long-term trend confirmation
```

### Multi-Timeframe Consensus

Each timeframe has its own model ensemble that votes on predictions. The system then aggregates across timeframes:

```
TF5m Consensus (Weight: 0.15)  → 75% BUY
TF15m Consensus (Weight: 0.20) → 70% BUY
TF1h Consensus (Weight: 0.25)  → 80% BUY
TF4h Consensus (Weight: 0.25)  → 65% BUY
TFDaily Consensus (Weight: 0.15) → 85% BUY
──────────────────────────────────
Final: 75% BUY across all timeframes
```

### Decision Logic
- **Alignment**: Signals aligned across timeframes = stronger confidence
- **Conflict**: Conflicting signals at different timeframes = caution or suppression
- **Weighted Aggregation**: Longer timeframes typically have higher weight
- **Timeframe Confirmation**: Short-term signals confirmed by longer-term trends

---

## Installation

### Prerequisites
- Python 3.8 or higher
- pip or conda package manager
- Git

### Quick Start

1. **Clone the Repository**
```bash
git clone https://github.com/Figbot1/figbot-online.git
cd figbot-online
```

2. **Create Virtual Environment**
```bash
# Using venv
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Or using conda
conda create -n figbot python=3.9
conda activate figbot
```

3. **Install Dependencies**
```bash
pip install -r requirements.txt
```

4. **Configure API Credentials**
```bash
cp config/config.example.yaml config/config.yaml
# Edit config.yaml with your API keys and settings
```

5. **Initialize Database**
```bash
python scripts/init_db.py
```

6. **Run the System**
```bash
python main.py
```

### Docker Installation (Optional)

```bash
docker build -t figbot-online .
docker run -it --name figbot \
  -v $(pwd)/config:/app/config \
  -v $(pwd)/data:/app/data \
  figbot-online
```

---

## Usage

### Basic Usage

```python
from figbot import DemocraticAITrader

# Initialize the trader
trader = DemocraticAITrader(config_file='config/config.yaml')

# Start the trading system
trader.start()

# The system will continuously:
# 1. Monitor market data
# 2. Generate predictions from all models
# 3. Aggregate votes
# 4. Execute trades based on consensus
# 5. Monitor performance
```

### Running Backtests

```python
from figbot.backtesting import BacktestEngine

# Initialize backtester
backtester = BacktestEngine(
    start_date='2024-01-01',
    end_date='2024-12-31',
    initial_capital=10000
)

# Run backtest
results = backtester.run(
    asset='BTC/USD',
    timeframes=['15m', '1h', '4h'],
    models=['lstm', 'transformer', 'gru'],
    voting_threshold=0.60
)

# Analyze results
print(results.summary())
print(f"Total Return: {results.total_return:.2%}")
print(f"Sharpe Ratio: {results.sharpe_ratio:.2f}")
print(f"Max Drawdown: {results.max_drawdown:.2%}")
print(f"Win Rate: {results.win_rate:.2%}")
```

### Monitoring Live Performance

```python
from figbot.monitoring import DashboardServer

# Start live dashboard
dashboard = DashboardServer(port=8080)
dashboard.start()

# Access dashboard at http://localhost:8080
# View:
# - Live predictions from each model
# - Voting results
# - Current positions
# - Performance metrics
# - Model accuracy trends
```

### API Endpoint Examples

```bash
# Get current predictions
curl http://localhost:8000/api/predictions/BTC-USD

# Get voting results
curl http://localhost:8000/api/voting/BTC-USD

# Get performance metrics
curl http://localhost:8000/api/metrics

# Submit manual trade signal
curl -X POST http://localhost:8000/api/trade \
  -H "Content-Type: application/json" \
  -d '{"asset": "BTC/USD", "action": "BUY", "size": 0.1}'
```

---

## Configuration

### Main Configuration File (`config/config.yaml`)

```yaml
# System Settings
system:
  log_level: INFO
  debug_mode: false
  backtesting_mode: false

# Data Sources
data_sources:
  primary: binance  # binance, coinbase, kraken, etc.
  secondary: 
    - coinbase
    - kraken
  update_frequency: 1s

# Model Configuration
models:
  ensemble:
    lstm:
      enabled: true
      lookback_period: 100
      units: 64
      dropout: 0.2
    transformer:
      enabled: true
      attention_heads: 4
      transformer_layers: 2
    gru:
      enabled: true
      lookback_period: 100
      units: 32
    cnn:
      enabled: true
      filters: 32
      kernel_size: 3

# Voting Configuration
voting:
  consensus_threshold: 0.60  # 60% agreement required
  weighting_method: accuracy  # accuracy, performance, equal
  confidence_calculation: weighted_average
  
# Timeframe Configuration
timeframes:
  enabled:
    - 5m
    - 15m
    - 1h
    - 4h
    - 1d
  weights:
    5m: 0.15
    15m: 0.20
    1h: 0.25
    4h: 0.25
    1d: 0.15

# Risk Management
risk_management:
  max_position_size: 0.1  # 10% of account per trade
  max_portfolio_exposure: 0.5  # 50% max
  stop_loss_percent: 2.0
  take_profit_ratio: 2.0  # 2:1 risk-reward
  max_daily_loss: 0.05  # 5% max daily loss

# Trading Settings
trading:
  order_type: limit  # limit or market
  order_timeout: 60  # seconds
  slippage_allowance: 0.1  # 0.1% max slippage
  
# API Settings
api:
  enabled: true
  host: 0.0.0.0
  port: 8000
  
# Dashboard Settings
dashboard:
  enabled: true
  port: 8080
  refresh_interval: 1000  # milliseconds

# Database
database:
  type: sqlite  # sqlite, postgresql, mongodb
  connection_string: "data/figbot.db"
  
# Notification Settings
notifications:
  email: false
  webhook: false
  slack: false
```

### Model-Specific Configuration

Each model can be fine-tuned with its own hyperparameters. See `config/models/` directory for detailed model configurations.

---

## Performance Monitoring

### Key Metrics Tracked

- **Prediction Accuracy**: Per-model and ensemble accuracy rates
- **Win Rate**: Percentage of profitable trades
- **Sharpe Ratio**: Risk-adjusted returns
- **Max Drawdown**: Largest peak-to-trough decline
- **Profit Factor**: Gross profit vs. gross loss ratio
- **Model Consensus**: How often models agree
- **Voting Distribution**: Distribution of model votes over time
- **Confidence Levels**: Average confidence of predictions

### Dashboard Features

The live dashboard provides real-time visualization of:
- Current model predictions for selected assets
- Voting results and consensus metrics
- Active positions and P&L
- Performance charts and statistics
- Model accuracy trends
- Risk metrics and exposure

---

## Development & Contributing

### Project Structure

```
figbot-online/
├── config/
│   ├── config.example.yaml
│   └── models/
├── src/
│   ├── models/
│   │   ├── lstm.py
│   │   ├── transformer.py
│   │   ├── gru.py
│   │   └── cnn.py
│   ├── voting/
│   │   ├── voter.py
│   │   └── consensus.py
│   ├── data/
│   │   ├── pipeline.py
│   │   └── sources.py
│   ├── trading/
│   │   ├── executor.py
│   │   └── risk_manager.py
│   └── monitoring/
│       ├── dashboard.py
│       └── metrics.py
├── scripts/
│   ├── init_db.py
│   ├── train_models.py
│   └── backtest.py
├── tests/
├── main.py
├── requirements.txt
└── README.md
```

### Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Standards

- Follow PEP 8 style guidelines
- Add unit tests for new features
- Update documentation
- Ensure all tests pass: `pytest tests/`

### Model Development

To add a new model to the ensemble:

1. Create new model file in `src/models/`
2. Inherit from `BaseModel` class
3. Implement `predict()` method
4. Add model to ensemble in `config.yaml`
5. Write unit tests
6. Document the model architecture

---

## Roadmap

- [x] Multi-model ensemble architecture
- [x] Democratic voting system
- [x] Multi-timeframe analysis
- [x] Basic backtesting engine
- [ ] Advanced risk management features
- [ ] Portfolio optimization
- [ ] Reinforcement learning models
- [ ] Real-time sentiment analysis integration
- [ ] Cryptocurrency futures trading
- [ ] Options trading support
- [ ] Machine learning pipeline optimization
- [ ] Advanced feature engineering
- [ ] Multi-asset portfolio management
- [ ] Cloud deployment templates (AWS, GCP, Azure)
- [ ] Mobile app interface

---

## Troubleshooting

### Common Issues

**Issue: Models not making predictions**
- Check data connection status
- Verify model files are loaded correctly
- Check logs for model errors

**Issue: Low consensus/predictions suppressed**
- Adjust consensus threshold in config
- Check if models are trained on recent data
- Verify feature engineering pipeline

**Issue: High slippage on orders**
- Use limit orders instead of market orders
- Adjust slippage_allowance setting
- Check market liquidity

**Issue: Out of memory errors**
- Reduce lookback period for models
- Decrease batch size in config
- Monitor memory usage

---

## FAQ

**Q: How often are models retrained?**
A: Models are automatically retrained daily by default, with weekly full retraining. This can be configured in settings.

**Q: What's the minimum capital needed?**
A: This depends on the asset and broker, but generally $1,000-$10,000 is recommended to properly manage risk.

**Q: Can I use this for live trading?**
A: Yes, but always start with paper trading first to validate the system with your specific configuration and market conditions.

**Q: How do I add new AI models?**
A: See the development section for detailed instructions on extending the model ensemble.

**Q: What exchanges are supported?**
A: Currently supports Binance, Coinbase, Kraken, and others via CCXT. Adding new exchanges is straightforward.

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## Support & Community

- 📧 Email: support@figbot-online.com
- 💬 Discord: [Join our community](https://discord.gg/figbot)
- 📚 Documentation: [Full docs](https://docs.figbot-online.com)
- 🐛 Issues: [GitHub Issues](https://github.com/Figbot1/figbot-online/issues)

---

## Disclaimer

**Risk Warning**: Trading financial instruments carries substantial risk of loss. The use of Figbot-Online for automated trading does not guarantee profits and could result in significant losses. Past performance does not indicate future results.

Always:
- Use appropriate risk management
- Start with paper trading
- Never trade with money you can't afford to lose
- Conduct thorough backtesting
- Monitor the system regularly

By using Figbot-Online, you acknowledge and accept all risks involved in algorithmic trading.

---

<div align="center">

**Built with ❤️ by the Figbot Team**

[⬆ back to top](#figbot-online-democratic-ai-trading-system)

</div>
