---
created: 2025-09-08T23:27:41Z
last_updated: 2025-09-08T23:27:41Z
version: 1.0
author: Claude Code PM System
---

# Project Structure

## Directory Organization

### Root Structure
```
SMA_TrendStrategy/
├── .claude/                          # Claude Code Project Management
│   ├── context/                      # Project context documentation
│   │   ├── README.md                 # Context system documentation
│   │   ├── progress.md               # Project status and progress
│   │   ├── project-structure.md      # Directory organization (this file)
│   │   ├── tech-context.md           # Technologies and dependencies
│   │   ├── system-patterns.md        # Architectural patterns
│   │   ├── product-context.md        # Product requirements
│   │   ├── project-brief.md          # Project scope and goals
│   │   ├── project-overview.md       # Feature summary
│   │   ├── project-vision.md         # Long-term vision
│   │   └── project-style-guide.md    # Coding standards
│   ├── commands/                     # Command scripts
│   │   └── testing/                  # Testing commands
│   └── CLAUDE.md                     # Development guidelines
└── CLAUDE.md                         # Root-level development guidelines
```

### MQL5 Ecosystem Structure
```
D:\MetaTrader 5\MQL5\
├── Experts/                          # Expert Advisors (trading robots)
│   └── LionEA/                       # Lion EA collection
│       └── SMA_TrendStrategy/        # Current project
├── Indicators/                       # Custom indicators
├── Scripts/                          # Utility scripts
├── Include/                          # MQL5 standard library
│   ├── Arrays/                       # Array utilities
│   ├── Canvas/                       # Drawing canvas
│   ├── Charts/                       # Chart operations
│   ├── Controls/                     # UI controls
│   ├── Expert/                       # Expert framework
│   │   ├── Expert.mqh               # Main EA base class
│   │   ├── ExpertSignal.mqh         # Signal base class
│   │   ├── ExpertTrade.mqh          # Trade operations
│   │   ├── ExpertMoney.mqh          # Money management
│   │   ├── ExpertTrailing.mqh       # Trailing stops
│   │   ├── Signal/                  # Signal implementations
│   │   │   ├── SignalMA.mqh         # Moving Average signals
│   │   │   ├── SignalCCI.mqh        # CCI signals
│   │   │   └── ...                   # Other indicator signals
│   │   ├── Money/                    # Money management strategies
│   │   └── Trailing/                 # Trailing stop implementations
│   ├── Files/                        # File operations
│   ├── Generic/                      # Generic utilities
│   ├── Graphics/                     # Graphics operations
│   ├── Indicators/                   # Indicator utilities
│   ├── Math/                         # Mathematical functions
│   ├── Strings/                      # String operations
│   ├── Tools/                        # Development tools
│   └── Trade/                        # Trading operations
│       ├── Trade.mqh                 # Main trading class
│       ├── SymbolInfo.mqh            # Symbol information
│       ├── AccountInfo.mqh           # Account information
│       └── ...                       # Other trading utilities
├── Images/                           # Image resources
├── Logs/                             # Log files
├── Profiles/                         # Trading profiles
└── Scripts/                          # Utility scripts
```

## File Organization Patterns

### Expert Advisor Files
- **Main EA File**: `SMA_TrendStrategy.mq5` - Primary EA implementation
- **Signal Classes**: Custom signal implementations extending standard classes
- **Utility Classes**: Helper classes for specific functionality
- **Include Files**: Reusable components and shared logic

### Naming Conventions
- **EA Files**: `[StrategyName].mq5` (e.g., `SMA_TrendStrategy.mq5`)
- **Header Files**: `[ComponentName].mqh` (e.g., `RiskManagement.mqh`)
- **Signal Classes**: `Signal[IndicatorName].mqh` (e.g., `SignalSMA.mqh`)
- **Test Files**: `Test[ComponentName].mq5` (e.g., `TestSignalLogic.mq5`)

### File Structure Template
```cpp
// Standard EA file structure
#include <Expert\Expert.mqh>
#include <Expert\Signal\SignalMA.mqh>
#include <Expert\Trailing\TrailingFixedPips.mqh>
#include "CustomSignal.mqh"
#include "RiskManagement.mqh"

// Input parameters
input int MA_Period = 20;
input double Lots = 0.1;

// EA class definition
class CSMATrendStrategy : public CExpert
{
private:
  CSignalMA *m_signal;
  CRiskManagement *m_risk;
  
protected:
  virtual bool Init();
  virtual void Deinit();
  virtual bool Processing();
  
public:
  CSMATrendStrategy();
  ~CSMATrendStrategy();
};

// Implementation
CSMATrendStrategy::CSMATrendStrategy()
{
  // Constructor implementation
}

bool CSMATrendStrategy::Init()
{
  // Initialization logic
  return true;
}

// Expert Advisor standard functions
int OnInit()
{
  // EA initialization
  return(INIT_SUCCEEDED);
}

void OnDeinit(const int reason)
{
  // EA cleanup
}

void OnTick()
{
  // Main EA logic
}
```

## Module Organization

### Core Modules
1. **Signal Module** - Trading signal generation and analysis
2. **Trade Module** - Order execution and management
3. **Risk Module** - Position sizing and risk management
4. **Analysis Module** - Market analysis and indicator calculations
5. **Utility Module** - Helper functions and utilities

### Module Dependencies
```
Main EA
├── Signal Module
│   └── Standard Library Signals
├── Trade Module
│   └── CTrade Class
├── Risk Module
├── Analysis Module
│   └── Indicator Calculations
└── Utility Module
```

## Build and Deployment Structure

### Development Files
- Source files (.mq5) in project directory
- Header files (.mqh) in project or include directories
- Test files in dedicated test directory

### Compiled Output
- Compiled files (.ex5) generated in same directory as source
- MetaTrader 5 automatically compiles when added to charts
- No separate build process required

### Testing Structure
- Unit tests as separate script files
- Backtesting through MetaTrader Strategy Tester
- Optimization through genetic algorithm in Strategy Tester

## Configuration Management

### Input Parameters
- Strategy parameters defined as input variables
- Configurable through MetaTrader input dialog
- Optimization parameters for Strategy Tester

### External Dependencies
- MQL5 Standard Library (always available)
- Custom indicators (if used)
- External data files (if needed)

## Documentation Structure

### Code Documentation
- Inline comments for complex logic
- Function documentation for public interfaces
- Parameter descriptions for input variables

### Project Documentation
- Development guidelines in CLAUDE.md
- Context documentation in .claude/context/
- README files for major components

## Best Practices

### File Organization
- Keep related functionality together
- Use clear, descriptive file names
- Maintain consistent directory structure
- Separate concerns into logical modules

### Code Organization
- Follow MQL5 standard library patterns
- Use object-oriented design for complex systems
- Implement proper error handling
- Include comprehensive testing

### Maintainability
- Use version control for all source files
- Document architectural decisions
- Keep dependencies minimal
- Follow established naming conventions