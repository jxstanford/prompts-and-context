# Development Context & Prompts

A curated collection of development context files, AI assistant instructions, and project templates for consistent software engineering workflows.

## Contents

### Code Context
- **[CLAUDE.md](code/CLAUDE.md)** - Comprehensive development instructions for Claude Code, including technology stack preferences, architectural patterns, and workflow guidelines
- **[mcp-llms-full.md](code/mcp-llms-full.md)** - Model Context Protocol (MCP) client reference and feature support matrix

### AI Agents
- **[tech_writer.md](agents/tech_writer.md)** - Technical writer agent instructions with document type standards and structured writing guidelines for SOPs, process docs, technical specs, user guides, and troubleshooting guides

### Templates
- **[pull-request-template.md](templates/pull-request-template.md)** - GitHub PR template with standardized checklist and structure

## Usage

### Claude Code Integration
The `code/CLAUDE.md` file contains detailed instructions for:
- Project discovery and analysis patterns
- Technology stack preferences (Python, TypeScript, FastAPI, etc.)
- Development workflows and git strategies
- Code quality standards and testing approaches
- Documentation and deployment practices

Place this file in your project root or reference it for consistent development practices across projects.

### AI Agent Specifications
The `agents/tech_writer.md` file provides comprehensive instructions for technical writing tasks, including:
- Document type selection framework (SOPs, Process Docs, Technical Specs, User Guides, Troubleshooting)
- Structured templates for each document type
- Quality standards and maintenance protocols
- Writing guidelines and success metrics

### MCP Reference
The MCP documentation provides a comprehensive overview of Model Context Protocol support across various AI development tools and editors.

## Repository Structure
```
├── agents/                  # AI agent instructions and specifications
│   └── tech_writer.md      # Technical writing agent with document standards
├── code/                    # Development context and instructions
│   ├── CLAUDE.md           # Primary development instructions
│   └── mcp-llms-full.md    # MCP client reference
├── templates/              # Project templates
│   └── pull-request-template.md
└── LICENSE                 # MIT License
```

## Contributing

This repository serves as a reference collection. To contribute:
1. Follow the established template structure
2. Ensure all content follows defensive security practices
3. Update this README when adding new content

## License

MIT License - see [LICENSE](LICENSE) file for details.
