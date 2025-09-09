---
created: 2025-09-08T23:27:41Z
last_updated: 2025-09-08T23:27:41Z
version: 1.0
author: Claude Code PM System
---

# System Patterns

## Architectural Patterns

### Expert Advisor Framework Pattern
The project follows the MQL5 Standard Library Expert Advisor framework pattern:

```cpp
// Base class inheritance pattern
class CSMATrendStrategy : public CExpert
{
private:
  // Signal management
  CSignalMA *m_signal;
  CExpertTrade *m_trade;
  
protected:
  // Lifecycle methods
  virtual bool Init();
  virtual void Deinit();
  virtual bool Processing();
  
public:
  // Constructor and destructor
  CSMATrendStrategy();
  ~CSMATrendStrategy();
};
```

**Key Characteristics**:
- Inheritance from CExpert base class
- Standard lifecycle methods (Init, Deinit, Processing)
- Composition pattern for signal and trade management
- Event-driven architecture through MetaTrader callbacks

### Signal Processing Pattern
Signal generation follows the observer pattern with indicator-based signals:

```cpp
// Signal processing pattern
class CCustomSignal : public CExpertSignal
{
private:
  CiMA *m_ma_fast;
  CiMA *m_ma_slow;
  
protected:
  virtual bool Validation();
  virtual bool CheckOpenLong();
  virtual bool CheckOpenShort();
  virtual bool CheckClose();
  
public:
  bool InitIndicators();
};
```

**Key Characteristics**:
- Signal classes inherit from CExpertSignal
- Indicator composition for signal generation
- Validation and check methods for decision making
- Separation of signal logic from trading logic

### Trading Operations Pattern
Trading operations use the command pattern with standardized execution:

```cpp
// Trading operations pattern
class CCustomTrade : public CExpertTrade
{
public:
  bool OpenPosition(ENUM_ORDER_TYPE type, double volume, double price, double sl, double tp);
  bool ClosePosition(ulong ticket);
  bool ModifyPosition(ulong ticket, double sl, double tp);
  
protected:
  virtual bool OrderValidate(const double volume);
  virtual double CorrectStopLoss(const double sl);
  virtual double CorrectTakeProfit(const double tp);
};
```

**Key Characteristics**:
- Standardized trading interface through CExpertTrade
- Command pattern for order operations
- Validation and correction methods for safety
- Error handling and logging integration

## Design Patterns

### Strategy Pattern
Signal generation uses the strategy pattern for different trading strategies:

```cpp
// Strategy pattern for signals
class CSignalStrategy
{
private:
  CExpertSignal *m_current_strategy;
  
public:
  void SetStrategy(CExpertSignal *strategy);
  bool CheckSignal();
  double GetSignalStrength();
};
```

### Factory Pattern
Indicator creation uses factory pattern for type safety:

```cpp
// Factory pattern for indicators
class CIndicatorFactory
{
public:
  static CiMA *CreateMA(string symbol, ENUM_TIMEFRAMES period, int ma_period);
  static CiRSI *CreateRSI(string symbol, ENUM_TIMEFRAMES period, int rsi_period);
  static CiMACD *CreateMACD(string symbol, ENUM_TIMEFRAMES period);
};
```

### Observer Pattern
Event handling uses observer pattern for market events:

```cpp
// Observer pattern for events
class CMarketObserver
{
private:
  CArrayObj *m_observers;
  
public:
  void RegisterObserver(CObserver *observer);
  void RemoveObserver(CObserver *observer);
  void NotifyObservers(ENUM_MARKET_EVENT event);
};
```

## Data Flow Patterns

### Event-Driven Architecture
The EA follows an event-driven architecture with clear data flow:

```
Market Data → OnTick() → Processing() → Signal Generation → Trading Decision → Order Execution
     ↓              ↓           ↓               ↓                ↓                 ↓
  Price Data    Analysis    Indicator       Signal          Risk Management    Position Management
```

### Indicator Data Flow
Indicator calculations follow a pipeline pattern:

```
Raw Data → Indicator Handle → Data Buffer → Signal Processing → Trading Signal
    ↓            ↓              ↓               ↓                  ↓
 Price Data    iMA()         CopyBuffer()   Cross Detection    Buy/Sell Decision
```

### Signal Processing Flow
Signal processing follows a chain of responsibility pattern:

```
Market Data → Indicator Calculation → Signal Validation → Risk Assessment → Final Decision
     ↓               ↓                    ↓                 ↓                  ↓
  Price Data      Technical Analysis    Signal Quality    Position Size      Execute Order
```

## State Management Patterns

### Finite State Machine
EA operations use finite state machine pattern:

```cpp
// State machine pattern
enum EA_STATE
{
  EA_STATE_INITIALIZING,
  EA_STATE_MONITORING,
  EA_STATE_SIGNAL_DETECTED,
  EA_STATE_EXECUTING,
  EA_STATE_ERROR
};

class CEAFSM
{
private:
  EA_STATE m_current_state;
  
public:
  void UpdateState(EA_STATE new_state);
  void ProcessState();
};
```

### Singleton Pattern
Global configuration uses singleton pattern:

```cpp
// Singleton pattern for configuration
class CConfigManager
{
private:
  static CConfigManager *m_instance;
  
public:
  static CConfigManager *GetInstance();
  bool LoadConfig();
  void SaveConfig();
};
```

## Error Handling Patterns

### Error Recovery Pattern
Comprehensive error handling with recovery mechanisms:

```cpp
// Error handling pattern
class CErrorHandler
{
public:
  bool ExecuteWithErrorHandling(function<void> operation);
  void LogError(int error_code, string description);
  bool RecoverFromError(int error_code);
  
private:
  bool HandleConnectionError();
  bool HandleDataError();
  bool HandleExecutionError();
};
```

### Validation Pattern
Input and operation validation pattern:

```cpp
// Validation pattern
class CValidator
{
public:
  bool ValidateInputParameters();
  bool ValidateOrderParameters(double volume, double sl, double tp);
  bool ValidateMarketConditions();
  bool ValidateAccountStatus();
};
```

## Performance Patterns

### Caching Pattern
Indicator handle caching for performance:

```cpp
// Caching pattern for indicators
class CIndicatorCache
{
private:
  CMap<string, int> m_indicator_handles;
  
public:
  int GetIndicatorHandle(string key, function<int()> creator);
  void ClearCache();
  bool IsCached(string key);
};
```

### Lazy Loading Pattern
Resource initialization on demand:

```cpp
// Lazy loading pattern
class CLazyResource
{
private:
  bool m_initialized;
  resource_type m_resource;
  
public:
  resource_type GetResource();
  bool IsInitialized();
  void Initialize();
};
```

## Testing Patterns

### Test-Driven Development
Unit testing pattern for EA components:

```cpp
// Testing pattern
class CSignalTester
{
public:
  bool TestSignalGeneration();
  bool TestRiskCalculation();
  bool TestIndicatorLogic();
  bool TestErrorHandling();
  
private:
  void SetupTestData();
  void ValidateResults();
};
```

### Mock Pattern
Mock objects for testing dependencies:

```cpp
// Mock pattern for testing
class CMockTrade : public CExpertTrade
{
public:
  virtual bool OrderOpen(/*...*/) override;
  virtual bool OrderClose(/*...*/) override;
  void SetExpectations(bool should_succeed);
};
```

## Integration Patterns

### Adapter Pattern
Integration with external systems:

```cpp
// Adapter pattern for external APIs
class CExternalAPIAdapter
{
public:
  bool SendNotification(string message);
  bool FetchExternalData();
  bool ProcessExternalSignal();
  
private:
  bool ConvertToInternalFormat();
};
```

### Bridge Pattern
Abstraction of platform-specific implementations:

```cpp
// Bridge pattern for platform abstraction
class CPlatformBridge
{
public:
  virtual bool ExecuteOrder(OrderParams params) = 0;
  virtual MarketData GetMarketData() = 0;
  virtual AccountInfo GetAccountInfo() = 0;
};
```

## Configuration Patterns

### Builder Pattern
Complex configuration object creation:

```cpp
// Builder pattern for configuration
class CEAConfigBuilder
{
public:
  CEAConfigBuilder &SetMAPeriod(int period);
  CEAConfigBuilder &SetRiskPercent(double percent);
  CEAConfigBuilder &SetTimeframe(ENUM_TIMEFRAMES tf);
  EAConfig Build();
};
```

### Strategy Configuration Pattern
Runtime strategy configuration:

```cpp
// Strategy configuration pattern
class CStrategyConfig
{
public:
  void LoadStrategy(string strategy_name);
  void SetParameter(string name, double value);
  double GetParameter(string name);
  bool ValidateConfiguration();
};
```

These patterns provide a robust foundation for developing maintainable, scalable, and testable Expert Advisors in MQL5 while following best practices and established design patterns.