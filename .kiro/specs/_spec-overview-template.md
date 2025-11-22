# Spec Overview - [Project Name]

> **Purpose**: This document provides a master overview of all specs in this project, their dependencies, implementation order, and progress tracking.
>
> **Generated**: [Date]
> **Last Updated**: [Date]

## Project Summary

**Project**: [Project Name]
**Description**: [Brief project description]
**BMAD Source Documents**:
- PRD: `docs/[project]-prd.md`
- Architecture: `docs/[project]-architecture.md`

## Specs Overview

### Foundation/Core Infrastructure

**Spec**: [foundation](./foundation/)
**Status**: ⏳ Not Started | 🔄 In Progress | ✅ Complete
**Priority**: Critical (Must be completed first)

**Purpose**: Core infrastructure that all features depend on

**Components**:
- Database schema and migrations
- Authentication and authorization
- API base structure and middleware
- Shared utilities and configuration
- Error handling framework

**Metrics**:
- Requirements: [X]
- Acceptance Criteria: [Y]
- Correctness Properties: [Z]
- Main Tasks: [A]
- Sub-tasks: [B]
- Completed Tasks: [C]/[Total]

**Progress**: [Progress bar or percentage]

---

### Feature 1: [Feature Name]

**Spec**: [[feature-slug]](./[feature-slug]/)
**Status**: ⏳ Not Started | 🔄 In Progress | ✅ Complete
**Priority**: High | Medium | Low

**Purpose**: [Brief description of feature purpose]

**Key Capabilities**:
- [Capability 1]
- [Capability 2]
- [Capability 3]

**Dependencies**:
- [Foundation](./foundation/) - Database, API, Auth
- [[Other Feature]](./[other-feature]/) - [Dependency description]

**Blocks**:
- [[Dependent Feature]](./[dependent-feature]/) - [Why it blocks]

**Metrics**:
- Requirements: [X]
- Acceptance Criteria: [Y]
- Correctness Properties: [Z]
- Main Tasks: [A]
- Sub-tasks: [B]
- Completed Tasks: [C]/[Total]

**Progress**: [Progress bar or percentage]

---

### Feature 2: [Feature Name]

**Spec**: [[feature-slug]](./[feature-slug]/)
**Status**: ⏳ Not Started | 🔄 In Progress | ✅ Complete
**Priority**: High | Medium | Low

**Purpose**: [Brief description of feature purpose]

**Key Capabilities**:
- [Capability 1]
- [Capability 2]
- [Capability 3]

**Dependencies**:
- [Foundation](./foundation/) - Database, API, Auth
- [[Other Feature]](./[other-feature]/) - [Dependency description]

**Blocks**:
- [[Dependent Feature]](./[dependent-feature]/) - [Why it blocks]

**Metrics**:
- Requirements: [X]
- Acceptance Criteria: [Y]
- Correctness Properties: [Z]
- Main Tasks: [A]
- Sub-tasks: [B]
- Completed Tasks: [C]/[Total]

**Progress**: [Progress bar or percentage]

---

[Continue for all features...]

## Dependency Graph

```
foundation (Critical - Must be first)
├── [feature-1] (High Priority)
│   ├── [feature-3] (Medium Priority)
│   └── [feature-4] (Low Priority)
└── [feature-2] (High Priority)
    └── [feature-5] (Medium Priority)
```

**Legend**:
- `foundation` → All features depend on this
- `feature-1` → `feature-3` means feature-3 depends on feature-1
- Indentation shows dependency depth

## Implementation Order

### Phase 1: Foundation (Critical)
1. ✅ **Foundation** - Core infrastructure
   - Status: Complete
   - Duration: [X] days
   - Completed: [Date]

### Phase 2: Core Features (High Priority)
2. 🔄 **[Feature 1]** - [Brief description]
   - Status: In Progress (Task 3/6)
   - Depends on: Foundation
   - Can start: After Phase 1
   - Parallel with: [Feature 2]

3. ⏳ **[Feature 2]** - [Brief description]
   - Status: Not Started
   - Depends on: Foundation
   - Can start: After Phase 1
   - Parallel with: [Feature 1]

### Phase 3: Dependent Features (Medium Priority)
4. ⏳ **[Feature 3]** - [Brief description]
   - Status: Not Started
   - Depends on: Foundation, Feature 1
   - Can start: After Phase 2 (Feature 1)
   - Parallel with: [Feature 4]

5. ⏳ **[Feature 4]** - [Brief description]
   - Status: Not Started
   - Depends on: Foundation, Feature 2
   - Can start: After Phase 2 (Feature 2)
   - Parallel with: [Feature 3]

### Phase 4: Advanced Features (Low Priority)
6. ⏳ **[Feature 5]** - [Brief description]
   - Status: Not Started
   - Depends on: Foundation, Feature 1, Feature 3
   - Can start: After Phase 3
   - Parallel with: None

## Parallel Development Opportunities

**Phase 2**: Features 1 and 2 can be developed simultaneously
- Both depend only on Foundation
- No inter-dependencies
- Recommended: Assign to different developers

**Phase 3**: Features 3 and 4 can be developed simultaneously
- Feature 3 depends on Feature 1
- Feature 4 depends on Feature 2
- No inter-dependencies between 3 and 4
- Can start when respective dependencies complete

## Progress Summary

### Overall Progress
- **Total Specs**: [N]
- **Completed Specs**: [X]/[N] ([Percentage]%)
- **In Progress Specs**: [Y]
- **Not Started Specs**: [Z]

### Requirements Coverage
- **Total Requirements**: [X]
- **Total Acceptance Criteria**: [Y]
- **Total Correctness Properties**: [Z]

### Implementation Progress
- **Total Main Tasks**: [A]
- **Total Sub-tasks**: [B]
- **Completed Tasks**: [C]/[Total] ([Percentage]%)
- **In Progress Tasks**: [D]
- **Blocked Tasks**: [E]

### Timeline
- **Project Start**: [Date]
- **Foundation Complete**: [Date] or [Estimated]
- **Phase 2 Target**: [Date]
- **Phase 3 Target**: [Date]
- **Phase 4 Target**: [Date]
- **Project Target Completion**: [Date]

## Features Not Included (BMAD Cycle)

These features are better suited for BMAD's SM → Dev → QA cycle rather than formal Kiro specs:

1. **[UI Feature 1]** - [Reason: Subjective quality, rapid iteration needed]
2. **[UI Feature 2]** - [Reason: Visual design, user feedback driven]
3. **[Content Feature]** - [Reason: Content-focused, minimal logic]
4. **[Marketing Feature]** - [Reason: Exploratory, frequent changes]

**Approach**: Use BMAD agents (@sm, @dev, @qa) for these features after core specs are implemented.

## Cross-Spec Integration Points

### Database Schema
- **Owner**: Foundation
- **Used By**: All features
- **Integration**: All features reference foundation schema
- **Changes**: Require foundation spec update and migration

### Authentication System
- **Owner**: Foundation
- **Used By**: All features requiring auth
- **Integration**: Features use foundation auth middleware
- **Changes**: Require foundation spec update

### API Middleware
- **Owner**: Foundation
- **Used By**: All features with API endpoints
- **Integration**: Features extend foundation API structure
- **Changes**: Require foundation spec update

### [Feature 1] Data Models
- **Owner**: Feature 1
- **Used By**: Feature 3, Feature 5
- **Integration**: Dependent features import and extend models
- **Changes**: May require updates to dependent features

### [Feature 2] Services
- **Owner**: Feature 2
- **Used By**: Feature 4
- **Integration**: Feature 4 calls Feature 2 services
- **Changes**: API contract changes require Feature 4 updates

## Maintenance and Updates

### When to Update This Document

Update this overview when:
- ✅ New spec is created
- ✅ Spec status changes (Not Started → In Progress → Complete)
- ✅ Task completion milestones reached
- ✅ Dependencies change
- ✅ Implementation order is adjusted
- ✅ New features are identified

### Update Procedure

1. Update spec status and progress metrics
2. Update dependency graph if dependencies change
3. Update implementation order if priorities change
4. Update progress summary with current metrics
5. Update timeline with actual completion dates
6. Commit changes with descriptive message

### Version History

| Date | Version | Changes | Updated By |
|------|---------|---------|------------|
| [Date] | 1.0 | Initial spec overview created | @spec-converter |
| [Date] | 1.1 | [Description of changes] | [Agent/User] |
| [Date] | 1.2 | [Description of changes] | [Agent/User] |

## Notes and Decisions

### Architectural Decisions
- [Date]: [Decision description and rationale]
- [Date]: [Decision description and rationale]

### Scope Changes
- [Date]: [Scope change description and impact]
- [Date]: [Scope change description and impact]

### Lessons Learned
- [Date]: [Lesson learned and how it affects future work]
- [Date]: [Lesson learned and how it affects future work]

## Quick Navigation

### By Status
- **Not Started**: [[Feature X]](./[feature-x]/), [[Feature Y]](./[feature-y]/)
- **In Progress**: [[Feature Z]](./[feature-z]/)
- **Complete**: [[Foundation]](./foundation/)

### By Priority
- **Critical**: [[Foundation]](./foundation/)
- **High**: [[Feature 1]](./[feature-1]/), [[Feature 2]](./[feature-2]/)
- **Medium**: [[Feature 3]](./[feature-3]/), [[Feature 4]](./[feature-4]/)
- **Low**: [[Feature 5]](./[feature-5]/)

### By Phase
- **Phase 1**: [[Foundation]](./foundation/)
- **Phase 2**: [[Feature 1]](./[feature-1]/), [[Feature 2]](./[feature-2]/)
- **Phase 3**: [[Feature 3]](./[feature-3]/), [[Feature 4]](./[feature-4]/)
- **Phase 4**: [[Feature 5]](./[feature-5]/)

---

**Last Updated**: [Date and Time]
**Next Review**: [Date]
