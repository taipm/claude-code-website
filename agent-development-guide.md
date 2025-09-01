# Agent Development Guide

## Overview

This guide provides comprehensive instructions for developing new Claude Code agents, from initial concept to production deployment. Follow these guidelines to create effective, maintainable agents that integrate seamlessly with the Claude Code ecosystem.

## Development Workflow

### Phase 1: Planning and Analysis

#### 1.1 Requirements Analysis

Use the `5w2h-analyzer` agent to systematically analyze the need for a new agent:

```bash
Task(subagent_type: "5w2h-analyzer",
     prompt: "Analyze the need for a new [DOMAIN] agent:
     - What specific tasks should it handle?
     - Why is a specialized agent needed?
     - When will it be used in workflows?
     - Where does it fit in the agent ecosystem?
     - Who will be the primary users?
     - How should it integrate with existing agents?
     - How much development effort is required?")
```

#### 1.2 Agent Specification

Define the following elements:

- **Agent Name**: kebab-case identifier (e.g., `data-analyst`)
- **Primary Purpose**: Single sentence describing main function
- **Scope and Boundaries**: What it does and doesn't do
- **Required Tools**: Minimum set of tools needed
- **Integration Points**: How it works with other agents

### Phase 2: Design and Creation

#### 2.1 Use Agent Builder

Leverage the `agent-builder` agent for creating the agent structure:

```bash
Task(subagent_type: "agent-builder",
     prompt: "Create a new agent with the following specifications:
     
     Name: [agent-name]
     Purpose: [detailed purpose description]
     
     Required capabilities:
     - [capability 1]
     - [capability 2]
     - [capability 3]
     
     Tools needed: [list of tools]
     Integration requirements: [how it works with other agents]
     
     Target use cases:
     - [use case 1]
     - [use case 2]
     - [use case 3]")
```

#### 2.2 Agent File Structure

Every agent follows this structure:

```markdown
---
name: agent-name
description: Brief description of agent purpose and capabilities (50-200 chars)
tools: Tool1, Tool2, Tool3
version: 1.0.0
category: classification
author: Agent Developer Name
created: YYYY-MM-DD
status: active
---

# Agent System Prompt

You are a [role] specialized in [domain/expertise].

## Purpose & Scope

[Detailed explanation of what this agent does]

## Workflow

When invoked:

1. **Step 1**: [Action description]
2. **Step 2**: [Decision point or analysis]
3. **Step 3**: [Output generation]

## [Additional sections as needed]
```

#### 2.3 Required Metadata Fields

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| `name` | ✅ | kebab-case identifier | `data-analyst` |
| `description` | ✅ | Purpose and capabilities | `Specialized data analysis and visualization agent` |
| `tools` | ✅ | Comma-separated tool list | `Read, Write, Edit, Glob, Grep, Bash` |
| `version` | ✅ | Semantic version | `1.0.0` |
| `category` | ✅ | Agent classification | `analysis`, `development`, `documentation` |
| `author` | ✅ | Creator identification | `Claude Code Agent Builder` |
| `created` | ✅ | Creation date | `2025-08-31` |
| `status` | ✅ | Current status | `active`, `beta`, `deprecated` |

### Phase 3: Implementation

#### 3.1 System Prompt Design

**Essential Components:**

1. **Role Definition**: Clear statement of what the agent is
2. **Purpose Statement**: Why this agent exists and what problems it solves
3. **Workflow Description**: Step-by-step process the agent follows
4. **Examples**: Real-world usage scenarios with inputs and expected outputs
5. **Error Handling**: How to handle edge cases and failures
6. **Integration Notes**: How to work with other agents

**Best Practices:**

- Use clear, specific language
- Include concrete examples
- Define boundaries and limitations
- Specify output formats
- Address common failure scenarios

#### 3.2 Tool Selection

Choose tools based on agent functionality:

**Available Tools:**
- **Read**: File reading and content analysis
- **Write**: Creating new files
- **Edit**: Modifying existing files
- **Glob**: File pattern matching and discovery
- **Grep**: Content searching and analysis
- **Bash**: System command execution

**Selection Guidelines:**

```bash
# Analysis-focused agents
tools: Read, Grep, Glob

# Generator agents  
tools: Read, Write, Edit, Glob

# System agents
tools: Read, Write, Edit, Bash

# Comprehensive agents
tools: Read, Write, Edit, Glob, Grep, Bash
```

#### 3.3 Workflow Patterns

**Pattern 1: Analyzer Pattern**
```markdown
## Workflow
1. **Discovery**: Find and read relevant files
2. **Analysis**: Examine content systematically  
3. **Pattern Recognition**: Identify insights
4. **Reporting**: Generate structured findings
```

**Pattern 2: Generator Pattern**
```markdown
## Workflow
1. **Requirements Gathering**: Understand what to create
2. **Template Selection**: Choose appropriate structure
3. **Content Generation**: Create the output
4. **Validation**: Verify quality and completeness
```

**Pattern 3: Optimizer Pattern**
```markdown
## Workflow
1. **Baseline Assessment**: Measure current state
2. **Improvement Identification**: Find optimization opportunities
3. **Solution Design**: Plan improvements
4. **Implementation**: Apply changes safely
5. **Validation**: Confirm improvements achieved
```

### Phase 4: Testing and Validation

#### 4.1 Functionality Testing

Use the `code-reviewer` agent to validate the agent implementation:

```bash
Task(subagent_type: "code-reviewer",
     prompt: "Review the new [agent-name] agent file for:
     - YAML frontmatter correctness
     - System prompt completeness
     - Workflow clarity
     - Integration considerations
     - Missing requirements")
```

#### 4.2 Permission Configuration

Add agent permissions to `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Task(your-agent-name:*)"
    ]
  }
}
```

#### 4.3 Integration Testing

Test the agent with real scenarios:

```bash
# Basic functionality test
Task(subagent_type: "your-agent-name",
     prompt: "Simple test request to verify basic functionality")

# Complex scenario test  
Task(subagent_type: "your-agent-name",
     prompt: "Complex real-world scenario that exercises multiple capabilities")

# Error handling test
Task(subagent_type: "your-agent-name", 
     prompt: "Edge case or invalid input to test error handling")
```

### Phase 5: Documentation and Deployment

#### 5.1 Agent Documentation

Use the `documentation-manager` agent to create comprehensive documentation:

```bash
Task(subagent_type: "documentation-manager",
     prompt: "Create documentation for the new [agent-name] agent including:
     - Purpose and capabilities overview
     - Usage examples and patterns
     - Integration with other agents
     - Best practices and troubleshooting")
```

#### 5.2 Deployment Checklist

- [ ] Agent file created in `.claude/agents/`
- [ ] YAML frontmatter validated
- [ ] System prompt comprehensive and tested
- [ ] Permissions configured in settings
- [ ] Basic functionality verified
- [ ] Integration patterns tested
- [ ] Documentation created
- [ ] Examples and use cases documented

## Agent Categories and Examples

### Analysis Agents
**Purpose**: Examine data, code, or systems to provide insights

**Examples**: 
- `5w2h-analyzer`: Systematic problem analysis
- `data-analyst`: Statistical analysis and visualization  
- `security-auditor`: Vulnerability assessment

**Typical Tools**: `Read, Grep, Glob, Bash`

### Generator Agents
**Purpose**: Create new content, code, or documentation

**Examples**:
- `python-developer`: Code generation and development
- `documentation-manager`: Technical writing and documentation
- `api-generator`: API endpoint and schema generation

**Typical Tools**: `Read, Write, Edit, Glob, Grep`

### Optimizer Agents  
**Purpose**: Improve existing systems, code, or processes

**Examples**:
- `database-optimizer`: Database performance tuning
- `code-optimizer`: Performance and efficiency improvements
- `resource-optimizer`: System resource optimization

**Typical Tools**: `Read, Write, Edit, Bash, Grep`

### Meta Agents
**Purpose**: Manage or create other agents and workflows

**Examples**:
- `agent-builder`: Create new specialized agents
- `workflow-orchestrator`: Coordinate multi-agent processes
- `quality-manager`: Oversee quality assurance processes

**Typical Tools**: `Read, Write, Edit, Glob, Grep, Bash`

## Best Practices

### Design Principles

1. **Single Responsibility**: Each agent should have one clear purpose
2. **Clear Boundaries**: Define what the agent does and doesn't do
3. **Integration Focused**: Design for collaboration with other agents
4. **User-Centric**: Optimize for actual user workflows and needs
5. **Maintainable**: Write clear, understandable system prompts

### Performance Optimization

1. **Efficient Tool Usage**: Only request tools actually needed
2. **Clear Instructions**: Reduce ambiguity in system prompts
3. **Structured Outputs**: Use consistent formatting for results
4. **Error Recovery**: Handle failures gracefully with helpful messages
5. **Context Management**: Keep interactions focused and relevant

### Quality Assurance

1. **Test Thoroughly**: Validate with real scenarios before deployment
2. **Document Completely**: Include usage examples and integration patterns
3. **Review Regularly**: Update agents based on usage feedback
4. **Monitor Performance**: Track success rates and user satisfaction
5. **Maintain Standards**: Follow established conventions and patterns

### Common Pitfalls

❌ **Avoid These Mistakes:**

- **Overly Broad Scope**: Trying to do too many different things
- **Insufficient Examples**: Not providing clear usage patterns
- **Tool Overload**: Requesting unnecessary tools "just in case"
- **Vague Instructions**: Using ambiguous language in system prompts
- **Poor Integration**: Not considering how agent fits in workflows
- **Missing Error Handling**: Not addressing failure scenarios
- **Inadequate Testing**: Deploying without proper validation

✅ **Follow These Practices:**

- **Focused Purpose**: Clear, specific agent responsibility
- **Rich Examples**: Multiple concrete usage scenarios
- **Minimal Tools**: Only tools directly needed for functionality
- **Precise Language**: Specific, actionable instructions
- **Ecosystem Awareness**: Designed for multi-agent workflows
- **Robust Handling**: Graceful failure management
- **Comprehensive Testing**: Validated with real scenarios

## Advanced Topics

### Agent Versioning

Use semantic versioning for agent evolution:

```yaml
version: 1.0.0  # Initial release
version: 1.1.0  # New features, backward compatible
version: 2.0.0  # Breaking changes
```

### Dynamic Behavior

Agents can adapt behavior based on context:

```markdown
## Context Adaptation

- **Project Type**: Adjust recommendations based on detected project type
- **User Experience**: Provide different detail levels based on expertise
- **Integration Mode**: Vary output format for different agent chains
```

### Performance Monitoring

Track agent effectiveness:

- **Success Rate**: Percentage of successful task completions
- **User Satisfaction**: Feedback scores and usage frequency  
- **Response Quality**: Accuracy and relevance of outputs
- **Integration Success**: Effectiveness in multi-agent workflows

### Agent Collaboration Patterns

Design agents to work together effectively:

**Sequential Processing**:
```
Agent A (Analysis) → Agent B (Implementation) → Agent C (Validation)
```

**Parallel Processing**:  
```
Input → [Agent A, Agent B, Agent C] → Aggregated Output
```

**Hierarchical Processing**:
```
Orchestrator Agent
├── Specialist Agent 1
├── Specialist Agent 2  
└── Quality Agent
```

## Troubleshooting

### Development Issues

**Agent Not Loading**
- Check YAML frontmatter syntax
- Verify required fields are present
- Ensure file is in correct location

**Permission Errors**
- Add agent to allowed permissions list
- Verify tool permissions are granted
- Check for typos in agent names

**Poor Performance** 
- Simplify system prompt language
- Reduce tool requirements
- Add more specific examples
- Test with smaller, focused requests

### Deployment Issues

**Integration Problems**
- Test agent in isolation first
- Verify compatibility with existing workflows
- Check for naming conflicts
- Validate tool access patterns

**User Adoption Issues**
- Improve documentation and examples
- Gather feedback on user experience
- Simplify usage patterns
- Provide clear value proposition

## Conclusion

Developing effective Claude Code agents requires careful planning, systematic implementation, and thorough testing. By following this guide and leveraging existing agents like `agent-builder`, `code-reviewer`, and `documentation-manager`, you can create powerful specialized agents that enhance the Claude Code ecosystem.

Remember to:
- Start with clear requirements analysis
- Design for integration and collaboration  
- Test thoroughly before deployment
- Document comprehensively for users
- Monitor and improve based on feedback

For specific technical questions, refer to the Technical Architecture Documentation or consult with experienced agent developers in your team.

---

*This guide is maintained by the documentation-manager agent and updated based on development experience and best practices.*