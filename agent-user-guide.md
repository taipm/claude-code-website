# Claude Code Agents User Guide

## Introduction

Claude Code agents are specialized AI assistants designed to handle specific types of tasks with expertise and efficiency. This guide will help you understand how to use the available agents effectively.

## Quick Start

### Basic Agent Usage

To use an agent, employ the Task tool with the appropriate subagent_type:

```bash
Task(subagent_type: "agent-name", prompt: "Your specific request")
```

### Available Agents Overview

| Agent | Best For | Example Use Cases |
|-------|----------|-------------------|
| `5w2h-analyzer` | Problem analysis | Project planning, root cause analysis, decision making |
| `agent-builder` | Creating agents | Building new specialized agents, agent optimization |
| `code-reviewer` | Code quality | Security review, performance analysis, best practices |
| `python-developer` | Python development | Feature development, debugging, optimization |
| `documentation-manager` | Documentation | API docs, technical writing, research papers |
| `database-optimizer` | Database performance | Query optimization, index strategy, performance tuning |

## Agent Detailed Guide

### 1. 5W2H Analyzer Agent

**Purpose**: Systematic problem analysis using the 5W2H methodology (What, Why, When, Where, Who, How, How much)

**When to Use**:
- Planning new projects or features
- Investigating problems or issues
- Making complex decisions
- Analyzing processes for improvement

**Example Usage**:
```bash
Task(subagent_type: "5w2h-analyzer", 
     prompt: "Analyze our slow database performance issue that started last week")
```

**Expected Output**:
- Comprehensive analysis across all 7 dimensions
- Action plan with specific steps
- Risk assessment and mitigation strategies
- Resource requirements and timeline

**Pro Tips**:
- Provide as much context as possible
- Include specific metrics and data when available
- Ask for follow-up analysis on specific dimensions if needed

### 2. Agent Builder Agent

**Purpose**: Meta-agent specialized in creating new Claude Code agents

**When to Use**:
- Need a new specialized agent for specific domain
- Want to optimize existing agent configurations
- Creating agent templates for team use

**Example Usage**:
```bash
Task(subagent_type: "agent-builder",
     prompt: "Create a security-audit agent for penetration testing and vulnerability assessment")
```

**Expected Output**:
- Complete agent file with proper YAML frontmatter
- Comprehensive system prompt with workflows
- Integration guidelines and examples
- Testing and validation procedures

**Pro Tips**:
- Be specific about the agent's intended use cases
- Specify required tools and capabilities
- Include examples of expected interactions

### 3. Code Reviewer Agent

**Purpose**: Expert code review focusing on quality, security, and maintainability

**When to Use**:
- Before merging pull requests
- During security audits
- When optimizing code performance
- Establishing coding standards

**Example Usage**:
```bash
Task(subagent_type: "code-reviewer",
     prompt: "Review the new authentication module for security vulnerabilities")
```

**Expected Output**:
- Structured review report with severity ratings
- Specific security and quality issues identified
- Actionable recommendations with code examples
- Overall score and merge recommendation

**Pro Tips**:
- Run after making significant code changes
- Provide context about the code's purpose
- Ask for specific focus areas (security, performance, etc.)

### 4. Python Developer Agent

**Purpose**: Expert Python development with modern practices and optimization

**When to Use**:
- Developing new Python features
- Debugging Python code issues
- Optimizing Python performance
- Setting up Python projects

**Example Usage**:
```bash
Task(subagent_type: "python-developer",
     prompt: "Optimize this slow data processing function that handles 1M+ records")
```

**Expected Output**:
- Optimized code with performance improvements
- Comprehensive testing strategy
- Modern Python best practices applied
- Performance benchmarks and measurements

**Pro Tips**:
- Include current code and performance metrics
- Specify target Python version and frameworks
- Mention any constraints (memory, time, dependencies)

### 5. Documentation Manager Agent

**Purpose**: Technical and scientific documentation specialist

**When to Use**:
- Creating API documentation
- Writing technical specifications
- Generating user guides
- Preparing research documentation

**Example Usage**:
```bash
Task(subagent_type: "documentation-manager",
     prompt: "Create comprehensive API documentation for our user management system")
```

**Expected Output**:
- Well-structured documentation in appropriate format
- Cross-referenced sections and navigation
- Code examples and usage scenarios
- Professional formatting and style

**Pro Tips**:
- Specify target audience (developers, end-users, researchers)
- Include preferred format (Markdown, LaTeX, etc.)
- Provide existing code or specifications to document

### 6. Database Optimizer Agent

**Purpose**: Database performance optimization and query tuning

**When to Use**:
- Slow database queries need optimization
- Planning database schema changes
- Performance monitoring and tuning
- Database migration strategies

**Example Usage**:
```bash
Task(subagent_type: "database-optimizer",
     prompt: "Optimize our e-commerce database that has 2-second query times on product searches")
```

**Expected Output**:
- Detailed performance analysis
- Specific optimization recommendations
- Safe implementation procedures with rollback plans
- Performance improvement projections

**Pro Tips**:
- Include database type, size, and current performance metrics
- Provide example slow queries when possible
- Specify production constraints and maintenance windows

## Advanced Usage Patterns

### Agent Chaining

Use multiple agents in sequence for complex workflows:

```bash
# 1. Analyze requirements
Task(subagent_type: "5w2h-analyzer", 
     prompt: "Analyze requirements for new user dashboard feature")

# 2. Develop the feature
Task(subagent_type: "python-developer",
     prompt: "Implement user dashboard based on the analysis above")

# 3. Review the code
Task(subagent_type: "code-reviewer",
     prompt: "Review the dashboard implementation for quality and security")

# 4. Document the feature
Task(subagent_type: "documentation-manager",
     prompt: "Create user guide and API docs for the new dashboard")
```

### Parallel Analysis

Use multiple agents to analyze different aspects simultaneously:

```bash
# Analyze from different perspectives
Task(subagent_type: "5w2h-analyzer", prompt: "Business analysis of performance issue")
Task(subagent_type: "database-optimizer", prompt: "Technical database analysis")
Task(subagent_type: "python-developer", prompt: "Application code analysis")
```

### Iterative Improvement

Use agents iteratively to refine solutions:

```bash
# Initial implementation
Task(subagent_type: "python-developer", prompt: "Create initial solution")

# Review and identify issues
Task(subagent_type: "code-reviewer", prompt: "Review initial implementation")

# Refine based on feedback
Task(subagent_type: "python-developer", prompt: "Address review feedback and optimize")
```

## Best Practices

### Effective Prompting

1. **Be Specific**: Provide clear, detailed requirements
2. **Include Context**: Share relevant background information
3. **Set Expectations**: Specify desired output format and depth
4. **Provide Examples**: Include sample inputs or expected outputs when helpful

### Agent Selection

1. **Match Expertise**: Choose the agent best suited for your task type
2. **Consider Scope**: Use specialized agents for focused tasks
3. **Think Sequentially**: Plan multi-step workflows with appropriate agents
4. **Leverage Strengths**: Understand each agent's particular capabilities

### Workflow Optimization

1. **Start Broad**: Use 5w2h-analyzer for initial analysis
2. **Get Specific**: Move to specialized agents for implementation
3. **Validate Quality**: Always review with code-reviewer for important changes
4. **Document Results**: Use documentation-manager for formal documentation

## Troubleshooting

### Common Issues

#### Agent Not Found
```
Error: Agent type 'agent-name' not found
```
**Solution**: Verify agent name spelling and check available agents list

#### Insufficient Context
**Symptom**: Generic or incomplete responses
**Solution**: Provide more specific context and requirements

#### Wrong Agent Choice
**Symptom**: Response doesn't match expectations
**Solution**: Review agent capabilities and choose more appropriate specialist

#### Permission Issues
**Symptom**: Tool access errors
**Solution**: Check agent permissions in configuration files

### Getting Help

1. **Check Documentation**: Review this guide and technical architecture docs
2. **Analyze Examples**: Look at successful usage patterns
3. **Start Simple**: Begin with basic requests before complex workflows
4. **Iterate**: Refine prompts based on agent responses

## Performance Tips

### Optimize Request Efficiency

1. **Batch Related Tasks**: Group similar requests to the same agent
2. **Provide Complete Information**: Avoid back-and-forth by including all necessary details
3. **Use Appropriate Detail Level**: Match request complexity to actual needs
4. **Cache Results**: Save agent outputs for reference in related tasks

### Resource Management

1. **Choose Right Tool**: Don't use heavyweight agents for simple tasks
2. **Monitor Usage**: Track which agents provide best value for your use cases
3. **Plan Workflows**: Design efficient multi-agent sequences
4. **Validate Early**: Use quick validation before expensive operations

## Examples and Templates

### Project Planning Template
```bash
# Step 1: Requirements Analysis
Task(subagent_type: "5w2h-analyzer",
     prompt: "Analyze requirements for [PROJECT NAME]: [DESCRIPTION]
     
     Context:
     - Business goals: [GOALS]
     - Constraints: [CONSTRAINTS]
     - Timeline: [TIMELINE]
     - Resources: [RESOURCES]")

# Step 2: Technical Planning  
Task(subagent_type: "python-developer",
     prompt: "Based on the analysis above, create technical implementation plan")

# Step 3: Documentation
Task(subagent_type: "documentation-manager", 
     prompt: "Create project specification document based on analysis and technical plan")
```

### Code Quality Workflow
```bash
# Step 1: Implementation
Task(subagent_type: "python-developer",
     prompt: "Implement [FEATURE] with the following requirements: [REQUIREMENTS]")

# Step 2: Review
Task(subagent_type: "code-reviewer",
     prompt: "Review the implementation above for security, performance, and maintainability")

# Step 3: Optimization
Task(subagent_type: "python-developer",
     prompt: "Address the review feedback and optimize the implementation")
```

### Database Performance Analysis
```bash
# Step 1: Problem Analysis
Task(subagent_type: "5w2h-analyzer",
     prompt: "Analyze database performance degradation:
     - Symptoms: [SYMPTOMS]
     - Timeline: [WHEN_STARTED]
     - Impact: [BUSINESS_IMPACT]")

# Step 2: Technical Investigation
Task(subagent_type: "database-optimizer",
     prompt: "Investigate and optimize database performance based on analysis above")

# Step 3: Documentation
Task(subagent_type: "documentation-manager",
     prompt: "Document the performance issue, solution, and prevention measures")
```

## Conclusion

Claude Code agents provide powerful specialized capabilities for software development, analysis, and documentation tasks. By understanding each agent's strengths and using effective prompting techniques, you can significantly improve your productivity and output quality.

Remember to:
- Choose the right agent for each task
- Provide clear, detailed context
- Use agents in logical sequences
- Document and share successful patterns

For more advanced usage and technical details, refer to the Technical Architecture Documentation.

---

*This guide is maintained by the documentation-manager agent. For updates or improvements, please provide feedback through the appropriate channels.*