---
created: 2025-09-08T23:27:41Z
last_updated: 2025-09-08T23:27:41Z
version: 1.0
author: Claude Code PM System
---

# Project Style Guide

## Coding Standards

### MQL5 Language Conventions

#### Naming Conventions
1. **Class Names**
   - Use PascalCase for class names
   - Prefix with 'C' for MQL5 standard compliance
   - Descriptive and meaningful names
   ```cpp
   class CSMATrendStrategy;
   class CRiskManager;
   class CSignalProcessor;
   ```

2. **Method Names**
   - Use PascalCase for method names
   - Verb-based for actions, noun-based for properties
   - Clear and descriptive
   ```cpp
   bool CalculateSignals();
   double GetRiskPercent();
   void SetStopLoss(double sl);
   ```

3. **Variable Names**
   - Use camelCase for local variables
   - Use m_ prefix for member variables
   - Use s_ prefix for static variables
   - Use g_ prefix for global variables
   ```cpp
   double m_riskPercent;
   static int s_signalCount;
   datetime g_lastExecutionTime;
   double calculatedValue;
   ```

4. **Constants**
   - Use UPPER_SNAKE_CASE for constants
   - Descriptive names
   ```cpp
   #define MAX_RISK_PERCENT 2.0
   #define DEFAULT_MA_PERIOD 20
   #define MIN_LOT_SIZE 0.01
   ```

5. **Enumeration Values**
   - Use UPPER_SNAKE_CASE with prefix
   ```cpp
   enum ENUM_SIGNAL_TYPE
   {
     SIGNAL_BUY = 1,
     SIGNAL_SELL = 2,
     SIGNAL_NONE = 0
   };
   ```

#### File Organization
1. **File Naming**
   - Use PascalCase for main files
   - Descriptive names
   - .mq5 extension for EA files
   - .mqh extension for header files
   ```
   SMATrendStrategy.mq5
   RiskManagement.mqh
   SignalProcessor.mqh
   ```

2. **File Structure**
   - Header guards for all .mqh files
   - Include dependencies at top
   - Clear section organization
   ```cpp
   //+------------------------------------------------------------------+
   //|                                                    SignalMA.mqh |
   //|                  Copyright 2025, MetaQuotes Software Corp. |
   //|                                             https://www.metaquotes.net/ |
   //+------------------------------------------------------------------+
   #property copyright "Copyright 2025, MetaQuotes Software Corp."
   #property link      "https://www.metaquotes.net/"
   #property version   "1.00"

   #ifndef __SIGNALMA_MQH__
   #define __SIGNALMA_MQH__

   //+------------------------------------------------------------------+
   //| Includes                                                        |
   //+------------------------------------------------------------------+
   #include <Expert\ExpertSignal.mqh>
   #include <Indicators\Trend.mqh>

   //+------------------------------------------------------------------+
   //| Class CSignalMA                                                 |
   //+------------------------------------------------------------------+
   class CSignalMA : public CExpertSignal
   {
     // Class implementation
   };

   //+------------------------------------------------------------------+
   #endif
   ```

#### Code Structure
1. **Class Organization**
   - Public methods first
   - Protected methods second
   - Private methods last
   - Member variables grouped by access level
   ```cpp
   class CExample
   {
   public:
     // Constructor and destructor
     CExample();
     ~CExample();
     
     // Public interface
     bool Initialize();
     void Process();
     double GetValue();
     
   protected:
     // Protected methods
     bool ValidateParameters();
     void CalculateInternal();
     
   private:
     // Private methods
     void Cleanup();
     bool CheckState();
     
     // Member variables
     double m_value;
     bool m_initialized;
     int m_handle;
   };
   ```

2. **Method Organization**
   - Input validation first
   - Main logic in the middle
   - Return value at the end
   - Error handling throughout
   ```cpp
   bool CExample::ProcessData(double input)
   {
     // Input validation
     if(input <= 0)
     {
       Print("Invalid input: ", input);
       return false;
     }
     
     // Main processing
     double result = input * m_multiplier;
     
     // Error handling
     if(!UpdateResult(result))
     {
       Print("Failed to update result");
       return false;
     }
     
     return true;
   }
   ```

#### Formatting Standards
1. **Indentation**
   - Use 2 spaces for indentation
   - Consistent throughout the file
   - No tabs, only spaces
   ```cpp
   class CExample
   {
     void Method()
     {
       if(condition)
       {
         // Code here
       }
     }
   };
   ```

2. **Braces**
   - K&R style for functions and classes
   - Consistent brace placement
   ```cpp
   class CExample {
   public:
     void Method() {
       if(condition) {
         // Code
       }
     }
   };
   ```

3. **Spacing**
   - Spaces around operators
   - Space after commas
   - No space before parentheses
   ```cpp
   int result = a + b;
   function(param1, param2);
   if(condition) {
     // Code
   }
   ```

4. **Line Length**
   - Maximum 120 characters per line
   - Break long lines appropriately
   - Align multi-line parameters
   ```cpp
   bool LongFunctionName(const string parameter1,
                         const int parameter2,
                         const double parameter3)
   {
     // Implementation
   }
   ```

### Documentation Standards

#### Comment Style
1. **Header Comments**
   - Standard MQL5 header format
   - Include copyright and version information
   ```cpp
   //+------------------------------------------------------------------+
   //|                                                 SMATrendStrategy.mq5 |
   //|                  Copyright 2025, MetaQuotes Software Corp. |
   //|                                             https://www.metaquotes.net/ |
   //+------------------------------------------------------------------+
   ```

2. **Class Documentation**
   - Purpose and functionality
   - Usage examples
   - Dependencies
   ```cpp
   //+------------------------------------------------------------------+
   //| Class CSMATrendStrategy                                          |
   //| Purpose: Implements SMA crossover trend strategy               |
   //| Usage: Create instance and call Initialize() then Process()     |
   //| Dependencies: CExpert, CSignalMA, CTrade                         |
   //+------------------------------------------------------------------+
   ```

3. **Method Documentation**
   - Purpose and parameters
   - Return values
   - Error conditions
   ```cpp
   //+------------------------------------------------------------------+
   //| Method: Initialize                                               |
   //| Purpose: Initialize the EA with given parameters                |
   //| Parameters:                                                      |
   //|   maPeriod - Period for moving average calculation               |
   //|   riskPercent - Risk percentage per trade (0.1-2.0)              |
   //| Return: true if successful, false otherwise                      |
   //| Errors: INVALID_PARAMETERS, INITIALIZATION_FAILED               |
   //+------------------------------------------------------------------+
   ```

4. **Inline Comments**
   - Explain complex logic
   - Mark TODO items
   - Explain non-obvious decisions
   ```cpp
   // Calculate position size based on account balance and risk
   double positionSize = (accountBalance * riskPercent) / (stopLoss * pointValue);
   
   // TODO: Add volatility-based position sizing adjustment
   // Note: Using simple calculation for now, enhance in next iteration
   ```

#### Documentation Requirements
1. **Public Interface Documentation**
   - All public methods must be documented
   - Include parameter descriptions
   - Document return values and error conditions

2. **Complex Logic Documentation**
   - Document non-obvious algorithms
   - Explain mathematical formulas
   - Provide context for business logic

3. **Configuration Documentation**
   - Document all input parameters
   - Provide valid ranges and defaults
   - Explain parameter interactions

## Development Patterns

### Design Patterns
1. **Singleton Pattern**
   - Use for global configuration
   - Thread-safe implementation
   ```cpp
   class CConfigManager
   {
   private:
     static CConfigManager *m_instance;
     
   public:
     static CConfigManager *GetInstance();
   };
   ```

2. **Factory Pattern**
   - Use for object creation
   - Centralized creation logic
   ```cpp
   class CIndicatorFactory
   {
   public:
     static CIndicator *CreateIndicator(ENUM_INDICATOR_TYPE type);
   };
   ```

3. **Observer Pattern**
   - Use for event handling
   - Decoupled communication
   ```cpp
   class CEventDispatcher
   {
   private:
     CArrayObj *m_observers;
     
   public:
     void RegisterObserver(CObserver *observer);
     void NotifyObservers(CEvent *event);
   };
   ```

### Error Handling Patterns
1. **Consistent Error Handling**
   - Use standardized error codes
   - Always check return values
   - Provide meaningful error messages
   ```cpp
   bool CExample::Process()
   {
     if(!ValidateParameters())
     {
       SetLastError(INVALID_PARAMETERS);
       return false;
     }
     
     if(!ExecuteOperation())
     {
       Print("Operation failed: ", GetLastError());
       return false;
     }
     
     return true;
   }
   ```

2. **Resource Management**
   - RAII pattern for resource cleanup
   - Always release handles and memory
   ```cpp
   class CResourceHolder
   {
   private:
     int m_indicatorHandle;
     
   public:
     CResourceHolder() { m_indicatorHandle = INVALID_HANDLE; }
     ~CResourceHolder() { Cleanup(); }
     
     void Cleanup()
     {
       if(m_indicatorHandle != INVALID_HANDLE)
       {
         IndicatorRelease(m_indicatorHandle);
         m_indicatorHandle = INVALID_HANDLE;
       }
     }
   };
   ```

### Testing Patterns
1. **Test Organization**
   - Separate test files for each component
   - Clear test naming conventions
   - Test both success and failure cases
   ```cpp
   // Test_SignalProcessor.mq5
   bool Test_SignalCalculation()
   {
     // Test signal calculation logic
   }
   
   bool Test_ErrorHandling()
   {
     // Test error conditions
   }
   ```

2. **Test-Driven Development**
   - Write tests before implementation
   - Maintain high test coverage
   - Test edge cases and boundary conditions

## Best Practices

### Performance Optimization
1. **Indicator Management**
   - Cache indicator handles
   - Avoid unnecessary recalculations
   - Use efficient buffer access
   ```cpp
   class CIndicatorCache
   {
   private:
     int m_maHandle;
     double m_maBuffer[];
     
   public:
     bool Initialize()
     {
       m_maHandle = iMA(_Symbol, _Period, MA_PERIOD, 0, MODE_SMA, PRICE_CLOSE);
       return m_maHandle != INVALID_HANDLE;
     }
     
     double GetMAValue(int shift)
     {
       if(CopyBuffer(m_maHandle, 0, shift, 1, m_maBuffer) > 0)
         return m_maBuffer[0];
       return 0;
     }
   };
   ```

2. **Memory Management**
   - Minimize dynamic allocation
   - Use arrays instead of objects where possible
   - Clean up resources properly

3. **Algorithm Efficiency**
   - Use appropriate data structures
   - Minimize computational complexity
   - Avoid unnecessary calculations

### Security Considerations
1. **Input Validation**
   - Validate all input parameters
   - Check ranges and types
   - Sanitize external data
   ```cpp
   bool CValidator::ValidateRiskPercent(double risk)
   {
     if(risk <= 0 || risk > MAX_RISK_PERCENT)
     {
       Print("Invalid risk percentage: ", risk);
       return false;
     }
     return true;
   }
   ```

2. **Error Handling**
   - Handle all possible error conditions
   - Provide meaningful error messages
   - Implement graceful degradation

3. **Risk Management**
   - Never risk more than configured percentage
   - Implement position size limits
   - Add account protection mechanisms

### Maintainability
1. **Code Organization**
   - Single responsibility principle
   - Clear separation of concerns
   - Modular design

2. **Documentation**
   - Keep documentation current
   - Document design decisions
   - Provide usage examples

3. **Version Control**
   - Commit frequently with meaningful messages
   - Use feature branches
   - Maintain clean git history

## Configuration Standards

### Input Parameters
1. **Parameter Naming**
   - Descriptive names
   - Include units in comments
   - Provide reasonable defaults
   ```cpp
   input group "SMA Parameters"
   input int      MA_Fast_Period = 10;     // Fast SMA period
   input int      MA_Slow_Period = 20;     // Slow SMA period
   input ENUM_MA_METHOD MA_Method = MODE_SMA; // MA calculation method
   
   input group "Risk Management"
   input double   Risk_Percent   = 1.0;    // Risk per trade (%)
   input double   StopLoss_Pips  = 20.0;   // Stop loss in pips
   input double   TakeProfit_Pips = 40.0;  // Take profit in pips
   ```

2. **Parameter Validation**
   - Validate parameter ranges
   - Check parameter combinations
   - Provide meaningful error messages

### Configuration Files
1. **External Configuration**
   - Use INI or JSON format for complex configs
   - Provide configuration validation
   - Include default configurations

2. **Environment Configuration**
   - Different settings for testing vs production
   - Environment-specific parameters
   - Configuration versioning

## Testing Standards

### Unit Testing
1. **Test Structure**
   - Arrange-Act-Assert pattern
   - Independent test cases
   - Clear test names
   ```cpp
   // Test MA calculation
   void Test_MACalculation()
   {
     // Arrange
     double testPrices[] = {1.0, 1.1, 1.2, 1.3, 1.4};
     double expectedMA = 1.2;
     
     // Act
     double actualMA = CalculateSMA(testPrices, 5);
     
     // Assert
     AssertEqual(actualMA, expectedMA, "SMA calculation incorrect");
   }
   ```

2. **Test Coverage**
   - Minimum 80% code coverage
   - Test all public methods
   - Include edge cases and error conditions

### Integration Testing
1. **Strategy Testing**
   - Test with historical data
   - Multiple market conditions
   - Performance benchmarking

2. **System Testing**
   - End-to-end testing
   - Real market conditions
   - User acceptance testing

## Quality Assurance

### Code Review Standards
1. **Review Checklist**
   - Code follows style guide
   - Proper error handling
   - Performance considerations
   - Security implications
   - Test coverage

2. **Review Process**
   - Peer review for all changes
   - Automated quality checks
   - Documentation updates

### Continuous Integration
1. **Build Process**
   - Automated compilation
   - Code analysis
   - Test execution
   - Documentation generation

2. **Quality Metrics**
   - Code complexity
   - Test coverage
   - Performance benchmarks
   - Security scanning

This style guide provides comprehensive standards for developing high-quality, maintainable, and reliable MQL5 Expert Advisors while following industry best practices and MQL5 conventions.