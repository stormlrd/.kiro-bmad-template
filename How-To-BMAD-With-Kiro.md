# How to Use BMAD with Kiro Specs

## Overview

This guide explains how to effectively combine BMAD's multi-agent methodology with Kiro's built-in Spec system. Both approaches are powerful, and understanding when to use each will maximize your development effectiveness.

## Understanding the Two Approaches

### Kiro's Built-in Spec System

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

### BMAD Multi-Agent System

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

## The Hybrid Workflow (Recommended)

Combine both approaches to get the best of both worlds:

### Phase 1: BMAD Planning (Pre-Spec)

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

### Phase 2: Kiro Spec Creation (Formalization)

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

### Phase 3: Implementation (Choose Your Path)

Pick the implementation approach based on feature characteristics:

#### Option A: Kiro Native (Correctness-Critical Features)

**Use When**:
- Feature involves parsing, serialization, or data transformation
- Correctness bugs would be costly or dangerous
- Need formal validation of universal properties
- Want tight integration with task tracking

**Process**:
1. Execute tasks through Kiro's built-in task execution
2. Leverage PBT integration and validation
3. Use Kiro for systematic implementation
4. Validate correctness properties automatically

**Example Features**:
- Message parser with round-trip validation
- Authentication system with security properties
- Data validation with invariant checking
- API serialization with format compliance

#### Option B: BMAD Cycle (Rapid Iteration Features)

**Use When**:
- Feature is UI/UX focused with subjective quality
- Need rapid iteration and user feedback
- Correctness is less critical than user experience
- Want specialized agent expertise (UX, frontend)

**Process**:
1. @sm creates stories from sharded docs
2. @dev implements stories
3. @qa reviews and refactors
4. Iterate quickly based on feedback

**Example Features**:
- UI components and layouts
- User interaction flows
- Visual design implementation
- Content management features

## Practical Example: Chat Application

Here's how to combine both approaches for a real project:

### Step 1: BMAD Planning

```
Chat with BMAD agents:

@analyst
Research chat protocols, analyze competitors (Slack, Discord, Teams).
What are the key features users expect? What are the technical standards?

@pm
Create a PRD for our chat application based on the analyst's research.
Include user stories, features, and success metrics.

@architect
Design the system architecture for the chat app. Consider:
- WebSocket vs polling for real-time messages
- Message storage and retrieval
- User authentication and presence
- Scalability for 10k concurrent users

@ux
Design the chat interface. Include:
- Message list and composition
- User presence indicators
- Notification patterns
- Mobile-responsive layout
```

**Result**: Comprehensive planning documents in `docs/`

### Step 2: Identify Critical Features for Kiro Specs

From the BMAD planning, identify features needing formal correctness:

**Critical Feature: Message Parser**
- Needs round-trip property (parse → serialize → parse = identity)
- Must handle edge cases (empty messages, special characters, large messages)
- Correctness bugs would corrupt message history

**Create Kiro Spec**:
```
Create a spec for the message parser:
- EARS requirements from PRD
- Correctness properties (round-trip, validation, encoding)
- PBT tasks for parser validation
```

**Result**: `.kiro/specs/message-parser/` with formal spec

### Step 3: Parallel Implementation

**Kiro Spec Execution** (Message Parser):
```
Execute tasks in .kiro/specs/message-parser/tasks.md
- Implement parser with correctness properties
- Write property-based tests
- Validate round-trip behavior
- Test edge cases automatically
```

**BMAD Cycle** (UI Components):
```
@sm
Create story for chat message component from docs/ux-design.md

@dev
Implement React component for displaying messages

@qa
Review component for accessibility, performance, and code quality

Repeat for:
- Message input component
- User list component
- Notification system
```

## Decision Matrix

Use this matrix to decide which approach for each feature:

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
| API Endpoints | ⚠️ Maybe | ⚠️ Maybe |
| Business Logic | ⚠️ Maybe | ⚠️ Maybe |

**Legend**:
- ✅ Strongly recommended
- ❌ Not recommended
- ⚠️ Depends on complexity and correctness requirements

## Integration Points

### BMAD Context Files Inform Kiro Specs

The BMAD context files are valuable for both approaches:

**Technical Preferences** (`.kiro/steering/context/technical-preferences.md`):
- Informs technology choices in Kiro spec design
- Guides implementation decisions
- Ensures consistency across approaches

**Project Context** (`.kiro/steering/context/project-context.md`):
- Provides project background for spec requirements
- Maintains alignment with project goals
- Tracks project evolution

**Team Standards** (`.kiro/steering/context/team-standards.md`):
- Defines code review standards for both approaches
- Establishes quality gates
- Ensures consistent practices

### BMAD Hooks Work with Kiro Specs

The BMAD automation hooks complement Kiro specs:

**Test Sync Hook** (`bmad-test-sync.hook`):
- Automatically syncs tests when code changes
- Works with both BMAD and Kiro implementations
- Maintains test coverage

**Code Standards Hook** (`bmad-code-standards.hook`):
- Applies coding standards automatically
- Ensures consistency across all code
- Works regardless of implementation approach

**Documentation Sync Hook** (`bmad-doc-sync.hook`):
- Keeps documentation updated
- Syncs with both BMAD docs and Kiro specs
- Maintains documentation quality

## Best Practices

### 1. Don't Mix During Execution

**❌ Don't Do This**:
```
Start executing Kiro spec tasks, then switch to @dev mid-implementation
```

**✅ Do This**:
```
Pick one approach per feature and stick with it through completion
```

**Why**: Mixing approaches creates confusion about task status, testing strategy, and completion criteria.

### 2. BMAD for Breadth, Kiro Specs for Depth

**BMAD Strength**: Exploring possibilities, gathering perspectives, creating comprehensive plans

**Kiro Spec Strength**: Systematic implementation, formal validation, correctness guarantees

**Strategy**: Use BMAD to explore the problem space broadly, then use Kiro specs to implement critical features deeply.

### 3. Leverage BMAD Templates as Spec Input

**BMAD Templates** → **Kiro Spec Requirements**

The BMAD templates generate excellent starting material:
- PRD user stories → EARS acceptance criteria
- Architecture decisions → Design constraints
- Success metrics → Testable properties

### 4. Use Fresh Context Windows

**BMAD Principle**: Always start new chat between SM, Dev, and QA work

**Kiro Principle**: Execute one task at a time with clear status tracking

**Combined**: Keep contexts clean and focused regardless of approach

### 5. Document the Approach Choice

In your spec or story, document why you chose each approach:

```markdown
## Implementation Approach

**Feature**: Message Parser
**Approach**: Kiro Spec with Property-Based Testing
**Rationale**: 
- Parsing requires round-trip correctness
- Edge cases are numerous and hard to enumerate
- PBT will catch unexpected input combinations
- Formal validation prevents message corruption

**Feature**: Chat UI Components
**Approach**: BMAD SM → Dev → QA Cycle
**Rationale**:
- UI quality is subjective and iterative
- Need rapid feedback and refinement
- UX expertise from specialized agents
- Correctness less critical than user experience
```

## Common Patterns

### Pattern 1: BMAD Planning → Multiple Kiro Specs

One BMAD planning phase can spawn multiple Kiro specs:

```
BMAD Planning (E-commerce Platform)
├── docs/prd.md
├── docs/architecture.md
└── docs/ux-design.md

↓ Formalize Critical Features ↓

Kiro Specs:
├── .kiro/specs/payment-processor/     (Correctness-critical)
├── .kiro/specs/inventory-validator/   (Correctness-critical)
└── .kiro/specs/order-state-machine/   (Correctness-critical)

BMAD Cycles:
├── Product catalog UI
├── Shopping cart interface
└── User account management
```

### Pattern 2: Kiro Spec with BMAD QA Review

Use Kiro spec for implementation, then BMAD QA for comprehensive review:

```
1. Execute Kiro spec tasks (implementation + PBT)
2. @qa comprehensive review
   - Code quality and patterns
   - Integration concerns
   - Performance considerations
   - Security review
3. Refactor based on QA feedback
4. Final validation with Kiro PBT
```

### Pattern 3: BMAD Brownfield → Kiro Greenfield

For existing projects, use BMAD to document, then Kiro for new features:

```
1. @bmad-master *detect-tech (analyze existing codebase)
2. Use brownfield-prd-tmpl to document current system
3. Create enhancement PRD with @pm
4. Formalize new features as Kiro specs
5. Implement with correctness guarantees
```

## Troubleshooting

### Issue: Unclear Which Approach to Use

**Solution**: Ask these questions:
1. Does this feature involve parsing, serialization, or data transformation? → Kiro Spec
2. Is correctness more important than iteration speed? → Kiro Spec
3. Do I need multiple expert perspectives? → BMAD
4. Is this UI/UX focused? → BMAD
5. When in doubt, start with BMAD planning, then decide

### Issue: BMAD Docs Don't Map to EARS Requirements

**Solution**: Use @pm to refine requirements:
```
@pm
Review these user stories and convert them to EARS format:
- WHEN [trigger], THE [system] SHALL [response]
- WHILE [condition], THE [system] SHALL [response]
```

### Issue: Kiro Spec Feels Too Formal for Simple Feature

**Solution**: You're probably right. Use BMAD cycle for simple features:
- Simple CRUD operations
- Basic UI components
- Straightforward integrations
- Features without complex edge cases

### Issue: Lost Track of What's Implemented Where

**Solution**: Maintain an implementation log:

```markdown
# Implementation Log

## Kiro Specs (Formal Validation)
- [x] Message Parser (.kiro/specs/message-parser/)
- [x] Authentication System (.kiro/specs/auth-system/)
- [ ] Order State Machine (.kiro/specs/order-fsm/)

## BMAD Cycles (Rapid Iteration)
- [x] Chat UI Components (stories 1-5 complete)
- [x] User Profile Pages (stories 1-3 complete)
- [ ] Admin Dashboard (story 1 in progress)

## Hybrid Approach
- [x] API Endpoints (Kiro spec for validation, BMAD for implementation)
```

## Summary

**The Golden Rule**: Use BMAD for strategic planning and exploration, use Kiro Specs for tactical implementation with correctness guarantees.

**Quick Reference**:
- **Planning Phase**: Always start with BMAD agents
- **Critical Features**: Formalize as Kiro specs with PBT
- **Rapid Iteration**: Use BMAD SM → Dev → QA cycle
- **Context Files**: Leverage for both approaches
- **Hooks**: Work with both approaches
- **Don't Mix**: Pick one approach per feature

**Remember**: These approaches are complementary, not competitive. BMAD gives you the strategic thinking and comprehensive planning, while Kiro Specs give you the formal correctness and systematic validation. Together, they create a powerful development workflow.

## Next Steps

1. **Try the Hybrid Workflow**: Pick a feature and go through all three phases
2. **Create Your First Formal Spec**: Take a BMAD PRD and formalize one critical feature
3. **Set Up Context Files**: Ensure your technical preferences are documented
4. **Configure Hooks**: Enable BMAD hooks to work alongside Kiro specs
5. **Document Your Patterns**: Track what works for your team and project

Happy building! 🚀
