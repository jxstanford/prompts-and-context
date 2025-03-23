# Claude 3.7 Coding Project Instructions
## Artifacts
- use artifacts for code and documentation
- one artifact per code file 
- code artifacts should start with file path/name
- artifact names should be same as file name

## Context
- use concise context to improve chat efficiency
- highlight opportunities to improve results with specific additional context
- look for references to additional context in a CLAUDE.md file

## Development Approach
- Prefer user-story and test-driven development
- Design interfaces first, with explicit dependency injection points
- Start with acceptance tests that capture key customer requirements
- Isolate domain logic from external dependencies
- prefer code efficiency over readability

## Code Quality Standards
- Production-grade error handling with appropriate context in exceptions
- Comprehensive test coverage (unit, integration, end-to-end)
- Structured logging with contextual information and appropriate levels
- Metrics collection via OpenTelemetry for instrumentation
- Use pydantic for typing 
- Type hints throughout with runtime validation where necessary
- Follow PEP 8 style guidelines with appropriate justifications for exceptions

## Architecture Principles
- Domain-driven design with clear bounded contexts
- Hexagonal/ports and adapters architecture to separate:
  - Domain/business logic (core)
  - External services (adapters)
  - Application services (orchestration)
- Inject dependencies through constructors or parameterized factory functions
- Configuration through environment variables, config files, and parameter stores
- Follow SOLID principles, especially interface segregation and dependency inversion

## ML Project Organization
- Separate codebases for training pipelines, evaluation, and inference services
- Version control for:
  - Model artifacts
  - Training datasets
  - Hyperparameters
  - Feature preprocessing rules
- Feature engineering code shared between training and inference
- Clear separation between offline and online components
- Model registry with metadata tracking
- Model validation suite with predefined quality gates
- A/B testing infrastructure for controlled deployment
- Monitoring for model drift, data quality, and performance degradation

## Project Infrastructure
- CI/CD pipeline with:
  - Linting and static analysis
  - Security scanning
  - Unit and integration testing
  - Deployment with infrastructure as code
- Containerization with Docker
  - Base images with minimal dependencies
  - Multi-stage builds for smaller production images
  - GPU support configuration when needed
  - Health checks and proper signal handling
- Environment management scripts
- Database migration tools
- Local development utilities

## Documentation
- README with:
  - Project overview
  - Quick start guide
  - Architecture diagram
  - Development setup instructions
- API documentation with clear input/output contracts
- Architectural Decision Records (ADRs) for key design choices
- Environment setup guides
- User guides for non-technical stakeholders
- Runbooks for operational tasks

## Specific Implementation Guidelines
- Prefer composition over inheritance
- Use factory patterns for creating complex objects
- Implement retries and circuit breakers for external dependencies
- Cache expensive computations and database queries
- Follow least privilege principle for all external integrations
- Validate inputs at system boundaries
- Use immutable data structures where appropriate
- Implement graceful degradation for non-critical features
