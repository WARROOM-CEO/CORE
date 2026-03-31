# Agents — WARROOM-CEO/CORE

## Overview

This document provides comprehensive guidance for working with **agents** in the WARROOM-CEO/CORE Claude Code environment. Agents are specialized subagents that can be invoked to handle specific tasks, workflows, or domains within your plugins.

---

## Agent File Structure & Naming

### Directory Location
All agent files must be placed in the `agents/` directory within your plugin:
```
plugin-name/
└── agents/
    ├── agent-name.md          # Primary agent instructions (English)
    └── agent-name-TH.md       # Thai translation for users (Thai)
```

### Naming Conventions
- **File names**: Use kebab-case (`my-agent-name.md`)
- **Agent names**: Must be unique within the plugin
- **Language suffix**: All localized agents must have `-TH` suffix for Thai translations
- **File extension**: Always use `.md` (Markdown)

### Bilingual Design Pattern
| File | Language | Used By | Purpose |
|------|----------|---------|---------|
| `agents/*.md` | English | Claude | Internal subagent instructions |
| `agents/*-TH.md` | Thai | Users | User-readable agent documentation |

**Important Rules:**
- Every `.md` file in `agents/` **must have a corresponding `-TH.md` pair**
- Exception: No exceptions for agent files (unlike README.md and LICENSE)
- All user-facing output from agents must be in **Thai (ภาษาไทย)**
- Internal logic, file paths, and technical values remain in English

---

## Agent File Format

### Required Structure
Each agent file (`agents/agent-name.md`) must follow this format:

```markdown
---
name: agent-name
description: Brief description of what this agent does and when to use it
---

# Agent Name

## Purpose
Clear explanation of the agent's primary function and scope.

## When to Use
Specific conditions, triggers, or contexts that should invoke this agent.

## Input Format
Expected input structure, parameters, or context the agent will receive.

## Output Format  
Expected output format, response structure, or actions the agent should produce.

## Workflow Steps
1. Step-by-step instructions for the agent to follow
2. Decision points and branching logic
3. Error handling and fallback procedures

## Examples
### Example 1: Basic Usage
**Input:** User request example
**Output:** Expected agent response

### Example 2: Complex Scenario  
**Input:** Complex user request
**Output:** Detailed agent response with multiple steps

## Constraints & Limitations
- What the agent should NOT do
- Security considerations
- Performance expectations
- Integration boundaries
```

### Thai Translation File
The corresponding `agents/agent-name-TH.md` file should contain a complete Thai translation of all user-facing content, formatted for easy reading and understanding by Thai users.

---

## Agent Types & Categories

### 1. Task-Specific Agents
Handle specific, well-defined tasks within a domain:
- **Code Review Agent**: Reviews code quality, security, and best practices
- **Documentation Agent**: Generates or improves documentation
- **Testing Agent**: Creates and executes test cases

### 2. Domain-Specialized Agents  
Focus on specific business domains or technical areas:
- **Finance Agent**: Handles financial calculations and analysis
- **Legal Agent**: Processes legal documents and compliance checks
- **HR Agent**: Manages human resources workflows

### 3. Workflow Orchestration Agents
Coordinate multiple steps or other agents:
- **Project Setup Agent**: Initializes new projects with proper structure
- **Migration Agent**: Handles data or code migrations between versions
- **Integration Agent**: Connects and configures external services

### 4. Quality Assurance Agents
Ensure quality and consistency:
- **Validation Agent**: Validates inputs, outputs, or configurations
- **Formatting Agent**: Ensures consistent code or document formatting
- **Compliance Agent**: Checks adherence to standards and policies

---

## Creating New Agents

### Step 1: Define Agent Scope
- Identify the specific problem or task the agent will solve
- Determine input requirements and expected outputs
- Define success criteria and quality metrics

### Step 2: Create Agent Files
1. Create `agents/your-agent-name.md` with English instructions
2. Create `agents/your-agent-name-TH.md` with Thai translation
3. Follow the required file format above

### Step 3: Implement Agent Logic
- Write clear, actionable instructions for Claude
- Include specific examples and edge cases
- Define constraints and limitations clearly
- Ensure all user-facing text will output in Thai

### Step 4: Test Agent Functionality
- Verify the agent works correctly in both English and Thai contexts
- Test with various input scenarios and edge cases
- Ensure proper error handling and fallback behavior

### Step 5: Document in Plugin README
- Update your plugin's README.md to include the new agent
- Explain when and how to use the agent
- Provide usage examples in Thai

---

## Best Practices

### Writing Effective Agent Instructions
- **Be Specific**: Avoid vague terms; use concrete examples and clear criteria
- **Use Imperative Voice**: Write instructions as direct commands ("Validate the input" not "You should validate the input")
- **Include Context**: Explain why certain steps are important or necessary
- **Handle Edge Cases**: Address common failure modes and unexpected inputs
- **Maintain Consistency**: Follow the same patterns and structures across all agents

### Performance Optimization
- **Minimize Context**: Keep agent files focused and concise (< 3000 words ideal)
- **Use References**: For detailed information, reference external files in `references/`
- **Cache Results**: When possible, store and reuse computed results
- **Parallel Processing**: Design agents to work efficiently with other concurrent agents

### Security Considerations
- **Never Expose Secrets**: Agents must not handle or log sensitive credentials
- **Validate Inputs**: Always validate and sanitize all inputs before processing
- **Limit Scope**: Restrict agent capabilities to only what's necessary for the task
- **Audit Trail**: Log agent activities appropriately for security monitoring

### Localization Guidelines
- **User-Facing Only**: Only translate content that users will read
- **Technical Terms**: Keep technical terms, file paths, and code in English
- **Cultural Context**: Adapt examples and explanations to Thai cultural context
- **Consistent Terminology**: Use consistent Thai terms across all localized files

---

## Integration with Skills

Agents work closely with skills in your plugin ecosystem:

### Skill-Agent Relationships
- **Skills invoke agents**: Skills can spawn agents to handle specific subtasks
- **Agents enhance skills**: Agents provide specialized capabilities that skills can leverage
- **Shared context**: Both skills and agents can access the same plugin resources

### Coordination Patterns
1. **Sequential**: Skill → Agent → Skill (for multi-step workflows)
2. **Parallel**: Skill spawns multiple agents simultaneously
3. **Conditional**: Skill decides which agent to invoke based on context
4. **Fallback**: Agent handles cases where skill logic is insufficient

### Resource Sharing
- Both skills and agents can access files in `references/`, `scripts/`, and `assets/`
- Use `${CLAUDE_PLUGIN_ROOT}` for portable path references
- Share MCP server connections and configurations

---

## Testing & Validation

### Agent Testing Framework
1. **Unit Tests**: Test individual agent functions with specific inputs
2. **Integration Tests**: Test agent interactions with skills and other agents  
3. **End-to-End Tests**: Test complete workflows involving multiple components
4. **Localization Tests**: Verify Thai output quality and accuracy

### Validation Checklist
- [ ] Agent file follows correct format and structure
- [ ] Thai translation file exists and is complete
- [ ] All user-facing output will be in Thai
- [ ] Technical terms and paths remain in English
- [ ] Examples are relevant and accurate
- [ ] Error handling is comprehensive
- [ ] Security considerations are addressed
- [ ] Performance is optimized for typical use cases

### Debugging Agents
- **Enable verbose logging**: Add debug information to understand agent behavior
- **Test incrementally**: Build and test agents step by step
- **Use mock data**: Test with controlled inputs to isolate issues
- **Monitor performance**: Track execution time and resource usage

---

## Common Agent Templates

### Template 1: Data Processing Agent
```markdown
---
name: data-processing-agent
description: Processes and transforms structured data according to specified rules
---

# Data Processing Agent

## Purpose
Transforms input data according to predefined rules and formats.

## When to Use
- When user requests data transformation or cleanup
- When importing data from external sources
- When preparing data for analysis or export

## Input Format
- Raw data (CSV, JSON, XML, or plain text)
- Transformation rules or specifications
- Target format requirements

## Output Format
- Cleaned and transformed data in specified format
- Processing summary and statistics
- Error report if applicable

## Workflow Steps
1. Parse input data and validate structure
2. Apply transformation rules sequentially
3. Validate transformed data against target schema
4. Format output according to specifications
5. Generate processing summary

[... rest of template ...]
```

### Template 2: Code Generation Agent
```markdown
---
name: code-generation-agent  
description: Generates code snippets or complete modules based on specifications
---

# Code Generation Agent

## Purpose
Creates functional code based on user requirements and specifications.

## When to Use
- When user requests code for specific functionality
- When implementing boilerplate or repetitive code patterns
- When creating code templates or scaffolds

## Input Format
- Functional requirements and specifications
- Target programming language and framework
- Style guidelines and constraints
- Existing code context (if applicable)

## Output Format
- Complete, functional code with proper syntax
- Inline comments explaining key decisions
- Usage examples and documentation
- Dependencies list if applicable

## Workflow Steps
1. Analyze requirements and identify key components
2. Select appropriate patterns and best practices
3. Generate code following specified style guidelines
4. Validate syntax and basic functionality
5. Add documentation and usage examples

[... rest of template ...]
```

---

## Troubleshooting

### Common Issues & Solutions

**Issue: Agent not being invoked**
- Solution: Check agent description for proper trigger phrases
- Solution: Verify agent file is in correct `agents/` directory
- Solution: Ensure agent name is unique within the plugin

**Issue: Thai output not working correctly**  
- Solution: Verify Thai Language Instruction Block is present in parent skill
- Solution: Check that Thai translation file exists and is properly formatted
- Solution: Ensure all user-facing text uses Thai characters

**Issue: Agent performance problems**
- Solution: Reduce agent file size by moving details to `references/`
- Solution: Optimize workflow steps to minimize unnecessary processing
- Solution: Implement caching for expensive operations

**Issue: Integration failures**
- Solution: Verify MCP server configurations are correct
- Solution: Check file path references use `${CLAUDE_PLUGIN_ROOT}`
- Solution: Ensure proper error handling for external service calls

### Support Resources
- **Plugin Documentation**: Refer to your plugin's README.md for specific guidance
- **Community Support**: Contact Poramate (WARROOM-CEO) at poramate@minsiri.com
- **Official Documentation**: Consult Claude Code official documentation for general agent patterns

---

## Version History

- **v1.0.0** (2026-03-31): Initial creation of agents.md guide
- **Maintenance**: This document should be updated whenever agent patterns or best practices change

> **Note**: This agents.md file serves as the authoritative guide for all agent-related development in the WARROOM-CEO/CORE ecosystem. All plugin developers must follow these guidelines to ensure consistency and quality across the plugin marketplace.