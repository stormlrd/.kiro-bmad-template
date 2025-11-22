# @spec-converter Agent - Your BMAD to Kiro Spec Automation

## The Solution You've Been Looking For

You asked: "Is there an agent that does this job?"

**YES!** I just created `@spec-converter` - a specialized agent whose sole purpose is to take your BMAD docs and convert them to Kiro specs.

## The Simplest Workflows

### Workflow 1: Multi-Spec Conversion (Recommended for Complex Projects)

**Best for**: Projects with multiple features, foundation infrastructure, or parallel development needs

#### Step 1: Create BMAD Documents (with BMAD agents)

```
@pm create a PRD for [your project]
@architect design the architecture for [your project]
```

Save these to `docs/[project]-prd.md` and `docs/[project]-architecture.md`

#### Step 2: Convert to Multiple Kiro Specs (with @spec-converter)

```
@spec-converter convert-multi docs/[project]-prd.md
```

**That's it!** The agent will:
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

### Workflow 2: Single-Spec Conversion (For Simple Features)

**Best for**: Single focused features, simple enhancements, or small projects

#### Step 1: Create BMAD Documents (with BMAD agents)

```
@pm create a PRD for [your feature]
@architect design the architecture for [your feature]
```

Save these to `docs/[feature]-prd.md` and `docs/[feature]-architecture.md`

#### Step 2: Convert to Single Kiro Spec (with @spec-converter)

```
@spec-converter convert docs/[feature]-prd.md to a Kiro spec
```

**That's it!** The agent will:
1. ✅ Read your BMAD documents
2. ✅ Analyze which features need formal specs
3. ✅ Convert to EARS requirements
4. ✅ Extract correctness properties
5. ✅ Create implementation tasks with PBT
6. ✅ Ask for your approval at each phase

**Result**: Single focused spec in `.kiro/specs/[feature-name]/`

## Available Commands

### Multi-Spec Conversion (Recommended for Complex Projects)

#### Full Multi-Spec Conversion
```
@spec-converter convert-multi docs/[project]-prd.md
```
Analyzes BMAD docs and creates multiple specs (foundation + features) with master overview.

#### Feature Analysis Only
```
@spec-converter analyze-features docs/[project]-prd.md
```
Shows feature breakdown, dependencies, and recommended spec structure without creating specs.

#### Create Foundation Only
```
@spec-converter create-foundation docs/[project]-prd.md
```
Creates only the foundation/core infrastructure spec. Useful for starting with infrastructure first.

#### Create Specific Feature
```
@spec-converter create-feature docs/[project]-prd.md --feature "user-management"
```
Creates a single feature spec from the BMAD documents.

#### Show Implementation Order
```
@spec-converter dependency-order
```
Shows recommended implementation order based on dependencies between specs.

#### Generate/Update Overview
```
@spec-converter spec-overview
```
Generates or updates the master `_spec-overview.md` file with current progress.

### Single-Spec Conversion (For Simple Features)

#### Full Single-Spec Conversion
```
@spec-converter convert docs/[feature]-prd.md to a Kiro spec
```
The agent will guide you through the entire workflow automatically.

#### Step-by-Step Conversion
```
@spec-converter requirements docs/[feature]-prd.md
[Review and approve]

@spec-converter design
[Review and approve]

@spec-converter tasks
[Review and approve]
```

### Analysis and Validation

#### General Analysis
```
@spec-converter analyze docs/[feature]-prd.md
```
Get recommendations on which features need formal specs vs BMAD cycle.

#### Identify Critical Features
```
@spec-converter identify-critical docs/[feature]-prd.md
```
Help identify which features need formal specs vs rapid iteration.

#### Extract Properties
```
@spec-converter extract-properties
```
Extract correctness properties from requirements.

#### Validate Spec
```
@spec-converter validate-spec [feature-name]
```
Validate created spec for completeness and correctness.

### Utility Commands

```
@spec-converter help
@spec-converter status
```

## Real Examples

### Example 1: Multi-Spec Conversion (E-commerce Platform)

This example shows how to convert a complex BMAD document with multiple features into separate, focused specs.

#### What You Say:
```
@spec-converter convert-multi docs/ecommerce-prd.md
```

#### What the Agent Does:

**Phase 1: Feature Extraction and Analysis**
```
🔄 Analyzing BMAD Documents for Multi-Spec Conversion

Reading:
- docs/ecommerce-prd.md
- docs/ecommerce-architecture.md

## Multi-Spec Analysis Results

### Foundation/Core Components
**Recommended Spec**: `.kiro/specs/foundation/`
- PostgreSQL database schema and migrations
- JWT authentication and session management
- Express API middleware and error handling
- Shared validation utilities
- Configuration management

**Priority**: Must be implemented first
**Why Separate**: All features depend on this infrastructure

### Feature 1: Product Catalog
**Recommended Spec**: `.kiro/specs/product-catalog/`
- Product CRUD operations with validation
- Category management and hierarchy
- Product search and filtering
- Image upload and storage

**Dependencies**: Foundation (database, API, auth)
**Priority**: High (core business feature)
**Correctness Focus**: Product validation, search accuracy

### Feature 2: Shopping Cart
**Recommended Spec**: `.kiro/specs/shopping-cart/`
- Cart state management
- Item addition/removal with validation
- Quantity limits and stock checking
- Cart persistence and recovery

**Dependencies**: Foundation, Product Catalog
**Priority**: High (core business feature)
**Correctness Focus**: Cart state consistency, quantity validation

### Feature 3: Order Processing
**Recommended Spec**: `.kiro/specs/order-processing/`
- Order creation and validation
- Payment integration (Stripe)
- Order state machine (pending → paid → shipped → delivered)
- Inventory updates and rollback

**Dependencies**: Foundation, Shopping Cart
**Priority**: High (core business feature)
**Correctness Focus**: State machine correctness, payment safety

### Feature 4: Admin Dashboard
**Recommended Spec**: `.kiro/specs/admin-dashboard/`
- Admin authentication and permissions
- Product management interface
- Order management and fulfillment
- Analytics and reporting

**Dependencies**: Foundation, Product Catalog, Order Processing
**Priority**: Medium (can be built after core features)
**Correctness Focus**: Permission validation, data integrity

### Features for BMAD Cycle (Not Specs)
- Product image gallery UI
- Customer reviews and ratings
- Email notification templates
- Marketing landing pages

## Recommended Spec Structure
```
.kiro/specs/
├── foundation/
├── product-catalog/
├── shopping-cart/
├── order-processing/
├── admin-dashboard/
└── _spec-overview.md
```

## Recommended Implementation Order
1. Foundation (must be first)
2. Product Catalog (can start after foundation)
3. Shopping Cart (can start after product-catalog)
4. Order Processing (requires shopping-cart)
5. Admin Dashboard (requires all features)

## Parallel Development Opportunities
- Product Catalog and Shopping Cart can be developed simultaneously after Foundation

Shall I create all 5 specs with this structure?
```

**You:** Yes, create all specs

**Phase 2-4: Spec Creation**
```
🔄 Creating Multi-Spec Structure

Creating foundation spec...
✅ .kiro/specs/foundation/requirements.md (12 requirements, 48 criteria)
✅ .kiro/specs/foundation/design.md (15 properties)
✅ .kiro/specs/foundation/tasks.md (8 main tasks, 24 sub-tasks)

Creating feature specs...
✅ .kiro/specs/product-catalog/requirements.md (8 requirements, 32 criteria)
✅ .kiro/specs/product-catalog/design.md (12 properties)
✅ .kiro/specs/product-catalog/tasks.md (6 main tasks, 18 sub-tasks)

✅ .kiro/specs/shopping-cart/requirements.md (6 requirements, 24 criteria)
✅ .kiro/specs/shopping-cart/design.md (10 properties)
✅ .kiro/specs/shopping-cart/tasks.md (5 main tasks, 15 sub-tasks)

✅ .kiro/specs/order-processing/requirements.md (10 requirements, 40 criteria)
✅ .kiro/specs/order-processing/design.md (18 properties)
✅ .kiro/specs/order-processing/tasks.md (7 main tasks, 21 sub-tasks)

✅ .kiro/specs/admin-dashboard/requirements.md (7 requirements, 28 criteria)
✅ .kiro/specs/admin-dashboard/design.md (8 properties)
✅ .kiro/specs/admin-dashboard/tasks.md (6 main tasks, 18 sub-tasks)

Creating master overview...
✅ .kiro/specs/_spec-overview.md

## Summary
Created 5 specs with 43 requirements, 63 properties, and 32 main tasks.

Recommended next steps:
1. Review foundation spec: .kiro/specs/foundation/requirements.md
2. Start implementation with foundation tasks
3. Once foundation complete, begin product-catalog
4. Track progress in _spec-overview.md

Ready to start with foundation?
```

**Result**: You now have a complete multi-spec structure with:
- Clear separation between foundation and features
- Dependency mapping showing what must be built first
- Parallel development opportunities identified
- Master overview for tracking progress
- Each spec focused and manageable

### Example 2: Single-Spec Conversion (Todo List)

### What You Say:
```
@spec-converter convert docs/todo-list-prd.md to a Kiro spec

Focus on:
- Task CRUD operations
- Data validation
- Persistence
```

### What the Agent Does:

**Phase 1: Analysis**
```
🔄 Analyzing BMAD Documents

Reading:
- docs/todo-list-prd.md
- docs/todo-list-architecture.md

## Critical Features Analysis

### Recommend Kiro Spec:
1. **Task Management Core**
   - Reason: Data integrity critical, bugs would corrupt app
   - Scope: CRUD, validation, persistence, state management
   - Properties: Round-trip persistence, validation rules, state transitions

2. **Task Filtering**
   - Reason: State-based logic with edge cases
   - Scope: Active/completed/all filtering
   - Properties: Filter correctness, state preservation

### Recommend BMAD Cycle:
1. **UI Components**
   - Reason: Subjective quality, needs rapid iteration
   - Approach: SM → Dev → QA cycle

Shall I create a Kiro spec for "Task Management Core"?
```

**You:** Yes

**Phase 2: Requirements**
```
🔄 Creating requirements.md

Converting BMAD user stories to EARS format...
- Epic 1: Core Task Management → Requirements 1-3
- Epic 2: Task Completion → Requirements 4-5
- Epic 4: Task Editing → Requirement 8

Created: .kiro/specs/todo-task-core/requirements.md
- 8 requirements
- 40 acceptance criteria
- All in EARS format (WHEN/THEN/SHALL)
- Glossary with technical terms

Do the requirements look good? If so, we can move on to the design.
```

**You:** Yes

**Phase 3: Design**
```
🔄 Creating design.md with correctness properties

Running prework analysis on 40 acceptance criteria...
- 23 testable as properties
- 4 edge cases
- 13 non-testable (UI/performance)

Extracting architecture from docs/todo-list-architecture.md...
- Component structure
- Data models
- Storage strategy

Creating correctness properties...
- Property 1: Task Creation Increases List Size
- Property 2: Whitespace-Only Descriptions Are Rejected
- Property 3: Task Persistence Round-Trip
... (20 more properties)

Created: .kiro/specs/todo-task-core/design.md
- 23 correctness properties
- All linked to requirements
- Component architecture
- Error handling strategy

Does the design look good? If so, we can move on to the implementation plan.
```

**You:** Yes

**Phase 4: Tasks**
```
🔄 Creating tasks.md implementation plan

Breaking down into sequential tasks...
- 13 main tasks
- 35 sub-tasks
- 23 property-based test tasks (marked optional)
- 2 checkpoints

Each PBT task linked to specific property from design.md
Each task linked to specific requirements

Created: .kiro/specs/todo-task-core/tasks.md

The current task list marks some tasks (e.g. tests, documentation) as optional 
to focus on core features first.

Options:
1. Keep optional tasks (faster MVP)
2. Make all tasks required (comprehensive from start)
```

**You:** Keep optional tasks

**Done!**
```
✅ Spec Complete!

Created:
- .kiro/specs/todo-task-core/requirements.md
- .kiro/specs/todo-task-core/design.md
- .kiro/specs/todo-task-core/tasks.md

You can now:
1. Execute tasks by opening tasks.md and clicking "Start task"
2. I'll implement with property-based testing
3. Continue with BMAD cycle for UI components

Next steps:
- Execute task 1: Set up project structure
- Or: @sm create story for TaskInput component (BMAD cycle)
```

## Comparison: Multi-Spec vs Single-Spec vs Manual

### Multi-Spec Conversion (Complex Projects)
```
You: @spec-converter convert-multi docs/ecommerce-prd.md
Agent: [Analyzes, identifies 5 features, shows structure]
You: Yes, create all specs
Agent: [Creates foundation + 4 feature specs + overview]
```

**Result**: 
- 1 command, 1 approval
- 5 focused specs created
- Dependency graph generated
- Implementation order defined
- Parallel development identified
- Master overview for tracking

**Time Saved**: Massive - would take hours to manually structure and create 5 separate specs

### Single-Spec Conversion (Simple Features)
```
You: @spec-converter convert docs/todo-list-prd.md to a Kiro spec
Agent: [Analyzes, creates requirements, asks approval]
You: Yes
Agent: [Creates design, asks approval]
You: Yes
Agent: [Creates tasks, asks about optional]
You: Keep optional tasks
```

**Result**: 
- 1 command, 3 approvals
- 1 focused spec created
- Guided workflow
- Quality assurance built-in

**Time Saved**: Significant - agent handles EARS conversion, property extraction, task breakdown

### Manual Approach (No Agent)
```
You: Create a Kiro spec for task core based on docs/todo-list-prd.md
Kiro: [Creates requirements]
You: Do requirements look good?
You: Yes
Kiro: [Creates design]
You: Does design look good?
You: Yes
Kiro: [Creates tasks]
You: Keep optional tasks
```

**Result**: 
- 5+ prompts
- Manual workflow
- No automatic analysis
- No feature extraction
- No dependency mapping

**Time Cost**: High - requires manual structuring, multiple iterations, no guidance

## Why Use @spec-converter?

### Advantages

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

### When to Use Direct Kiro Prompts

✅ **Use direct Kiro prompts when:**
- You don't have BMAD documents
- You want to create spec from scratch
- You prefer complete manual control
- You're creating a very simple spec
- You're experimenting with spec format

## Integration with BMAD Workflow

### Complete Workflow for Complex Projects

```
Phase 1: BMAD Planning
├── @analyst research [project]
├── @pm create comprehensive PRD
├── @architect design system architecture
└── Save to docs/[project]-prd.md and docs/[project]-architecture.md

Phase 2: Multi-Spec Conversion
├── @spec-converter analyze-features docs/[project]-prd.md
├── Review feature breakdown and dependencies
├── @spec-converter convert-multi docs/[project]-prd.md
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

### Complete Workflow for Simple Features

```
Phase 1: BMAD Planning
├── @analyst research [feature]
├── @pm create PRD
├── @architect design architecture
└── Save to docs/[feature]-prd.md and docs/[feature]-architecture.md

Phase 2: Single-Spec Conversion
├── @spec-converter analyze docs/[feature]-prd.md
├── Identify critical features
├── @spec-converter convert docs/[feature]-prd.md
└── Approve requirements → design → tasks

Phase 3: Implementation
├── Execute Kiro spec tasks (critical features)
└── Use BMAD cycle (UI features)
```

## Tips for Best Results

### 1. Provide Good BMAD Documents

The better your BMAD PRD and Architecture, the better the conversion:
- ✅ Clear user stories with acceptance criteria
- ✅ Technical architecture with data models
- ✅ Technology decisions explained
- ✅ Edge cases and constraints documented

### 2. Be Specific About Focus

Tell the agent what aspects to focus on:
```
@spec-converter convert docs/[feature]-prd.md to a Kiro spec

Focus on:
- Data validation and integrity
- Persistence and storage
- State management
```

### 3. Review Each Phase

Don't just approve blindly:
- Read the requirements - are they testable?
- Check the properties - do they cover edge cases?
- Review the tasks - are they actionable?

### 4. Iterate When Needed

If something's not right, ask for changes:
```
Add a requirement for handling Unicode characters
Add a property for round-trip consistency with emoji
Break down task 3 into smaller sub-tasks
```

## Troubleshooting

### Agent Not Found
```
Error: @spec-converter not recognized
```

**Solution**: The agent was just created. Restart Kiro or start a new chat session.

### Documents Not Found
```
Agent: I can't find docs/[feature]-prd.md
```

**Solution**: Provide the correct path:
```
@spec-converter convert docs/my-actual-file.md to a Kiro spec
```

### Conversion Too Broad
```
Agent: This PRD covers too many features for one spec
```

**Solution**: Be specific about which feature to convert:
```
@spec-converter convert docs/[feature]-prd.md to a Kiro spec

Focus only on: [specific feature]
```

### Want Different Format
```
You: I want different property format
```

**Solution**: Ask the agent to adjust:
```
@spec-converter rewrite properties with more detail
@spec-converter add more edge case properties
@spec-converter simplify the task breakdown
```

## Summary

**The @spec-converter agent is your automation for BMAD → Kiro conversion.**

**One command:**
```
@spec-converter convert docs/[feature]-prd.md to a Kiro spec
```

**Three approvals:**
1. Requirements ✓
2. Design ✓
3. Tasks ✓

**Done!** You have a formal Kiro spec ready for implementation with property-based testing.

No more manual conversion. No more wondering what to say. Just activate the agent and let it guide you through the process.

## Try It Now

If you have BMAD documents ready:
```
@spec-converter analyze docs/[your-feature]-prd.md
```

If you want to see it in action:
```
@spec-converter convert docs/todo-list-prd.md to a Kiro spec
```

The agent will take care of the rest!
