# ORB Pro - Opening Range Breakout Strategy

A professional-grade Opening Range Breakout (ORB) strategy implemented in PineScript v5 for TradingView.

## Features

### Core Strategy
- **Opening Range Detection**: 9:30-9:45 AM ET opening range capture
- **Breakout Confirmation**: Multiple confirmation filters for high-probability entries
- **Risk Management**: Comprehensive position sizing, stops, and targets

### Entry Filters
- VWAP confirmation (optional)
- EMA trend alignment (34-period default)
- Higher timeframe trend filter (30-min default)
- Second candle confirmation
- ATR-based volatility filters (0.5x - 1.5x range)
- VWAP slope filter (anti-chop)
- Inside day detection

### Exit Strategy
- **Partial Profit Taking**: 50% at 1R by default
- **Trailing Stops**: ATR-based trailing for runners (1.5x ATR)
- **Breakeven Management**: Automatic BE trigger at 75% of OR width
- **VWAP Invalidation**: Exit on VWAP cross
- **End of Day Exit**: Flatten all positions at 4 PM ET

### Risk Controls
- Minimum OR width validation (5 ticks)
- Maximum OR width filter
- Max loss per trade override
- Configurable stop loss (50% of OR default)
- Take profit targets (100% of OR default)

## Files

- `ORB_Pro_Fixed.pine` - Latest working version with bug fixes
- `ORB_Pro.pine` - Original version

## Configuration

### Recommended Settings for ES/NQ
- **Timeframe**: 5-minute chart
- **Opening Range**: 9:30-9:45 AM ET
- **Trading Sessions**: 9:30 AM - 11:45 AM ET
- **HTF Filter**: 30-minute EMA(100)
- **TP**: 100% of OR width
- **SL**: 50% of OR width

### Key Input Groups
1. **Opening Range & Sessions** - Define OR window and trading hours
2. **Confirmations** - VWAP, EMA, buffer, second candle
3. **HTF Trend Filter** - Higher timeframe alignment
4. **ATR / Volatility Filters** - Dynamic range validation
5. **Stops / Targets / Partials** - Exit management
6. **Breakeven / Risk Caps** - Risk control parameters

## Installation

1. Open TradingView
2. Create new Pine Script indicator
3. Copy contents of `ORB_Pro_Fixed.pine`
4. Click "Add to Chart"
5. Configure settings as needed

## Performance Notes

### Strengths
- Works well in trending markets with clear direction
- Strong risk/reward with partial profit taking
- Adaptive to different volatility conditions

### Limitations
- May produce false signals in choppy/ranging markets
- Requires sufficient OR width for valid signals
- HTF bar detection may have 1-bar lag on timeframe boundaries
- VWAP invalidation closes entire position (partials not preserved)

## Version History

### v2 (ORB_Pro_Fixed.pine)
- Fixed HTF bar closed detection logic
- Improved trailing stop implementation using `trail_points`
- Added minimum OR width validation (5 ticks)
- Enhanced second candle confirmation logic
- Consolidated request.security() calls for efficiency
- Better backtest range handling

### v1 (ORB_Pro.pine)
- Initial implementation
- Core ORB strategy with basic filters

## Trading Instruments

Optimized for:
- ES (S&P 500 E-mini)
- NQ (NASDAQ 100 E-mini)
- YM (Dow Jones E-mini)
- RTY (Russell 2000 E-mini)

Can be adapted for other liquid futures contracts.

## Alerts

Webhook-compatible alerts included for automation:
- Entry signals (long/short)
- TP1 fills
- Runner stop fills
- VWAP invalidation
- Breakeven triggers
- End of day exits

Alert messages include unique ID: `TV_N8N_2f6e9b3c`

## Known Issues

1. Trailing stop uses `trail_points` - behavior is consistent in backtest and real-time
2. HTF bar closed detection tracks time changes - may have 1-bar lag on timeframe boundaries
3. Second candle confirmation requires 2+ bars of history - no signals on first 2 bars
4. VWAP invalidation closes entire position - partials not preserved
5. Max loss override adjusts SL but doesn't reduce position size
6. Minimum OR width set to 5 ticks - adjust `MIN_OR_WIDTH_TICKS` constant if needed

## Support

For issues or questions about this strategy, please open an issue in this repository.

## License

This strategy is provided as-is for educational and trading purposes.

## Disclaimer

Trading futures and derivatives involves substantial risk of loss. This strategy is provided for educational purposes only. Past performance is not indicative of future results. Always test thoroughly on paper trading before risking real capital.

---

**Last Updated**: December 5, 2025
