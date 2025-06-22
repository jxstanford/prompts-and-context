# Claude Code Development Instructions

## Project Discovery & Context Analysis
**Always start by analyzing the existing project:**
- Read `pyproject.toml`, `package.json`, `requirements.txt` to understand dependencies
- Check `docker-compose.yml`, `Dockerfile` for service architecture
- Review `.env.example`, `config/` for configuration patterns
- Examine existing code structure and patterns
- Look for `CLAUDE.md` or similar files with project-specific context
- Identify project type: CLI tool, web API, ML pipeline, full-stack app, etc.

**Adapt architecture complexity to project scope:**
- Simple scripts: minimal structure, focus on functionality
- CLI tools: typer + rich, simple error handling
- APIs: FastAPI + pydantic models, structured logging
- ML projects: full pipeline separation, experiment tracking
- Full-stack: clear frontend/backend boundaries

## Technology Stack Preferences

**Python Core Stack:**
- **Package Management**: uv for dependencies and virtual environments
- **Task Coordination**: Makefiles for common workflows
- **Documentation**: MkDocs + mkdocstrings for comprehensive docs
- **Web APIs**: FastAPI + pydantic + httpx
- **CLI**: typer + rich for user interaction
- **Testing**: pytest + coverage, tox for multi-version (consider nox for complex environments)
- **Code Quality**: ruff (linting/formatting) + mypy + deptry
- **Data**: pandas (vectorized operations), polars for performance-critical
- **HTTP**: httpx over requests

**Multi-Language Support:**
- **Frontend**: React + TypeScript, Vite for build tooling
- **Containers**: Docker multi-stage builds, docker-compose for development
- **Scripts**: bash for system automation, Python for data processing
- **Shell Script Quality**: ShellCheck for static analysis, bats-core for unit testing
- **Notebooks**: Jupyter for exploration, convert to modules for production

## Claude Code Tool Usage & Project Setup
- **File Operations**: Direct file creation/editing for implementation
- **Terminal**: Package installation, testing, running services, git operations
- **Artifacts**: Documentation, architecture diagrams, code reviews, examples
- **Directory Structure**: Create full project scaffolding upfront
- **Environment Setup**: Use terminal for virtual environments, dependency installation

**CLAUDE.md File Management:**
When starting work on a project, always manage CLAUDE.md files:

1. **Check for existing CLAUDE.md**:
   ```bash
   # Read existing CLAUDE.md if present
   cat CLAUDE.md
   ```

2. **Create or update project context**:
   - **If no CLAUDE.md exists**: Create new CLAUDE.md with project-specific instructions
   - **If CLAUDE.md exists**: Create CLAUDE.md.local to supplement existing instructions
   - **Always ensure CLAUDE.md.local is in .gitignore**

3. **CLAUDE.md.local Template**:
   ```markdown
   # Project-Specific Context (Local)
   
   ## Project Analysis
   - **Type**: [CLI/API/ML Pipeline/Full-Stack/etc.]
   - **Stack**: [Key technologies discovered]
   - **Architecture**: [Brief description of structure]
   
   ## Build & Test Commands
   - **Install**: `uv sync` or discovered install command
   - **Test**: `pytest` or discovered test command
   - **Lint**: `ruff check` or discovered lint command
   - **Build**: [Build command if applicable]
   - **Run**: [Run command for development]
   
   ## Project-Specific Notes
   - [Any unusual patterns or requirements]
   - [Performance considerations]
   - [Team conventions discovered]
   - [Integration points]
   
   ## Recent Changes
   - [Date]: [Significant change description]
   ```

4. **Merge Strategy for Existing CLAUDE.md**:
   - Preserve existing team conventions and standards
   - Add complementary instructions in CLAUDE.md.local
   - Avoid conflicts with established patterns
   - Focus on additions rather than replacements

5. **Refresh Triggers**:
   Update both CLAUDE.md and CLAUDE.md.local when:
   - Major dependencies change
   - New services/components added
   - Build/test processes change
   - Architecture evolves
   - New team standards adopted

## Performance-First Development Approach
**Prioritize performance in:**
- Data processing (vectorized pandas/polars over loops)
- API endpoints (async/await, connection pooling)
- ML inference pipelines (batching, caching)
- Database queries (select only needed fields, proper indexing)

**Performance vs Readability Balance:**
```python
# Prefer this (vectorized)
df['result'] = df['values'].apply(complex_transform)

# Over this (iterative)
results = []
for value in df['values']:
    results.append(complex_transform(value))
df['result'] = results
```

**Readability priority for:**
- Configuration and setup code
- Test fixtures and helpers
- One-time migration scripts
- Documentation examples

## Generative AI Integration Patterns
- **LLM Client Management**: Async clients with connection pooling
- **Prompt Engineering**: Template-based prompts with pydantic validation
- **Response Processing**: Structured outputs with fallback parsing
- **Rate Limiting**: Implement backoff and retry logic
- **Cost Optimization**: Token counting, response caching
- **Monitoring**: Track usage, latency, and error rates

```python
# Example pattern
class LLMClient:
    def __init__(self, model: str, max_retries: int = 3):
        self.client = httpx.AsyncClient()
        self.model = model
        self.max_retries = max_retries
    
    async def generate(self, prompt: PromptTemplate) -> ParsedResponse:
        # Implementation with retries, validation, monitoring
        pass
```

## Development Workflow & Git Strategy
1. **Discovery**: Analyze existing project structure and requirements
2. **Planning**: Define interfaces and data models first
3. **Implementation**: Small, isolated changes with frequent commits
4. **Testing**: Write comprehensive unit tests, focused integration tests
5. **Integration**: Wire up external dependencies
6. **PR Preparation**: Each PR should contain a single feature/fix + tests + docs as a complete unit

**Commit Strategy:**
- Small, focused commits that build incrementally during development
- Each commit should pass tests and maintain working state
- Descriptive commit messages explaining the "why"
- Commit often to preserve development history
- **Squash commits before merging** to maintain clean project history
- **NEVER reference Claude as co-author in commits**

**Pull Request Structure:**
- Single feature or bug fix per PR
- Include unit and integration tests
- Update documentation (README, docstrings, etc.)
- Ensure all tests pass and code quality checks succeed
- **Squash and merge** to keep main branch history clean
- **NEVER reference Claude as co-author in PRs or code comments**

**Code Quality & Design Standards:**
- **Design Patterns**: Apply appropriate patterns (Factory, Strategy, Observer, etc.) for cleaner code organization
- **Testability**: Structure code to enable easy unit testing with clear separation of concerns
- **Error Handling**: Context-rich exceptions, graceful degradation
- **Logging**: Structured logging with correlation IDs
- **Typing**: Full type hints with pydantic models for data validation
- **Documentation**: Google-style docstrings for mkdocstrings compatibility

**Docstring Standards for mkdocstrings:**
```python
def process_data(data: List[Dict], config: ProcessingConfig) -> ProcessedResult:
    """Process input data according to configuration.
    
    Args:
        data: List of data dictionaries to process
        config: Processing configuration parameters
        
    Returns:
        Processed result with metadata and statistics
        
    Raises:
        ProcessingError: When data validation fails
        ConfigurationError: When config is invalid
        
    Examples:
        >>> config = ProcessingConfig(batch_size=100)
        >>> result = process_data([{"id": 1}], config)
        >>> result.success
        True
    """
```

**Testing Strategy:**
- **High Unit Test Coverage**: Focus on business logic, edge cases, error conditions
- **Clear Test Categories**: 
  - Unit tests: Fast, isolated, no external dependencies
  - Integration tests: Test component interactions, external services
  - End-to-end tests: Full workflow validation
  - Shell script tests: BATS-core for bash scripts, ShellCheck for static analysis
- **Test Structure**: Arrange-Act-Assert pattern with descriptive test names
- **Edge Cases**: Explicitly test boundary conditions, error states, and unusual inputs
- **Mocking**: Use dependency injection to enable easy mocking of external services

**Multi-Version Testing:**
- Use tox for standard multi-Python version testing
- Consider nox for complex environment matrices or custom test scenarios
- Test against minimum and maximum supported versions

## Architecture Patterns by Project Type

**CLI Tools:**
- Simple command structure with typer
- Rich output formatting
- Configuration via files + environment variables

**Web APIs:**
- FastAPI with automatic OpenAPI docs
- Pydantic models for request/response validation
- Middleware for logging, metrics, auth
- Async handlers for I/O operations

**ML Projects:**
- Separate training, evaluation, and inference codebases
- Feature stores for shared preprocessing
- Model registry with versioning
- Monitoring for drift and performance

**Full-Stack Applications:**
- Clear API boundaries between frontend/backend
- Shared type definitions (TypeScript interfaces)
- Docker composition for development environment

## Environment & Deployment
- **Package Management**: uv for dependency resolution and virtual environments
- **Task Automation**: Makefiles for common development workflows
- **GitHub Integration**: 
  - Use existing issue/PR templates in `.github/templates/`
  - Follow established workflows in `.github/workflows/`
  - Leverage GitHub Actions for CI/CD automation
- **Development**: docker-compose with hot reload
- **Dependencies**: uv.lock files for reproducible environments
- **Environment Variables**: .env for local, parameter store for production
- **Health Checks**: Implement proper health endpoints
- **Observability**: OpenTelemetry for metrics, structured logs

## Documentation Strategy
- **Primary Tool**: MkDocs + mkdocstrings for comprehensive documentation
- **Structure**: Follow Diátaxis framework (Tutorials, How-to Guides, Reference, Explanation)
- **API Documentation**: Auto-generated from docstrings using mkdocstrings
- **Narrative Documentation**: Written in Markdown for tutorials and guides
- **Live Preview**: Use `mkdocs serve` for real-time documentation updates
- **Theme**: Material for MkDocs for professional appearance
- **Deployment**: Automated via GitHub Actions to GitHub Pages or similar

**Documentation Configuration**:
```yaml
# mkdocs.yml
site_name: Project Name
theme:
  name: material
  features:
    - navigation.tabs
    - navigation.sections
    - toc.integrate
    - search.suggest
    - search.highlight

plugins:
  - search
  - mkdocstrings:
      handlers:
        python:
          options:
            docstring_style: google
            show_source: true
            show_root_heading: true
            merge_init_into_class: true

nav:
  - Home: index.md
  - Getting Started: getting-started.md
  - API Reference: reference/
  - How-to Guides: guides/
  - Changelog: changelog.md
```

## Implementation Guidelines

**Python Development:**
- **Design Patterns**: Use appropriate patterns (Dependency Injection, Factory, Strategy, Observer) for maintainable code
- **Composition over Inheritance**: Favor composition for flexibility
- **Dependency Injection**: Constructor injection for testability
- **Testable Architecture**: Structure code to enable easy unit testing
- **Input Validation**: Validate at system boundaries with pydantic
- **External Services**: Implement circuit breakers and retries
- **Caching**: Cache expensive operations (Redis, in-memory)
- **Security**: Follow least privilege for integrations
- **Resilience**: Graceful degradation for non-critical features
- **Immutability**: Use immutable data structures for shared state

**Example Testable Structure:**
```python
# Domain logic - easily testable
class OrderProcessor:
    def __init__(self, payment_service: PaymentService, inventory_service: InventoryService):
        self.payment_service = payment_service
        self.inventory_service = inventory_service
    
    def process_order(self, order: Order) -> OrderResult:
        # Pure business logic, easy to unit test
        pass

# Application service - integration testing
class OrderHandler:
    def __init__(self, processor: OrderProcessor):
        self.processor = processor
    
    async def handle_order_request(self, request: OrderRequest) -> OrderResponse:
        # Orchestration logic, integration testing
        pass
```
