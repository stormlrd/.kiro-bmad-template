# .kiro-bmad-template

A ready-to-use template for integrating BMAD (Breakthrough Method of Agile AI-driven Development) with Kiro IDE. This template provides a complete setup with 10 BMAD agents, automation hooks, and a specialized spec converter agent for transforming BMAD documents into formal Kiro specifications.

## What's Included

- **10 BMAD Agents**: PM, Architect, Developer, QA, PO, Analyst, UX Expert, SM, BMad Master, BMad Orchestrator
- **Kiro Spec Converter Agent**: Automated conversion from BMAD documents to Kiro specs
- **Automation Hooks**: Test sync, code standards, documentation sync, story validation, tech discovery
- **Context Files**: Technical preferences, project context, team standards
- **Error Handling**: Comprehensive error recovery for MCP, agents, and hooks
- **Methodology Guide**: Complete BMAD methodology reference

## Before You Begin

### Prerequisites

1. **Kiro IDE**: Install Kiro IDE from [kiro.dev](https://kiro.dev)

2. **BMAD Method**: Install BMAD globally for access to core resources
   ```bash
   # Clone BMAD repository
   git clone https://github.com/bmad-code-org/BMAD-METHOD.git
   
   # Set up BMAD in your global context
   # Follow instructions at: https://github.com/bmad-code-org/BMAD-METHOD
   ```

3. **Node.js** (Optional): For running validation scripts
   ```bash
   node --version  # Should be v18 or higher
   ```

4. **Git**: For version control
   ```bash
   git --version
   ```

## Quick Start

### 1. Create Your New Project

```bash
# Create your project directory
mkdir my-awesome-project
cd my-awesome-project

# Initialize git (optional but recommended)
git init
```

### 2. Copy the .kiro Folder

```bash
# Clone this template repository
git clone https://github.com/stormlrd/.kiro-bmad-template.git temp-template

# Copy the .kiro folder to your project
cp -r temp-template/.kiro .

# Copy the guide documents (optional but helpful)
cp temp-template/How-To-BMAD-With-Kiro.md .
cp temp-template/Kiro-Spec-Converter-Agent-Guide.md .

# Remove the temporary template folder
rm -rf temp-template
```

**Windows (PowerShell)**:
```powershell
# Clone this template repository
git clone https://github.com/stormlrd/.kiro-bmad-template.git temp-template

# Copy the .kiro folder to your project
Copy-Item -Recurse temp-template/.kiro .

# Copy the guide documents (optional but helpful)
Copy-Item temp-template/How-To-BMAD-With-Kiro.md .
Copy-Item temp-template/Kiro-Spec-Converter-Agent-Guide.md .

# Remove the temporary template folder
Remove-Item -Recurse -Force temp-template
```

### 3. Open in Kiro IDE

```bash
# Open your project in Kiro
kiro .
```

Or open Kiro IDE and use File → Open Folder to open your project directory.

### 4. Verify Setup

In Kiro chat, test that agents are available:

```
@bmad-master help
@kiro-spec-converter help
```

You should see the agents respond with their available commands.

## Project Structure

After copying the `.kiro` folder, your project will have:

```
your-project/
├── .kiro/
│   ├── hooks/                          # Automation hooks
│   │   ├── bmad-test-sync.kiro.hook
│   │   ├── bmad-code-standards.kiro.hook
│   │   ├── bmad-doc-sync.kiro.hook
│   │   ├── bmad-story-validation.kiro.hook
│   │   ├── bmad-tech-discovery.kiro.hook
│   │   └── bmad-spec-docs.kiro.hook
│   │
│   ├── settings/                       # Kiro settings
│   │   └── env-vars.json
│   │
│   ├── specs/                          # Kiro specs (created as you work)
│   │   └── _spec-overview-template.md
│   │
│   └── steering/                       # Agent configurations
│       ├── agents/                     # 10 BMAD agents + spec converter
│       │   ├── kiro-bmad-master-agent.md
│       │   ├── kiro-bmad-orchestrator-agent.md
│       │   ├── kiro-spec-converter-agent.md
│       │   └── ... (7 more agents)
│       │
│       ├── context/                    # Project context files
│       │   ├── technical-preferences.md
│       │   ├── frontend-preferences.md
│       │   ├── project-context.md
│       │   ├── team-standards.md
│       │   ├── mcp-error-handling.md
│       │   ├── agent-error-recovery.md
│       │   └── hook-error-handling.md
│       │
│       ├── bmad-method-guide.md        # Complete BMAD methodology
│       └── README.md                   # Steering system overview
│
├── docs/                               # BMAD planning documents (you create)
│   ├── prd.md
│   └── architecture.md
│
├── How-To-BMAD-With-Kiro.md           # Usage guide (optional)
└── Kiro-Spec-Converter-Agent-Guide.md # Spec converter guide (optional)
```

## Basic Workflow

### Option 1: Start with BMAD Planning

Use BMAD agents to create comprehensive planning documents:

```
1. @analyst research [your project idea]
2. @pm create a PRD for [your project]
3. @architect design the architecture for [your project]
```

Save these to `docs/prd.md` and `docs/architecture.md`

### Option 2: Convert to Kiro Specs

Use the spec converter to transform BMAD docs into formal Kiro specs:

```
@kiro-spec-converter convert-multi docs/prd.md
```

This will create multiple focused specs with:
- Foundation/core infrastructure
- Individual feature specs
- Dependency mapping
- Implementation order
- Master overview for tracking

### Option 3: Implement with Kiro or BMAD

**For correctness-critical features** (parsers, validation, state machines):
- Execute Kiro spec tasks
- Use property-based testing
- Validate correctness properties

**For UI/UX features** (components, layouts, interactions):
- Use BMAD SM → Dev → QA cycle
- Rapid iteration
- Subjective quality focus

## Customization

### Update Technical Preferences

Edit `.kiro/steering/context/technical-preferences.md` to match your stack:

```markdown
### Languages and Frameworks
- **Primary**: Node.js with TypeScript, Python with FastAPI, or Go
- **Database**: PostgreSQL for relational data, Redis for caching
- **API Style**: REST with OpenAPI specification
```

### Update Project Context

Edit `.kiro/steering/context/project-context.md` with your project details:

```markdown
### Project Name
Your Project Name

### Project Description
Your project description

### Project Goals
- Goal 1
- Goal 2
```

### Configure Team Standards

Edit `.kiro/steering/context/team-standards.md` for your team's practices:

```markdown
### Code Review Standards
- Mandatory Reviews: All code changes require at least one peer review
- Review Timeline: Reviews should be completed within 24 hours
```

## Available Agents

Activate any agent in Kiro chat with `@agent-name`:

- `@pm` - Product Manager (PRDs, strategy, prioritization)
- `@architect` - System Architect (design, architecture, technology)
- `@dev` - Developer (code implementation, debugging)
- `@qa` - QA Specialist (testing, quality assurance)
- `@po` - Product Owner (backlog, story refinement)
- `@analyst` - Business Analyst (research, analysis)
- `@ux` - UX Designer (UI/UX, user experience)
- `@sm` - Scrum Master (story creation, process)
- `@bmad-master` - Universal executor with all capabilities
- `@bmad-orchestrator` - Multi-agent workflow coordinator
- `@kiro-spec-converter` - BMAD to Kiro spec conversion

## Common Commands

### Spec Converter Commands

```bash
# Analyze BMAD documents and show feature breakdown
@kiro-spec-converter analyze-features docs/prd.md

# Create multiple specs from BMAD documents
@kiro-spec-converter convert-multi docs/prd.md

# Create single spec for simple feature
@kiro-spec-converter convert docs/feature-prd.md to a Kiro spec

# Show implementation order
@kiro-spec-converter dependency-order
```

### BMAD Master Commands

```bash
# Detect technologies in project
@bmad-master *detect-tech

# Suggest documentation servers
@bmad-master *suggest-docs

# System diagnostics
@bmad-master *validate
```

### BMAD Orchestrator Commands

```bash
# Analyze project for documentation needs
@bmad-orchestrator *analyze-project

# Manage MCP documentation servers
@bmad-orchestrator *manage-docs
```

## Troubleshooting

### Agents Not Responding

**Issue**: `@agent-name` not recognized

**Solution**: 
1. Restart Kiro IDE
2. Start a new chat session
3. Verify `.kiro/steering/agents/` folder exists

### Hooks Not Triggering

**Issue**: Automation hooks not executing

**Solution**:
1. Check hook configurations in `.kiro/hooks/`
2. Verify file patterns match your project structure
3. Check Kiro's hook execution logs

### MCP Servers Not Connecting

**Issue**: Documentation servers unavailable

**Solution**:
1. Check internet connection
2. Verify MCP configuration in `.kiro/settings/mcp.json`
3. Agents will automatically fall back to local resources

## Resources

- **BMAD Method**: https://github.com/bmad-code-org/BMAD-METHOD
- **Kiro IDE**: https://kiro.dev
- **Template Repository**: https://github.com/stormlrd/.kiro-bmad-template
- **Original Setup Tool**: https://github.com/bonarjs/kiro-bmad-setup

## Credits

- BMAD Method by [BMAD Code Org](https://github.com/bmad-code-org)
- Kiro IDE by [Kiro Team](https://kiro.dev)
- Template created by [stormlrd](https://github.com/stormlrd)
- Based on [kiro-bmad-setup](https://github.com/bonarjs/kiro-bmad-setup)

## License

This template is provided as-is for personal and commercial use. See LICENSE file for details.

---

# 
Complete Usage Guides

## How to Use BMAD with Kiro Specs

### Overview

This guide explains how to effectively combine BMAD's multi-agent methodology with Kiro's built-in Spec system. Both approaches are powerful, and understanding when to use each will maximize your development effectiveness.

### Understanding the Two Approaches

#### Kiro's Built-in Spec System

**Philosophy**: Formal correctness through property-based testing

**Key Features**:
- **EARS Requirements**: Structured acceptance criteria with formal patterns (WHEN/THEN/WHILE)
- **Correctness Properties**: Universal properties that must hold across all inputs
- **Property-Based Testing**: Automated validation with 100+ test iterations
- **Three-Phase Workflow**: Requirements → Design → Tasks
- **Single-Agent Execution**: Kiro executes tasks sequentially with tight integration
- **Native Task Tracking**: Built-in status updates, PBT validation, diagnostics

**Best For**:
- Features requiring formal correctness guarantees
- Parsers, serializers, and core algorithms
- Systems where bugs have high cost
- Features needing systematic property validation

#### BMAD Multi-Agent System

**Philosophy**: Natural language orchestration with specialized expertise

**Key Features**:
- **Specialized Agents**: 10 agents with distinct expertise (@pm, @architect, @dev, @qa, etc.)
- **Natural Language First**: Everything is markdown, minimal formalism
- **Document Sharding**: Break large documents into manageable development chunks
- **SM → Dev → QA Cycle**: Iterative story-based development
- **Flexible Templates**: YAML-based templates for various document types
- **Multi-Agent Workflows**: Orchestrate different perspectives and expertise

**Best For**:
- Early exploration and strategic planning
- Multi-faceted projects needing diverse expertise
- Brownfield projects requiring comprehensive documentation
- Large document creation (PRDs, architecture specs)
- Rapid iteration on UI/UX features

### The Hybrid Workflow (Recommended)

Combine both approaches to get the best of both worlds:

#### Phase 1: BMAD Planning (Pre-Spec)

Use BMAD agents for strategic planning and comprehensive documentation:

```
1. @analyst - Market research, competitive analysis, user research
2. @pm - Create comprehensive PRD with features and user stories
3. @architect - Design system architecture, data models, APIs
4. @ux - UI/UX specifications, user flows, design system (if needed)
```

**Output**: Rich planning documents in `docs/` folder
- `docs/prd.md` - Product Requirements Document
- `docs/architecture.md` - System Architecture
- `docs/ux-design.md` - User Experience Design (optional)

**Why BMAD First?**
- Multiple expert perspectives inform better requirements
- Large context windows (Gemini 1M tokens) handle comprehensive planning
- Natural language exploration before formal constraints
- Cost-effective for big-picture thinking

#### Phase 2: Kiro Spec Creation (Formalization)

Transform BMAD planning documents into formal Kiro specs:

```
1. Use BMAD docs as input to create Kiro spec
2. Transform PRD requirements into EARS format
3. Extract correctness properties from architecture
4. Create formal task list with PBT requirements
```

**Output**: `.kiro/specs/{feature}/` with:
- `requirements.md` - EARS-formatted requirements with acceptance criteria
- `design.md` - Design with correctness properties
- `tasks.md` - Implementation tasks with PBT validation

**Why Formalize?**
- EARS requirements ensure testability
- Correctness properties catch edge cases
- Property-based testing validates universal behavior
- Systematic task tracking prevents missed requirements

#### Phase 3: Implementation (Choose Your Path)

Pick the implementation approach based on feature characteristics:

**Option A: Kiro Native (Correctness-Critical Features)**

Use When:
- Feature involves parsing, serialization, or data transformation
- Correctness bugs would be costly or dangerous
- Need formal validation of universal properties
- Want tight integration with task tracking

Process:
1. Execute tasks through Kiro's built-in task execution
2. Leverage PBT integration and validation
3. Use Kiro for systematic implementation
4. Validate correctness properties automatically

**Option B: BMAD Cycle (Rapid Iteration Features)**

Use When:
- Feature is UI/UX focused with subjective quality
- Need rapid iteration and user feedback
- Correctness is less critical than user experience
- Want specialized agent expertise (UX, frontend)

Process:
1. @sm creates stories from sharded docs
2. @dev implements stories
3. @qa reviews and refactors
4. Iterate quickly based on feedback

### Decision Matrix

| Feature Characteristic | Use Kiro Spec | Use BMAD Cycle |
|------------------------|---------------|----------------|
| Parsing/Serialization | ✅ Yes | ❌ No |
| Data Validation | ✅ Yes | ❌ No |
| Security-Critical | ✅ Yes | ❌ No |
| Core Algorithms | ✅ Yes | ❌ No |
| UI Components | ❌ No | ✅ Yes |
| User Interactions | ❌ No | ✅ Yes |
| Visual Design | ❌ No | ✅ Yes |
| Content Management | ❌ No | ✅ Yes |

---

## Kiro Spec Converter Agent Guide

### The Solution You've Been Looking For

The `@kiro-spec-converter` agent is a specialized agent whose sole purpose is to take your BMAD docs and convert them to Kiro specs.

### The Simplest Workflows

#### Workflow 1: Multi-Spec Conversion (Recommended for Complex Projects)

**Best for**: Projects with multiple features, foundation infrastructure, or parallel development needs

**Step 1**: Create BMAD Documents (with BMAD agents)

```
@pm create a PRD for [your project]
@architect design the architecture for [your project]
```

Save these to `docs/[project]-prd.md` and `docs/[project]-architecture.md`

**Step 2**: Convert to Multiple Kiro Specs

```
@kiro-spec-converter convert-multi docs/[project]-prd.md
```

The agent will:
1. ✅ Read your BMAD documents
2. ✅ Identify foundation/core infrastructure
3. ✅ Extract distinct features from epics
4. ✅ Analyze dependencies between features
5. ✅ Recommend implementation order
6. ✅ Create separate specs for foundation + each feature
7. ✅ Generate master overview with dependency graph
8. ✅ Ask for your approval at each phase

**Result**: Multiple focused specs in `.kiro/specs/`:
```
.kiro/specs/
├── foundation/           # Core infrastructure
├── feature-1/           # First feature
├── feature-2/           # Second feature
├── feature-3/           # Third feature
└── _spec-overview.md    # Master overview
```

#### Workflow 2: Single-Spec Conversion (For Simple Features)

**Best for**: Single focused features, simple enhancements, or small projects

**Step 1**: Create BMAD Documents

```
@pm create a PRD for [your feature]
@architect design the architecture for [your feature]
```

**Step 2**: Convert to Single Kiro Spec

```
@kiro-spec-converter convert docs/[feature]-prd.md to a Kiro spec
```

The agent will:
1. ✅ Read your BMAD documents
2. ✅ Analyze which features need formal specs
3. ✅ Convert to EARS requirements
4. ✅ Extract correctness properties
5. ✅ Create implementation tasks with PBT
6. ✅ Ask for your approval at each phase

### Available Commands

#### Multi-Spec Conversion

```bash
# Full multi-spec conversion
@kiro-spec-converter convert-multi docs/[project]-prd.md

# Feature analysis only
@kiro-spec-converter analyze-features docs/[project]-prd.md

# Create foundation only
@kiro-spec-converter create-foundation docs/[project]-prd.md

# Create specific feature
@kiro-spec-converter create-feature docs/[project]-prd.md --feature "user-management"

# Show implementation order
@kiro-spec-converter dependency-order

# Generate/update overview
@kiro-spec-converter spec-overview
```

#### Single-Spec Conversion

```bash
# Full single-spec conversion
@kiro-spec-converter convert docs/[feature]-prd.md to a Kiro spec

# Step-by-step conversion
@kiro-spec-converter requirements docs/[feature]-prd.md
@kiro-spec-converter design
@kiro-spec-converter tasks
```

#### Analysis and Validation

```bash
# General analysis
@kiro-spec-converter analyze docs/[feature]-prd.md

# Identify critical features
@kiro-spec-converter identify-critical docs/[feature]-prd.md

# Extract properties
@kiro-spec-converter extract-properties

# Validate spec
@kiro-spec-converter validate-spec [feature-name]
```

### Why Use @kiro-spec-converter?

**Advantages**:
1. **Specialized Expertise**: Agent knows exactly how to convert BMAD → Kiro
2. **Automatic Feature Extraction**: Identifies foundation vs features automatically
3. **Dependency Analysis**: Maps dependencies and recommends implementation order
4. **Multi-Spec Structure**: Creates organized, focused specs for complex projects
5. **Guided Workflow**: Walks you through each phase with clear approvals
6. **Quality Assurance**: Validates EARS format, properties, traceability
7. **Consistent Results**: Same conversion rules every time
8. **Master Overview**: Generates tracking document with dependency graph
9. **Parallel Development**: Identifies opportunities for simultaneous work
10. **Clear Communication**: Explains reasoning and recommendations

### When to Use Multi-Spec Conversion

✅ **Use `convert-multi` when:**
- BMAD document contains multiple epics or features
- Project has foundation/infrastructure components
- Features have different priorities or timelines
- Multiple developers will work in parallel
- You want clear dependency mapping
- Project will grow with additional features
- You need organized, focused specs

### When to Use Single-Spec Conversion

✅ **Use `convert` when:**
- BMAD document describes one focused feature
- Feature is self-contained with minimal dependencies
- Project is small or experimental
- Single developer working sequentially
- Feature is an enhancement to existing system
- You prefer simpler structure

### Integration with BMAD Workflow

#### Complete Workflow for Complex Projects

```
Phase 1: BMAD Planning
├── @analyst research [project]
├── @pm create comprehensive PRD
├── @architect design system architecture
└── Save to docs/[project]-prd.md and docs/[project]-architecture.md

Phase 2: Multi-Spec Conversion
├── @kiro-spec-converter analyze-features docs/[project]-prd.md
├── Review feature breakdown and dependencies
├── @kiro-spec-converter convert-multi docs/[project]-prd.md
├── Approve spec structure
└── Review generated specs and overview

Phase 3: Foundation Implementation
├── Execute foundation spec tasks
├── Establish core infrastructure
├── Validate foundation properties
└── Mark foundation as complete

Phase 4: Feature Implementation (Parallel)
├── Execute feature spec tasks (based on dependencies)
├── Implement features with property-based testing
├── Track progress in _spec-overview.md
└── Use BMAD cycle for UI features

Phase 5: Integration and Polish
├── Integrate all features
├── Use BMAD cycle for remaining UI/UX work
├── Final testing and validation
└── Deploy
```

### Tips for Best Results

1. **Provide Good BMAD Documents**: Clear user stories, technical architecture, technology decisions, edge cases
2. **Be Specific About Focus**: Tell the agent what aspects to focus on
3. **Review Each Phase**: Read requirements, check properties, review tasks
4. **Iterate When Needed**: Ask for changes if something's not right

### Troubleshooting

**Agent Not Found**
```
Error: @kiro-spec-converter not recognized
```
Solution: Restart Kiro or start a new chat session

**Documents Not Found**
```
Agent: I can't find docs/[feature]-prd.md
```
Solution: Provide the correct path

**Conversion Too Broad**
```
Agent: This PRD covers too many features for one spec
```
Solution: Be specific about which feature to convert or use `convert-multi`

---

## Summary

This template provides everything you need to use BMAD methodology with Kiro IDE:

- **10 BMAD Agents** for specialized expertise
- **Kiro Spec Converter** for automated BMAD → Kiro conversion
- **Automation Hooks** for quality assurance
- **Context Files** for consistent standards
- **Complete Guides** for effective usage

**The Golden Rule**: Use BMAD for strategic planning and exploration, use Kiro Specs for tactical implementation with correctness guarantees.

Happy building! 🚀
