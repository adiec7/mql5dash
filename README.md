# Hon-APS Dashboard - Professional Trading Interface

A comprehensive, real-time trading dashboard for MetaTrader 5 that provides advanced market analysis, risk management, and automated pattern system monitoring.

![Version](https://img.shields.io/badge/version-1.3.0-blue.svg)
![Platform](https://img.shields.io/badge/platform-MetaTrader%205-green.svg)
![Language](https://img.shields.io/badge/language-MQL5-orange.svg)

## 🚀 Features

### 📊 **Real-time Monitoring**
- **Account Information**: Balance, equity, margin levels, and P&L tracking
- **Trading Status**: Active positions, lot sizes, market regime analysis
- **News Integration**: Economic calendar with impact assessment
- **Market Analysis**: Volatility, trend strength, and pattern recognition

### 📈 **Advanced Analytics**
- **Depth of Market (DOM)**: Live order book visualization
- **Performance Metrics**: Win rate, profit factor, Sharpe ratio
- **Risk Management**: Adaptive risk controls and drawdown monitoring
- **KAMA Trend Analysis**: Kaufman Adaptive Moving Average signals

### 🎯 **Professional Interface**
- **Modern Dark Theme**: Professional color scheme with gradient effects
- **Responsive Layout**: Organized card-based design
- **Interactive Controls**: One-click pause, emergency stop, and optimisation
- **Visual Indicators**: Colour-coded status lights and progress bars

### ⚡ **Smart Controls**
- Emergency stop functionality
- Automated pause/resume trading
- Risk parameter reset
- News trading toggle
- Real-time statistics display

## 🛠 Installation

1. **Download the file**: Save `Hon-APS-Dashboard-COMPLETE-BEAUTIFUL.mqh` to your MetaTrader 5 installation directory:
   ```
   MetaTrader 5/MQL5/Include/
   ```

2. **Include in your EA**: Add this line to your Expert Advisor:
   ```mql5
   #include <Hon-APS-Dashboard-COMPLETE-BEAUTIFUL.mqh>
   ```

3. **Initialize in your EA**:
   ```mql5
   BeautifulDashboard dashboard;
   
   int OnInit()
   {
       dashboard.Init(MagicNumber, 15, 15); // x_offset, y_offset
       return INIT_SUCCEEDED;
   }
   ```

## 💻 Usage

### Basic Implementation

```mql5
#include <Hon-APS-Dashboard-COMPLETE-BEAUTIFUL.mqh>

BeautifulDashboard g_dashboard;

int OnInit()
{
    //Initialise dashboard with magic number and position
    if(!g_dashboard.Init(12345, 20, 20))
    {
        Print("Failed to initialize dashboard");
        return INIT_FAILED;
    }
    return INIT_SUCCEEDED;
}

void OnTick()
{
    // Prepare dashboard data
    DashboardData data;
    
    // Fill account information
    data.balance = AccountInfoDouble(ACCOUNT_BALANCE);
    data.equity = AccountInfoDouble(ACCOUNT_EQUITY);
    data.free_margin = AccountInfoDouble(ACCOUNT_MARGIN_FREE);
    data.floating_pl = AccountInfoDouble(ACCOUNT_PROFIT);
    
    // Fill trading status
    data.symbol = Symbol();
    data.is_trading_allowed = TerminalInfoInteger(TERMINAL_TRADE_ALLOWED);
    data.open_positions = PositionsTotal();
    
    // Update dashboard
    g_dashboard.Update(data);
}

void OnChartEvent(const int id, const long& lparam, const double& dparam, const string& sparam)
{
    if(id == CHARTEVENT_OBJECT_CLICK)
    {
        ENUM_DASHBOARD_ACTION action = g_dashboard.EventAction(sparam);
        
        switch(action)
        {
            case DASH_ACTION_PAUSE_TOGGLE:
                // Handle pause/resume logic
                break;
            case DASH_ACTION_CLOSE_ALL:
                // Close all positions
                break;
            case DASH_ACTION_EMERGENCY_STOP:
                // Emergency stop protocol
                break;
        }
    }
}

void OnDeinit(const int reason)
{
    g_dashboard.Deinit();
}
```

## 📋 Data Structure

The dashboard uses a comprehensive `DashboardData` structure:

```mql5
struct DashboardData
{
    // EA Status
    bool   is_trading_allowed;
    bool   is_paused;
    string symbol;
    bool   is_emergency_stop;
    
    // Account Information
    double balance;
    double equity;
    double free_margin;
    double floating_pl;
    
    // Market Analysis
    string market_regime;
    string kama_trend;
    double volatility_level;
    double trend_strength;
    
    // Performance Metrics
    double win_rate;
    double profit_factor;
    int    total_trades;
    double sharpe_ratio;
    
    // Risk Management
    double daily_loss_pct;
    double max_daily_loss_pct;
    double current_drawdown;
    
    // News Trading
    bool   news_trading_active;
    string next_news_currency;
    int    minutes_to_news;
    
    // DOM Data
    MqlBookInfo dom_book[];
};
```

## 🎮 Available Actions

The dashboard supports these interactive actions:

- `DASH_ACTION_PAUSE_TOGGLE` - Pause/Resume trading
- `DASH_ACTION_CLOSE_ALL` - Close all open positions
- `DASH_ACTION_EMERGENCY_STOP` - Emergency halt
- `DASH_ACTION_RESET_RISK` - Reset risk parameters
- `DASH_ACTION_SHOW_STATS` - Display statistics
- `DASH_ACTION_NEWS_TOGGLE` - Toggle news trading
- `DASH_ACTION_MINIMIZE` - Minimize/Show dashboard

## 🎨 Customization

### Color Themes
The dashboard uses a professional dark theme with customizable colors:
- Main background: Deep dark blue
- Accent colors: Bright blue, green (success), red (danger), orange (warning)
- Text: Light gray hierarchy for optimal readability

### Layout Configuration
- **Position**: Adjustable X/Y offsets
- **Size**: 760x430 pixels (optimized for 1920x1080+ displays)
- **Update Interval**: Configurable refresh rate (default: 3 seconds)

## 📊 Dashboard Sections

1. **Header**: System status and window controls
2. **Account Card**: Balance, equity, margin information
3. **Trading Card**: Position status and market regime
4. **News Card**: Economic calendar integration
5. **Market Analysis**: Volatility and trend data
6. **DOM Card**: Depth of market visualization
7. **Performance Card**: Trading statistics
8. **Risk Controls**: Comprehensive risk monitoring
9. **Action Buttons**: Quick trading controls

## ⚙️ Requirements

- **Platform**: MetaTrader 5 (Build 3000+)
- **Language**: MQL5
- **Display**: Minimum 1366x768 resolution
- **Permissions**: Allow DLL imports and live trading

## 🤝 Contributing

This is a professional trading tool. For improvements or customisations:

1. Fork the repository
2. Create a feature branch
3. Test thoroughly in demo environment
4. Submit a pull request

## ⚠️ Disclaimer

This dashboard is a monitoring and control interface for automated trading systems. Trading involves substantial risk of loss. Use only with proper risk management and in demo environments first.

## 📝 License

Copyright 2025, KSQUANTITATIVE  
Website: [www.ksquants.com](https://www.ksquants.com)

---

**Built for professional traders who demand precision, performance, and visual excellence.**
```
