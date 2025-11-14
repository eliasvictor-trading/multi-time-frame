# multi-time-frame
Automated PineScript Indicators
# Multi-Time Frame (MTF) Checklist Dashboard (with Enhanced Filters)

A comprehensive multi-timeframe (MTF) analysis indicator for TradingView that provides confluence-based trading signals with advanced filtering capabilities.

## Features

- **Multi-Timeframe Analysis**: Monitors 6 configurable timeframes simultaneously (default: 1m, 5m, 15m, 30m, 1h, 4h)
- **ORB (Opening Range Breakout)**: Customizable opening range calculation with breakout detection
- **Confluence Scoring**: Requires alignment across multiple timeframes before signaling
- **Advanced Filters**:
  - Volume confirmation (above average volume requirement)
  - ATR volatility filter
  - Session-based trading hours (EST timezone)
  - Momentum confirmation
  - Daily range extremes blocker
  - Strong directional candle filter
- **Visual Dashboard**: Clean, color-coded table showing market conditions across all timeframes
- **Daily Levels Display**: Current day and previous day high/low prices
- **Arrow Signals**: Simple up/down arrows for long/short entries without chart clutter

## Installation

1. Open TradingView and navigate to the Pine Editor (bottom panel)
2. Click "Open" → "New indicator"
3. Delete the default code
4. Copy and paste the entire script from `mtf_checklist_dashboard.pine`
5. Click "Save" and name your indicator
6. Click "Add to Chart"

## Configuration

### Basic Settings
- **Timeframes**: Comma-separated list of timeframes to monitor (default: "1,5,15,30,60,240")
- **ORB Minutes**: Opening range period in minutes (default: 15)
- **Dashboard Position**: Choose from 9 positions (Top Right, Top Center, etc.)

### Confluence Filters
- **Minimum Timeframes Aligned**: How many timeframes must align for a signal (3-6, default: 5)
- **Require HTF Confirmation**: Forces higher timeframe (30m/1h/4h) alignment
- **Min Higher Timeframes**: Number of HTFs that must align (1-3, default: 2)

### Volume Filter
- **Volume Multiplier**: Requires volume to be X times the average (default: 1.5)
- **Volume Average Length**: Bars to calculate average volume (default: 20)

### Volatility Filter (ATR)
- **ATR Length**: Period for ATR calculation (default: 14)
- **Min ATR vs Average**: Minimum ATR compared to its average (default: 0.5)

### ORB Filters
- **Min Breakout % Beyond ORB**: How far price must break beyond ORB levels (default: 0.10%)

### Session Filter
- **Session 1 & 2**: Trading hour windows in EST (default: 0930-1130, 1400-1530)

### Momentum Filter
- **Lookback Bars**: Number of bars for momentum confirmation (default: 3)

### Daily Range Filter
- **Distance from High/Low %**: Blocks signals too close to daily extremes (default: 2%)

### Candle Filter
- **Min Candle Body %**: Requires strong directional candles (default: 60%)

## Dashboard Legend

### Columns
- **TF**: Timeframe
- **C**: Current candle (Green = bullish, Red = bearish)
- **P**: Previous candle
- **ORB**: Position relative to Opening Range (A = Above, B = Below, W = Within)
- **VWAP**: Price vs VWAP (A = Above, B = Below)
- **E200**: Price vs 200 EMA (A = Above, B = Below)
- **D Hi/Lo**: Near daily high or low
- **PD Hi/Lo**: Near previous day high or low
- **9 vs 21**: 9 EMA vs 21 EMA relationship (A = bullish, B = bearish)
- **9&21 v200**: Both EMAs vs 200 EMA (>> = both above, << = both below, <> = mixed)

### Summary Rows
- **ORB Range**: Displays the opening range high, low, and total range
- **Current Day**: Today's high and low prices
- **Previous Day**: Yesterday's high and low prices

## How It Works

The indicator analyzes multiple timeframes and checks each against several bullish/bearish criteria:
- Current candle direction
- Price position vs VWAP
- Price position vs 200 EMA
- EMA alignment (9 vs 21, both vs 200)
- ORB position

When a configurable number of timeframes align (default: 5 out of 6) and all enabled filters pass, the indicator generates a signal:
- **Green arrow below bar**: Long entry signal
- **Red arrow above bar**: Short entry signal
- **Optional background color**: Highlights the signal bar

**Multi-timeframe data requests**: The script uses request.security() to fetch data from multiple timeframes. TradingView limits the number of security calls, but with 6 default timeframes, the script operates well within platform limits.

## Alerts

The script includes four alert conditions:
- Long Entry Signal
- Short Entry Signal
- Long Exit Signal (when 3+ timeframes turn bearish)
- Short Exit Signal (when 3+ timeframes turn bullish)

Alert messages include ticker, action, price, and quantity in JSON format for automation compatibility.

**Alert format**: Alerts use JSON format optimized for webhook automation with third-party trading platforms.

## Requirements

- TradingView account (Free or Paid)
- Pine Script v6 compatible
- Works on all timeframes and symbols
- Best results on liquid markets during active trading hours


## Known Limitations

- Signals are based on historical confluence and may lag in fast-moving markets
- Requires sufficient historical data for accurate calculations
- Performance varies by market conditions and symbol liquidity
- Tick/Second-based charts: Fully supported. Please note that on TradingView that the session filter automatically uses 1-minute resolution for session detection when running on tick or second-based timeframes


## License

Mozilla Public License 2.0

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open an issue or submit a pull request.

## Disclaimer

This indicator is for educational purposes only. Trading involves risk. Always perform your own analysis and never risk more than you can afford to lose.

## Contact

eliasvictorllc@gmail.com

## Acknowledgments

Built using TradingView's Pine Script v6 language.
