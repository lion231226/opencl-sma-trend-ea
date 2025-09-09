---
created: 2025-09-08T23:27:41Z
last_updated: 2025-09-08T23:27:41Z
version: 1.0
author: Claude Code PM System
---

# Technical Context

## Technology Stack

### Primary Technology
- **Language**: MQL5 (MetaQuotes Language 5)
- **Platform**: MetaTrader 5 Trading Platform
- **Version**: MQL5 build 3000+ (current version)
- **Execution Environment**: MetaTrader 5 Terminal

### Development Environment
- **IDE**: MetaEditor (built-in with MetaTrader 5)
- **Compiler**: MQL5 Compiler (built-in)
- **Debugger**: MetaEditor Debugger
- **Profiler**: Strategy Tester with optimization

### Standard Library
- **MQL5 Standard Library**: Full framework included with MetaTrader 5
- **Location**: `D:\MetaTrader 5\MQL5\Include\`
- **Version**: Latest stable release with MetaTrader 5

## Dependencies

### Core Dependencies
- **Expert Framework**: `<Expert\Expert.mqh>` - Main EA base class
- **Signal Classes**: `<Expert\Signal\SignalMA.mqh>` - Moving average signals
- **Trade Operations**: `<Trade\Trade.mqh>` - Standardized trading interface
- **Math Utilities**: `<Math\Math.mqh>` - Mathematical functions
- **String Utilities**: `<Strings\String.mqh>` - String operations

### External Dependencies
- **MetaTrader 5 Terminal**: Required for execution
- **Market Data Feed**: Required for trading operations
- **Broker Connection**: Required for live trading

### Build Dependencies
- **MQL5 Compiler**: Built into MetaEditor
- **MetaEditor**: Included with MetaTrader 5
- **No external build tools required**

## Development Tools

### Primary Tools
- **MetaEditor**: Integrated development environment
  - Syntax highlighting
  - Code completion
  - Built-in debugger
  - Strategy Tester integration
  - Profiling tools

### Testing Tools
- **Strategy Tester**: Backtesting and optimization
  - Historical data testing
  - Genetic optimization
  - Visual testing mode
  - Forward testing capabilities

### Version Control
- **Git**: Distributed version control system
- **GitHub CLI**: Command-line interface for GitHub operations
- **Remote Repository**: https://forge.mql5.io/Lion1226/mql5.git

## Configuration

### Environment Configuration
- **MetaTrader 5 Path**: `D:\MetaTrader 5\`
- **MQL5 Data Path**: `D:\MetaTrader 5\MQL5\`
- **Include Path**: `D:\MetaTrader 5\MQL5\Include\`
- **Experts Path**: `D:\MetaTrader 5\MQL5\Experts\`

### Compiler Settings
- **Optimization Level**: Standard optimization
- **Debug Information**: Available for debugging
- **Warning Level**: High warnings enabled
- **Strict Mode**: Enabled for type safety

### Runtime Configuration
- **Timeframe**: Multiple timeframes supported
- **Symbols**: All available trading instruments
- **Account Types**: Hedging and Netting accounts
- **Execution Types**: Instant, Market, Exchange execution

## Key Libraries and Frameworks

### Expert Framework
- **CExpert**: Base class for Expert Advisors
- **CExpertSignal**: Base class for signal generation
- **CExpertTrade**: Trading operations management
- **CExpertMoney**: Money management strategies
- **CExpertTrailing**: Trailing stop implementations

### Trading Framework
- **CTrade**: Standardized trading interface
- **CSymbolInfo**: Symbol information management
- **CAccountInfo**: Account information access
- **COrderInfo**: Order information management
- **CPositionInfo**: Position information management

### Signal Framework
- **CSignalMA**: Moving average signals
- **CSignalCCI**: Commodity Channel Index signals
- **CSignalRSI**: Relative Strength Index signals
- **CSignalMACD**: MACD signals
- **Custom Signal Classes**: Extensible framework

### Indicator Framework
- **CiMA**: Moving average indicator
- **CiRSI**: RSI indicator
- **CiMACD**: MACD indicator
- **Custom Indicators**: Support for custom indicators

## Data Sources

### Market Data
- **Real-time Data**: Live market data feed
- **Historical Data**: Historical price data for backtesting
- **Tick Data**: High-resolution tick data available
- **Timeframes**: M1 to MN1 timeframes supported

### Account Data
- **Account Information**: Balance, equity, margin, etc.
- **Position Data**: Current positions and their status
- **Order Data**: Pending orders and their status
- **History Data**: Closed positions and order history

### External Data
- **Economic Calendar**: Built-in economic calendar
- **News Feed**: Financial news integration
- **Custom Data**: External file support for custom data

## Performance Considerations

### Execution Speed
- **Tick Processing**: Real-time tick processing
- **Indicator Calculations**: Optimized indicator calculations
- **Memory Management**: Efficient memory usage patterns
- **CPU Usage**: Minimal CPU impact during normal operation

### Memory Management
- **Automatic Memory**: MQL5 handles most memory management
- **Object Cleanup**: Automatic object destruction
- **String Management**: Efficient string handling
- **Array Management**: Dynamic array support

### Network Considerations
- **Latency**: Network latency affects order execution
- **Connection Stability**: Reliable connection required
- **Data Flow**: Continuous market data stream
- **Order Execution**: Fast execution critical for trading

## Security Considerations

### Code Security
- **Compilation**: Source code compiled to .ex5 format
- **Obfuscation**: Compiled code is not easily readable
- **Protection**: No direct access to source code in production

### Trading Security
- **Risk Management**: Built-in risk controls
- **Order Validation**: Order validation before execution
- **Account Protection**: Account-level protection mechanisms
- **Margin Requirements**: Strict margin requirements enforced

### Data Security
- **Local Storage**: All data stored locally
- **Encryption**: Secure communication with broker
- **Authentication**: Broker authentication required
- **Authorization**: Proper authorization for trading operations

## Monitoring and Logging

### Built-in Monitoring
- **Expert Advisors Tab**: Real-time EA monitoring
- **Journal Tab**: Detailed operation logs
- **Strategy Tester**: Performance monitoring
- **Account History**: Trading history tracking

### Custom Logging
- **Print() Function**: Console output logging
- **Comment() Function**: Chart comment display
- **File Operations**: Custom log file creation
- **Email Notifications**: Email alert capabilities

### Error Handling
- **GetLastError()**: Error code retrieval
- **Error Codes**: Comprehensive error code system
- **Recovery Mechanisms**: Automatic recovery from errors
- **User Notifications**: Error notification system

## Integration Capabilities

### Broker Integration
- **MT5 Protocol**: Native MetaTrader 5 protocol
- **FIX Protocol**: Some brokers support FIX protocol
- **API Integration**: Custom API support through DLL imports
- **Web Services**: Limited web service integration

### Third-party Tools
- **DLL Import**: Native DLL import capabilities
- **Web Requests**: HTTP/HTTPS request support
- **Database Integration**: SQLite support built-in
- **File Operations**: Extensive file system access

### External Systems
- **Economic Data**: Economic calendar integration
- **News Services**: Financial news integration
- **Signal Services**: Copy trading capabilities
- **Analytics**: Performance analytics integration