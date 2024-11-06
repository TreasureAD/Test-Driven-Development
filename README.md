# Testing Notes

## Software Development Challenges

- **Phases of Software Development**: 
  - Analysis and Design, Development, Testing, Integration, and Maintenance.
  - Agile vs. Waterfall: Same phases but Agile cycles are smaller and faster, focusing on iterative development.
  
- **Cost Distribution in Software Development**:
  - Initial phases (analysis, design, implementation) are relatively low cost.
  - **Testing and Integration**: More expensive.
  - **Maintenance**: Most costly (up to 65% of total software costs).

- **Challenges in Software Maintenance**:
  - **Code Entropy**: Code becomes brittle and rigid over time, especially when systems change and code isn't updated.
  - **Isolated Code Ownership**: Knowledge often limited to one developer or team, leading to issues when that owner leaves or changes focus.
  - **Infrequent Validation**: Limited testing, especially before releases, leads to regression-prone software where changes in one area break other parts.
  - **Legacy Code**:
    - Often outdated or inherited code.
    - **Definition from "Working Effectively with Legacy Code"**: Legacy code is any code without automated tests, making it brittle and error-prone.

## Test-Driven Development (TDD)

- **Definition of a Test**:
  - Verifies code works as expected in terms of quality, performance, reliability, and functionality.
  - Three key aspects to verify:
    - **Requirements Satisfaction**: Solves the intended problem.
    - **Input Handling**: Responds properly to valid and invalid inputs.
    - **Performance and Reliability**: Must meet acceptable standards.

- **What is TDD?**
  - TDD is a **development process driven by tests**.
  - Focuses on short development cycles to continually deliver customer value.
  
- **TDD Cycle (Red/Green/Refactor)**:
  1. **Red**: Write a test that fails, indicating the feature hasn’t been implemented.
  2. **Green**: Write minimal code to make the test pass. Often, initial implementations may include hardcoded values.
  3. **Refactor**: Clean up the code, ensuring it’s maintainable and flexible while keeping the test passing.
  - **Benefits**:
    - Iterative feedback and improvement.
    - Often results in simpler, more robust solutions.

## History of Test-Driven Development

- **Origin and Evolution**:
  - First formalized in 1999 in **"eXtreme Programming Explained"** by Kent Beck, followed by **"TDD: By Example"** in 2002.
  - NASA’s Project Mercury (1960s): Early test-focused development, but not TDD as we know it.
  - 1989: TDD practices began in the Smalltalk community.
  - 1994: Kent Beck’s paper on **SUnit** (foundation for xUnit frameworks, e.g., JUnit).

- **Legacy**:
  - TDD has a **long history** with frameworks and practices well-vetted across various platforms and programming languages.

## Why Practice Test-Driven Development (TDD)?

- **Business Benefits**:
  - **Requirement Verification**: Ensures that the software meets specified requirements by incorporating test writing and red/green/refactor cycles.
  - **Catch Regressions**: Helps prevent regressions (features that stop working after changes) by catching issues as soon as they occur.
  - **Lower Maintenance Costs**: Reduces maintenance efforts by verifying requirements early and preventing repeated issues.

- **Developer Benefits**:
  - **Design-First Mentality**: Writing failing tests encourages thinking about code interactions and design simplicity, preventing overengineering.
  - **Increased Momentum**: TDD’s cycle breaks features down into smaller steps, making continuous progress easier and motivating.
  - **Confidence in Code Changes**: With a robust test suite, developers can confidently refactor and improve the code without fear of breaking functionality.
  - **Focus on Customer Needs**: Ensures that the software aligns with real customer requirements, avoiding overcomplicated solutions.

## Types of Testing

- **Unit Testing**:
  - Verifies each unit (e.g., classes, functions) independently.
  - **Strength**: Fast, isolated tests ideal for the inner development cycle.
  - **Weakness**: Doesn’t test interactions between units.

- **Integration Testing**:
  - Verifies multiple units working together to catch issues in dependencies and data flow.
  - **Strength**: Confirms units’ interactions and contracts.
  - **Weakness**: Slower than unit tests and often run in continuous integration environments.

- **Acceptance Testing**:
  - Tests software from the end-user’s perspective, confirming overall functionality.
  - **Strength**: Ensures the system meets user expectations.
  - **Weakness**: Complex to maintain in large systems; slower.

- **Balanced Testing Strategy**:
  - A good testing approach combines unit, integration, and acceptance tests.
  - **Note**: TDD is not limited to unit tests; it includes integration and acceptance testing where appropriate.

## Testing Perspectives

- **Black-Box Testing**:
  - Tests the system from the outside without knowledge of its internals, ideal for less brittle tests.
  - **Downside**: May require setting up dependencies, which can be complex.

- **White-Box Testing**:
  - Accesses the internals of the component, allowing for detailed testing and custom dependency injection.
  - **Downside**: Risks becoming brittle as tests may break with internal changes.

## Testing Frameworks and Tools

- **xUnit Family**:
  - Popular for TDD, with frameworks for nearly all languages (e.g., JUnit for Java).
  - Widely available for various testing types, making TDD accessible for different development contexts.

- **Acceptance Testing Tools**:
  - Examples include **Selenium**, **Watir**, **Cypress.io** for UI testing.

## Basic Testing Concepts

- **Test**: Fundamental building block verifying specific functionality.
- **Test Suite**: A collection of tests grouped logically.
- **Hooks**:
  - **BeforeEach/AfterEach**: Run before/after every test.
  - **Before/After**: Run once for the entire suite.
- **Assertions**:
  - Core of test verification, checking for specific outcomes (e.g., equality, null values, collection containment).

## Test Execution and Test Runners

- **Test Runner**:
  - Executes tests, either synchronously or asynchronously.
  - **Synchronous Execution**: Tests run one after another, reducing conflicts.
  - **Asynchronous Execution**: Tests run in parallel, which can cause issues if shared states are not isolated.

- **Concurrency in Tests**:
  - **Example**: An e-commerce cart where add/remove item tests might conflict if run in parallel on a shared cart instance.
  - **Solution**: Create new instances for unit tests; carefully manage shared dependencies in integration/acceptance tests.

**Key Reminder**: Writing tests at all is more critical than writing perfect tests. Start simple and improve over time.

## Insights from Testing

- **Enhanced Insights**: Testing, especially through TDD, provides more than just a pass/fail status.
  - **Coverage Metrics**: Determine how much code is covered by tests.
  - **Dependency Health**: Check if dependencies (e.g., external libraries) function properly.
  - **Code Quality**: Helps ensure adherence to coding style guidelines.
  - **Business-Level Insights**:
    - Detect regressions.
    - Monitor performance under load.
    - Identify breaking changes that may impact partner code.

## Dependency Injection

- **Definition**: A technique for supplying code with the dependencies it requires, useful in TDD for creating flexible tests.
- **Purpose**: Allows control over dependencies in tests, such as simulating errors or specific conditions.
  
- **Types of Dependency Injection**:
  - **Constructor Injection**: Dependencies are passed via a class’s constructor (e.g., a `Greeter` class receiving `nameService` via constructor).
  - **Property Injection**: Uses setters or properties to inject dependencies.
  - **Method Injection**: In functional languages, dependencies are parameters in the methods/functions.

- **Benefits**:
  - Simplifies testing by allowing specific behaviors to be tested.
  - Enhances flexibility for creating different testing conditions.

- **Trade-offs**:
  - **Self-Contained Code**: Easier to understand but harder to test.
  - **Heavy Dependency Injection**: Easier to test, more flexible but harder to follow/debug due to unclear dependency usage.

## Test Doubles

- **Definition**: Substitute objects used in tests to mimic real objects.
  - **Stubs**: Provide predefined responses to specific calls (e.g., a `BadNameService` that simulates an error).
  - **Mocks**: Advanced stubs that include predefined responses and verify expected behaviors after tests.

- **Test Double Best Practices**:
  - Avoid creating excessive dependencies between the product code and test code.
  - Test for behavior, not implementation details, to prevent brittle code.

## Best Practices for Testing Code

1. **Treat Test Code as Production Code**:
   - Write maintainable, readable test code since it will need regular updates.
   
2. **Cover Positive and Negative Cases**:
   - Test for correct behavior as well as incorrect or unexpected inputs.

3. **Avoid Code Duplication**:
   - Centralize common setup and teardown logic to simplify maintenance.

4. **Only Focus on Necessary Asserts**:
   - Avoid unnecessary assertions that may make tests brittle.

5. **Regularly Review Team Practices**:
   - Continually refine testing strategies and address challenges, such as long test execution times.
   
6. **Strive for Continuous Improvement**:
   - Leave code and tests in better condition than they were before each task.

## Anti-Patterns in Test-Driven Development (TDD)

1. **Interdependent Tests**:
   - **Order Independence**: Tests should run successfully in any order. If test order affects results, there is likely an unintended dependency.
   - **Cascading Failures**: Failures in one test should not cause failures in unrelated tests, as it makes debugging difficult.
   - **Parallel vs. Serial Execution**: Running tests in parallel can reveal hidden dependencies but may also add complexity.

2. **Testing Implementation Details**:
   - Focus on testing what the code accomplishes, not how it accomplishes it.
   - Overuse of mocks to test internal workings is a sign of this anti-pattern, as it can make tests brittle and sensitive to minor changes in code structure.

3. **Long-Running Tests**:
   - **Warning Signs**: Long test durations may indicate overly coupled code or insufficient modularization.
   - **Impact on TDD Cycle**: Slow tests disrupt the rapid red/green/refactor cycle, reducing agility and confidence in changes.
   - **Causes**: Tightly coupled code or too much setup required for basic scenarios.

## Limitations of TDD

1. **Incomplete Coverage**:
   - TDD doesn’t guarantee all bugs are caught. Even with TDD, production issues can arise that were missed during testing.
   
2. **Not Sufficient for Deployment Verification**:
   - TDD ensures functionality but doesn’t handle deployment-specific issues, such as configuration or network changes that can break software in production.

3. **Integration Challenges**:
   - TDD doesn’t inherently address integration problems that may only emerge in production environments (e.g., breaking changes in dependencies).

4. **Management Buy-In**:
   - Support from management is crucial for the successful adoption of TDD. Short-term challenges may deter managers unfamiliar with its long-term benefits.

## Common Questions About TDD

1. **Do You Need to Be Agile to Practice TDD?**
   - No, TDD can be practiced in any development methodology, including Waterfall. However, TDD pairs well with Agile due to its iterative, feedback-focused nature.

2. **Do Tests Need to Be Written First?**
   - While TDD traditionally requires tests to be written first (red/green/refactor), writing tests later can still provide benefits, such as preventing overengineering and enhancing confidence in code changes.
   - The ultimate goal is delivering value to the customer, so TDD practices can be adapted as needed.

3. **Is TDD a One-Size-Fits-All Approach?**
   - No, TDD should be customized to fit the needs of the team and project. Retrospectives and continuous improvement are key to refining TDD practices.

## Performance Testing

- **Purpose**: Measures software speed and responsiveness, primarily focusing on **latency** (e.g., time between user action and app response).
  - **Acceptable Latency**: Generally, users tolerate 150-300 milliseconds. Exceeding this can result in user frustration and potential app abandonment.

- **Core Web Vitals**: 
  - Created by Google to measure and improve web performance by capturing common latency metrics that affect user experience.

- **Types of Performance Testing**:
  - **Load Testing**: Simulates expected user load to ensure the system can handle it.
  - **Stress Testing**: Gradually increases load to test the system's breaking point.
  - **Soak Testing**: Maintains high load over a prolonged period to observe system stability and resource leaks.
  - **Spike Testing**: Introduces sudden, high loads to test system recovery.

- **Goal**: Identify and resolve bottlenecks causing high latency, iteratively improving user experience by fixing issues as they are found.

## Production Testing

- **Purpose**: Verifies that production software operates as expected under real conditions.
  
- **Methods**:
  - **Synthetic Monitoring**: Generates simulated load through scripted actions to monitor key functions, even during low activity times, ensuring hidden issues are detected.
  - **Chaos Engineering**:
    - Tests resilience by intentionally causing failures (e.g., shutting down servers or simulating high latency).
    - Originated from Netflix to help build robust systems that tolerate unexpected issues.

- **Significance**: Both synthetic monitoring and chaos engineering are essential for high-quality production systems, although they’re not typically integrated with TDD.

## Security and Compliance Testing

- **Importance**: Security is critical to prevent unauthorized access and ensure data protection.
  
- **Key Methods**:
  - **Penetration Testing (Pen Testing)**:
    - Simulates cyberattacks to identify vulnerabilities in software security.
    - Aims to prevent data breaches and infrastructure failures.
  
  - **Compliance Testing**:
    - Ensures adherence to regulations like **GDPR** for data protection in the EU.
    - Common certifications:
      - **ISO 9001** for quality management.
      - **ISO 27001** for information security.
    - These certifications often require rigorous testing and documentation, sometimes involving external evaluations.

- **Limitations in TDD**: Security and compliance testing are essential but not suited to TDD due to their complex, often manual nature.




