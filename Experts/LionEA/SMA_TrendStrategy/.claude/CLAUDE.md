# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## MQL5 Expert Advisor Development

This is a MetaTrader 5 MQL5 project for developing an SMA Trend Strategy Expert Advisor. The project follows MQL5 standard library architecture and best practices.

### Development Environment

**IDE**: MetaEditor (included with MetaTrader 5)
- **Compile**: Press F7 or use Compile menu
- **Test**: Use Strategy Tester for backtesting and optimization
- **Run**: Load EA directly in MetaTrader 5 terminal

**File Structure**:
- `.mq5` - MQL5 source code files
- `.mqh` - MQL5 header files
- `.ex5` - Compiled executable files
- Standard library location: `D:\MetaTrader 5\MQL5\Include\`

### Core Architecture Components

**Expert Framework** (from `../../../Include/Expert/`):
- `CExpert` - Main Expert Advisor base class
- `CExpertSignal` - Signal generation base class
- `CExpertTrade` - Trade operations management
- `CExpertMoney` - Money management
- `CExpertTrailing` - Trailing stop management

**Trade Operations** (from `../../../Include/Trade/`):
- `CTrade` - Standardized trading interface
- `CSymbolInfo` - Symbol information management
- `CAccountInfo` - Account information access

**Signal Classes** (from `../../../Include/Expert/Signal/`):
- `CSignalMA` - Moving Average signal implementation
- Various other indicator-based signals (CCI, RSI, MACD, etc.)

### Key Development Patterns

**EA Structure**:
```cpp
#include <Expert\Expert.mqh>
#include <Expert\Signal\SignalMA.mqh>
#include <Expert\Trailing\TrailingFixedPips.mqh>

input int MA_Period = 20;
input double Lots = 0.1;

class CSimpleEA : public CExpert
{
protected:
  CSignalMA *m_signal;
  
public:
  bool CSimpleEA::Init()
  {
    // Initialize signal and other components
  }
  
  bool CSimpleEA::Processing()
  {
    // Main processing logic
  }
};
```

**Testing Methodology**:
- Use MetaTrader Strategy Tester for backtesting
- Test multiple timeframes and market conditions
- Optimize parameters using genetic optimization
- Forward test after optimization

**Error Handling**:
- Always check return values from trading operations
- Use GetLastError() for debugging
- Implement proper order validation
- Handle margin requirements and lot size limits

### Performance Optimization

**Indicator Management**:
- Cache indicator handles to avoid recreation
- Use CopyBuffer() efficiently
- Minimize indicator calculations per tick

**Memory Management**:
- Properly delete dynamic objects
- Avoid memory leaks in long-running EA
- Use MQL5 string management functions

### Risk Management

**Position Sizing**:
- Calculate lot sizes based on account balance
- Implement maximum risk per trade
- Consider margin requirements

**Stop Loss & Take Profit**:
- Always use stop losses for risk management
- Implement dynamic stop loss adjustment
- Consider volatility-based stop levels

## USE SUB-AGENTS FOR CONTEXT OPTIMIZATION

### 1. Always use the file-analyzer sub-agent when asked to read files.
The file-analyzer agent is an expert in extracting and summarizing critical information from files, particularly log files and verbose outputs. It provides concise, actionable summaries that preserve essential information while dramatically reducing context usage.

### 2. Always use the code-analyzer sub-agent when asked to search code, analyze code, research bugs, or trace logic flow.

The code-analyzer agent is an expert in code analysis, logic tracing, and vulnerability detection. It provides concise, actionable summaries that preserve essential information while dramatically reducing context usage.

### 3. Always use the test-runner sub-agent to run tests and analyze the test results.

Using the test-runner agent ensures:

- Full test output is captured for debugging
- Main conversation stays clean and focused
- Context usage is optimized
- All issues are properly surfaced
- No approval dialogs interrupt the workflow

## Philosophy

### Error Handling

- **Fail fast** for critical configuration (missing indicators, invalid parameters)
- **Log and continue** for optional features (signal filtering, advanced features)
- **Graceful degradation** when market data unavailable
- **User-friendly messages** through Print() and Comment() functions

### Testing

- Always use the test-runner agent to execute tests.
- Do not use mock services for anything ever.
- Do not move on to the next test until the current test is complete.
- If the test fails, consider checking if the test is structured correctly before deciding we need to refactor the codebase.
- Tests to be verbose so we can use them for debugging.

## Tone and Behavior

- Criticism is welcome. Please tell me when I am wrong or mistaken, or even when you think I might be wrong or mistaken.
- Please tell me if there is a better approach than the one I am taking.
- Please tell me if there is a relevant standard or convention that I appear to be unaware of.
- Be skeptical.
- Be concise.
- Short summaries are OK, but don't give an extended breakdown unless we are working through the details of a plan.
- Do not flatter, and do not give compliments unless I am specifically asking for your judgement.
- Occasional pleasantries are fine.
- Feel free to ask many questions. If you are in doubt of my intent, don't guess. Ask.

## ABSOLUTE RULES:

- NO PARTIAL IMPLEMENTATION
- NO SIMPLIFICATION : no "//This is simplified stuff for now, complete implementation would blablabla"
- NO CODE DUPLICATION : check existing codebase to reuse functions and constants Read files before writing new functions. Use common sense function name to find them easily.
- NO DEAD CODE : either use or delete from codebase completely
- IMPLEMENT TEST FOR EVERY FUNCTIONS
- NO CHEATER TESTS : test must be accurate, reflect real usage and be designed to reveal flaws. No useless tests! Design tests to be verbose so we can use them for debuging.
- NO INCONSISTENT NAMING - read existing codebase naming patterns.
- NO OVER-ENGINEERING - Don't add unnecessary abstractions, factory patterns, or middleware when simple functions would work. Don't think "enterprise" when you need "working"
- NO MIXED CONCERNS - Don't put validation logic inside API handlers, database queries inside UI components, etc. instead of proper separation
- NO RESOURCE LEAKS - Don't forget to delete dynamic objects, release indicator handles, or clean up string buffers
