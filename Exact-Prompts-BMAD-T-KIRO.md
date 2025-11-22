# Exact Prompts: BMAD to Kiro Spec Conversion

## The Problem

You have BMAD planning documents (PRD, Architecture) and want to convert them to formal Kiro specs. Here are the **exact prompts** to use.

## Prerequisites

You should have:
- `docs/[feature]-prd.md` - Created by @pm agent
- `docs/[feature]-architecture.md` - Created by @architect agent

## Step-by-Step Prompts

### Step 1: Identify the Feature to Formalize

**Your Prompt:**
```
I have a PRD at docs/[feature]-prd.md and architecture at docs/[feature]-architecture.md.

Help me identify which parts need formal Kiro specs with property-based testing versus which parts should use BMAD rapid iteration.

Look for:
- Features involving parsing, serialization, or data transformation
- Features where correctness bugs would be costly
- Core business logic with complex state transitions
- Features with many edge cases

List the critical features that should become Kiro specs.
```

**What I'll Do:**
- Read your BMAD documents
- Analyze each feature/epic
- Recommend which need formal specs
- Explain the reasoning

**Example Response:**
```
Based on your PRD and architecture, here are the critical features:

1. **Task Management Core** (Recommend Kiro Spec)
   - Reason: Data integrity is critical, bugs would corrupt entire app
   - Includes: CRUD operations, validation, persistence
   
2. **Duplicate Detection** (Recommend Kiro Spec)
   - Reason: Complex algorithm with edge cases
   - Includes: Similarity calculation, threshold logic

3. **UI Components** (Recommend BMAD Cycle)
   - Reason: Subjective quality, needs rapid iteration
   - Includes: TaskInput, TaskList, TaskItem components

Should I create a Kiro spec for "Task Management Core"?
```

### Step 2: Create the Kiro Spec

**Your Prompt (Option A - Let Me Do Everything):**
```
Create a Kiro spec for [feature name] based on docs/[feature]-prd.md and docs/[feature]-architecture.md.

Focus on:
- [Specific aspect 1, e.g., "task CRUD operations"]
- [Specific aspect 2, e.g., "data validation"]
- [Specific aspect 3, e.g., "persistence"]

Create the spec at .kiro/specs/[feature-name]/
```

**Your Prompt (Option B - Step by Step):**
```
Create a Kiro spec for [feature name] based on docs/[feature]-prd.md.

Start with the requirements.md file. Convert the relevant user stories and acceptance criteria to EARS format.

Focus on these epics/stories:
- [Epic/Story 1]
- [Epic/Story 2]
- [Epic/Story 3]

Create .kiro/specs/[feature-name]/requirements.md
```

**What I'll Do:**
- Read your BMAD documents
- Extract relevant user stories
- Convert to EARS format (WHEN/THEN/SHALL)
- Create glossary
- Write formal acceptance criteria
- Save to `.kiro/specs/[feature-name]/requirements.md`

### Step 3: Review Requirements

**What I'll Ask:**
```
Do the requirements look good? If so, we can move on to the design.
```

**Your Response Options:**
- `Yes` or `Looks good` → I proceed to design
- `Change [specific thing]` → I make changes and ask again
- `Add requirement for [X]` → I add it and ask again

### Step 4: Create Design with Properties

**Your Prompt (if I don't automatically continue):**
```
Create the design.md for [feature-name] spec based on:
- The requirements we just created
- The architecture in docs/[feature]-architecture.md

Include:
- Component structure
- Data models
- Correctness properties for each requirement
- Error handling strategy
```

**What I'll Do:**
- Analyze each acceptance criterion for testability (prework)
- Extract architecture details from your docs
- Create correctness properties (universally quantified)
- Link each property to specific requirements
- Save to `.kiro/specs/[feature-name]/design.md`

### Step 5: Review Design

**What I'll Ask:**
```
Does the design look good? If so, we can move on to the implementation plan.
```

**Your Response Options:**
- `Yes` or `Approved` → I proceed to tasks
- `Add property for [X]` → I add it and ask again
- `Change [specific thing]` → I make changes and ask again

### Step 6: Create Implementation Tasks

**Your Prompt (if I don't automatically continue):**
```
Create the tasks.md for [feature-name] spec.

Break down the implementation into:
- Setup and infrastructure tasks
- Core implementation tasks
- Property-based test tasks (mark as optional with *)
- Integration tasks
- Checkpoints

Each task should reference specific requirements.
Each PBT task should reference a specific property from design.md.
```

**What I'll Do:**
- Create sequential implementation tasks
- Add sub-tasks for each main task
- Create PBT tasks for each property (marked optional with *)
- Add checkpoints at logical breaks
- Link tasks to requirements
- Save to `.kiro/specs/[feature-name]/tasks.md`

### Step 7: Review Tasks

**What I'll Ask:**
```
The current task list marks some tasks (e.g. tests, documentation) as optional to focus on core features first.

Options:
1. Keep optional tasks (faster MVP)
2. Make all tasks required (comprehensive from start)
```

**Your Response:**
- Choose option 1 or 2
- Or request specific changes

### Step 8: Spec Complete

**What I'll Say:**
```
The spec is complete! You can now:

1. Execute tasks by opening .kiro/specs/[feature-name]/tasks.md
2. Click "Start task" next to any task
3. I'll implement with property-based testing

Or continue with BMAD cycle for other features.
```

## Complete Example Prompts

### Example 1: Todo List (What We Just Did)

```
Prompt 1:
I have a PRD at docs/todo-list-prd.md and architecture at docs/todo-list-architecture.md.
Help me identify which parts need formal Kiro specs.

Prompt 2:
Create a Kiro spec for "task management core" based on docs/todo-list-prd.md and docs/todo-list-architecture.md.
Focus on:
- Task CRUD operations
- Data validation and integrity
- Persistence to local storage
- State management

Create the spec at .kiro/specs/todo-task-core/

[I create requirements.md and ask for review]

Prompt 3:
Yes, looks good

[I create design.md with properties and ask for review]

Prompt 4:
Approved

[I create tasks.md and ask about optional tasks]

Prompt 5:
Keep optional tasks (faster MVP)

[Spec complete!]
```

### Example 2: Chat Application Message Parser

```
Prompt 1:
I have a PRD at docs/chat-app-prd.md and architecture at docs/chat-app-architecture.md.
Help me identify which parts need formal Kiro specs.

[I analyze and recommend: message parser, presence system]

Prompt 2:
Create a Kiro spec for "message parser" based on docs/chat-app-prd.md and docs/chat-app-architecture.md.
Focus on:
- Message format validation
- Serialization/deserialization
- Special character handling
- Edge cases (empty, very long, special chars)

Create the spec at .kiro/specs/message-parser/

[I create requirements.md]

Prompt 3:
Add a requirement for handling Unicode emoji

[I add the requirement and ask for review again]

Prompt 4:
Looks good now

[I create design.md with properties]

Prompt 5:
Add a property for round-trip consistency with emoji

[I add the property and ask for review again]

Prompt 6:
Approved

[I create tasks.md]

Prompt 7:
Make all tasks required (comprehensive from start)

[I remove * markers from optional tasks]

[Spec complete!]
```

### Example 3: E-commerce Payment Processor

```
Prompt 1:
Create a Kiro spec for "payment processor" based on docs/ecommerce-prd.md and docs/ecommerce-architecture.md.

Focus on:
- Payment validation
- Transaction state machine
- Idempotency guarantees
- Error handling and retries

Create the spec at .kiro/specs/payment-processor/

[I create full spec through the workflow]
```

## Quick Reference: Common Prompts

### Starting the Conversion
```
Create a Kiro spec for [feature] based on docs/[feature]-prd.md
Focus on: [list key aspects]
```

### Requesting Changes
```
Add a requirement for [X]
Change requirement [N] to [new text]
Add a property for [X]
Remove property [N]
```

### Approving Phases
```
Yes
Looks good
Approved
Continue
```

### Requesting More Detail
```
Add more detail to requirement [N]
Explain property [N] more clearly
Break down task [N] into smaller sub-tasks
```

### Adjusting Scope
```
This is too broad, focus only on [X]
Add [Y] to the scope
Remove [Z] from the scope
```

## Template Prompts You Can Copy

### Full Spec Creation (One Shot)
```
Create a complete Kiro spec for [FEATURE_NAME] based on:
- docs/[FEATURE]-prd.md
- docs/[FEATURE]-architecture.md

Focus on these aspects:
- [ASPECT_1]
- [ASPECT_2]
- [ASPECT_3]

Create the spec at .kiro/specs/[FEATURE_NAME]/

Include:
- EARS-formatted requirements with acceptance criteria
- Correctness properties for property-based testing
- Implementation tasks with PBT tasks marked optional
- Checkpoints for validation

I'll review each phase (requirements, design, tasks) before you proceed.
```

### Incremental Spec Creation
```
Step 1: Create requirements.md for [FEATURE_NAME] based on docs/[FEATURE]-prd.md
Focus on [SPECIFIC_EPICS_OR_STORIES]

[After review]

Step 2: Create design.md with correctness properties based on the requirements and docs/[FEATURE]-architecture.md

[After review]

Step 3: Create tasks.md with implementation plan
```

### Spec from Scratch (No BMAD Docs)
```
Create a Kiro spec for [FEATURE_NAME] from scratch.

Feature description:
[DESCRIBE_FEATURE]

Key requirements:
- [REQUIREMENT_1]
- [REQUIREMENT_2]
- [REQUIREMENT_3]

Create the spec at .kiro/specs/[FEATURE_NAME]/
```

## What NOT to Say

### ❌ Don't Say:
```
"Use the BMAD template"
"Run the template"
"Execute the YAML template"
"Generate from template"
```

These don't work because templates are starting points, not executable.

### ✅ Instead Say:
```
"Create a Kiro spec based on my BMAD documents"
"Convert my PRD to a formal Kiro spec"
"Transform my planning docs into a spec"
```

## Troubleshooting Prompts

### If I'm Not Understanding Your BMAD Docs
```
The PRD is at docs/[FILE].md
The architecture is at docs/[FILE].md
Please read these files first, then create the spec.
```

### If the Spec Is Too Broad
```
This spec is too broad. Focus only on [SPECIFIC_PART].
We'll create separate specs for the other parts.
```

### If the Spec Is Too Narrow
```
This spec is too narrow. Also include [ADDITIONAL_PART].
```

### If Properties Are Missing
```
Add correctness properties for:
- [ASPECT_1]
- [ASPECT_2]
```

### If You Want More/Fewer Tests
```
Add more property-based tests for edge cases
OR
Reduce the number of PBT tasks, focus on critical properties only
```

## Summary

**The Magic Prompt:**
```
Create a Kiro spec for [feature] based on docs/[feature]-prd.md and docs/[feature]-architecture.md.
Focus on: [key aspects]
Create the spec at .kiro/specs/[feature-name]/
```

**Then just respond to my questions:**
- "Do the requirements look good?" → Yes/No/Changes
- "Does the design look good?" → Yes/No/Changes  
- "Keep optional tasks or make all required?" → Choose one

**That's it.** Three prompts, three reviews, done.

## Real-World Usage

### Your Typical Workflow

1. **Chat with BMAD agents** (separate chats or web UI)
   ```
   @pm create PRD for [feature]
   @architect design architecture for [feature]
   ```

2. **Save documents** to `docs/`

3. **Come to Kiro and say:**
   ```
   Create a Kiro spec for [critical feature] based on docs/[feature]-prd.md
   Focus on: [what needs correctness]
   ```

4. **Review and approve** each phase

5. **Execute tasks** from the spec

That's the workflow. Simple as that.
