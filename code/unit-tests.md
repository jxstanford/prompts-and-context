Create comprehensive pytest unit tests for #$ARGUMENTS that follow these requirements. Mirror the path of the codebase in the tests/unit folder. Create ONLY one test file per source file.
ALWAYS start in plannning mode. If we're not in planning mode ask the user to switch modes or do it for them.

**Test Coverage Requirements:**

- Test all public methods and functions
- Cover edge cases, boundary conditions, and error scenarios
- Test both positive and negative cases
- Aim for high code coverage while focusing on meaningful tests

**Test Structure:**

- Use descriptive test names that explain what is being tested
- Group related tests using test classes when appropriate
- Use pytest fixtures for setup and teardown
- Follow the Arrange-Act-Assert pattern

**Testing Scenarios to Include:**

- Valid inputs with expected outputs
- Invalid inputs and error handling
- Boundary values (empty, null, min/max values)
- Type validation and edge cases
- Side effects and state changes
- Integration points and dependencies

**Pytest Features to Utilize:**

- Parametrized tests for multiple input scenarios
- Fixtures for common setup/teardown
- Mocking for external dependencies
- Exception testing with pytest.raises
- Markers for test categorization if needed

**Code Quality:**

- Write clear, readable test code
- Include docstrings for complex test scenarios
- Use meaningful variable names
- Keep tests focused and atomic
- Avoid test interdependencies

**Additional Considerations:**

- Mock external services, APIs, and file I/O
- Test configuration and environment-specific behaviorcla
- Include performance tests for critical paths if relevant
- Consider async testing if the code uses async/await
- When appropriate, generate fuzz tests
- ALWAYS keep track of opportunities to refactor complex code into more SOLID, testable code. Write these to REFACTORING_OPPORTUNITIES.md in the root of the project
- run created test to ensure they pass
- all tests MUST pass!
- assess the coverage
- do not create extraneous files
- if you find obvious bugs, file a github issue with a bug label using the kamiwaza-internal/kamiwaza repo

