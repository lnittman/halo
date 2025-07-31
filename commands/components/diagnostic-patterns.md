# 🔍 diagnostic patterns component

provides structured patterns for recognizing, analyzing, and debugging various types of errors and issues.

<component_directive>
this component offers reusable diagnostic patterns for commands that need to handle error analysis, debugging, and issue resolution.
</component_directive>

## error pattern recognition

### syntax error patterns
```xml
<syntax_patterns>
  <javascript>
    <pattern>
      <trigger>Unexpected token</trigger>
      <causes>
        - Missing closing bracket/parenthesis
        - Invalid keyword usage
        - Template literal unclosed
        - Import/export syntax issue
      </causes>
      <fix_strategy>
        Check syntax highlighting, match brackets, verify keyword usage
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>Unexpected identifier</trigger>
      <causes>
        - Variable declared without let/const/var
        - Reserved keyword as variable name
        - Missing comma in object/array
      </causes>
      <fix_strategy>
        Add declarations, rename variables, check punctuation
      </fix_strategy>
    </pattern>
  </javascript>
  
  <typescript>
    <pattern>
      <trigger>Type 'X' is not assignable to type 'Y'</trigger>
      <causes>
        - Type mismatch in assignment
        - Missing type assertion
        - Incorrect generic usage
        - Interface/type definition mismatch
      </causes>
      <fix_strategy>
        Update types, add assertion, cast correctly
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>Property 'X' does not exist on type 'Y'</trigger>
      <causes>
        - Optional property access
        - Interface missing property
        - Type assertion needed
        - Index signature required
      </causes>
      <fix_strategy>
        Add property, use optional chaining, add signature
      </fix_strategy>
    </pattern>
  </typescript>
</syntax_patterns>
```

### runtime error patterns
```xml
<runtime_patterns>
  <null_undefined>
    <pattern>
      <trigger>Cannot read property 'X' of undefined</trigger>
      <causes>
        - Undefined object access
        - Async operation before complete
        - Missing initialization
        - Optional parameter not provided
      </causes>
      <fix_strategy>
        Add null checks, default values, optional chaining
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>Cannot read property 'X' of null</trigger>
      <causes>
        - Null reference from API/database
        - DOM element not found
        - Expected array/object is null
      </causes>
      <fix_strategy>
        Null checks, fallback values, existence verification
      </fix_strategy>
    </pattern>
  </null_undefined>
  
  <async_errors>
    <pattern>
      <trigger>UnhandledPromiseRejection</trigger>
      <causes>
        - Missing try/catch in async function
        - Promise chain without error handler
        - Async/await without proper error handling
      </causes>
      <fix_strategy>
        Add try/catch, .catch() handlers, error boundaries
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>Callback was already called</trigger>
      <causes>
        - Multiple callback invocations
        - Improper control flow
        - Race condition in async operations
      </causes>
      <fix_strategy>
        Add guard clauses, ensure single execution, use promises
      </fix_strategy>
    </pattern>
  </async_errors>
</runtime_patterns>
```

### network error patterns
```xml
<network_patterns>
  <api_errors>
    <pattern>
      <trigger>404 Not Found</trigger>
      <causes>
        - Incorrect endpoint URL
        - Resource deleted
        - Wrong HTTP method
        - Authorization issues
      </causes>
      <fix_strategy>
        Verify URL, check resource exists, confirm method
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>500 Internal Server Error</trigger>
      <causes>
        - Server-side exception
        - Database connection failed
        - Configuration error
        - Timeout occurred
      </causes>
      <fix_strategy>
        Check server logs, verify configuration, add retry
      </fix_strategy>
    </pattern>
  </api_errors>
  
  <connection_errors>
    <pattern>
      <trigger>ECONNREFUSED</trigger>
      <causes>
        - Service not running
        - Wrong port number
        - Firewall blocking
        - Network configuration
      </causes>
      <fix_strategy>
        Verify service status, check port, configure firewall
      </fix_strategy>
    </pattern>
    
    <pattern>
      <trigger>ETIMEDOUT</trigger>
      <causes>
        - Slow response
        - Network latency
        - Server overload
        - Request timeout too short
      </causes>
      <fix_strategy>
        Increase timeout, optimize query, check server health
      </fix_strategy>
    </pattern>
  </connection_errors>
</network_patterns>
```

## stack trace analysis

### stack trace parsing
```xml
<stack_analysis>
  <nodejs_stack>
    <pattern>
      <format>
        at functionName (filename:line:column)
      </format>
      <interpretation>
        - functionName: failing function
        - filename: location of error
        - line: specific line number
        - column: character position
      </interpretation>
    </pattern>
  </nodejs_stack>
  
  <browser_stack>
    <pattern>
      <format>
        functionName@filename:line:column
      </format>
      <interpretation>
        - Similar to Node.js but with @ separator
        - Minified code may show different patterns
        - Source maps needed for original code
      </interpretation>
    </pattern>
  </browser_stack>
</stack_analysis>
```

### call stack interpretation
```xml
<stack_interpretation>
  <bottom_to_top>
    - Entry point: where execution began
    - Middle layers: intermediate functions
    - Top line: immediate cause of error
  </bottom_to_top>
  
  <async_stack_markers>
    - Promise.then: async operation chain
    - setTimeout: delayed execution
    - EventEmitter: event-driven code
    - async/await: modern async pattern
  </async_stack_markers>
</stack_interpretation>
```

## error correlation patterns

### multi-error analysis
```xml
<multi_error_patterns>
  <cascading_errors>
    <pattern>
      Multiple related failures in sequence
      <analysis>
        - Primary error causes secondary failures
        - Identify the root error
        - Fix primary to resolve all
      </analysis>
    </pattern>
  </cascading_errors>
  
  <concurrent_errors>
    <pattern>
      Multiple unrelated errors
      <analysis>
        - Separate root causes
        - Prioritize by severity
        - Fix independently
      </analysis>
    </pattern>
  </concurrent_errors>
  
  <intermittent_errors>
    <pattern>
      Errors that occur sporadically
      <analysis>
        - Race conditions likely
        - Resource contention
        - Timing-dependent bugs
      </analysis>
    </pattern>
  </intermittent_errors>
</multi_error_patterns>
```

## diagnostic workflows

### systematic debugging
```xml
<debugging_workflow>
  <step_1>
    <name>Reproduce consistently</name>
    <actions>
      - Create minimal test case
      - Identify precise conditions
      - Eliminate variables
    </actions>
  </step_1>
  
  <step_2>
    <name>Gather evidence</name>
    <actions>
      - Collect logs and traces
      - Check environment state
      - Document exact steps
    </actions>
  </step_2>
  
  <step_3>
    <name>Isolate cause</name>
    <actions>
      - Binary search through code
      - Comment out sections
      - Use debugger strategically
    </actions>
  </step_3>
  
  <step_4>
    <name>Fix and verify</name>
    <actions>
      - Implement minimal fix
      - Test extensively
      - Ensure no regressions
    </actions>
  </step_4>
</debugging_workflow>
```

### error prevention patterns
```xml
<prevention_patterns>
  <null_safe_patterns>
    - Optional chaining: obj?.prop
    - Nullish coalescing: value ?? defaultValue
    - Default parameters: function(param = defaultValue)
    - Existence checks: if (obj && obj.prop)
  </null_safe_patterns>
  
  <async_safety>
    - Always await promises
    - Try/catch async operations
    - Use Promise.allSettled for multiple
    - Add timeout mechanisms
  </async_safety>
  
  <type_safety>
    - Strict TypeScript mode
    - No implicit any
    - Proper type definitions
    - Runtime validation at boundaries
  </type_safety>
</prevention_patterns>
```

## usage integration

### in commands
```xml
<component_usage>
  <use>@diagnostic-patterns</use>
  
  <apply_to>
    <error_recognition>
      Match input against known patterns
    </error_recognition>
    
    <root_cause_analysis>
      Apply correlation and interpretation
    </root_cause_analysis>
    
    <solution_generation>
      Map identified patterns to fixes
    </solution_generation>
  </apply_to>
</component_usage>
```