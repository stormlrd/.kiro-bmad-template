# Brownfield Iteration Guide - Using BMAD Template with Existing Codebases

## Overview

This guide explains how to use the .kiro-bmad-template to iterate on existing codebases, such as AWS SBT (SaaS Builder Toolkit) or any other established project. The brownfield approach focuses on understanding, documenting, and extending existing systems rather than building from scratch.

## When to Use This Approach

✅ **Use brownfield iteration when:**
- Working with an existing codebase (AWS SBT, open source projects, legacy systems)
- Adding new features to established applications
- Modernizing or enhancing existing functionality
- Integrating with existing control planes or APIs
- Maintaining compatibility with existing systems

❌ **Don't use brownfield when:**
- Starting a completely new project (use greenfield approach)
- Rewriting from scratch
- No existing code to reference

## Brownfield Workflow for AWS SBT Application Plane

This example uses AWS SBT, but the principles apply to any existing codebase.

### Phase 1: Project Setup and Documentation

#### 1. Set Up Your Iteration Project

```bash
# Create your iteration project
mkdir aws-sbt-app-plane-iteration
cd aws-sbt-app-plane-iteration

# Copy the .kiro folder from this template
cp -r /path/to/.kiro-bmad-template/.kiro .

# Clone or reference the existing codebase
git clone https://github.com/awslabs/sbt-aws.git reference/sbt-aws
# Or add as submodule if you prefer
git submodule add https://github.com/awslabs/sbt-aws.git reference/sbt-aws
```

**Windows (PowerShell)**:
```powershell
# Create your iteration project
mkdir aws-sbt-app-plane-iteration
cd aws-sbt-app-plane-iteration

# Copy the .kiro folder from this template
Copy-Item -Recurse \path\to\.kiro-bmad-template\.kiro .

# Clone or reference the existing codebase
git clone https://github.com/awslabs/sbt-aws.git reference/sbt-aws
```

#### 2. Document the Existing System First

**This is CRITICAL for brownfield** - you need to understand what exists before iterating.

**Step 2.1: Technology Detection**

```
@bmad-master *detect-tech

# This will analyze the existing codebase and identify:
# - Technologies used (CDK, TypeScript, Python, etc.)
# - Architecture patterns
# - Dependencies
# - Key components
```


**Step 2.2: System Analysis**

```
@analyst
Analyze the AWS SBT application plane architecture. Focus on:
- Current application plane components
- Control plane vs application plane separation
- Tenant isolation mechanisms
- Current limitations or pain points
- Integration points with control plane
- Existing APIs and contracts
- Data flow and state management

Save findings to docs/sbt-current-state-analysis.md
```

**Step 2.3: Architecture Documentation**

```
@architect
Document the existing AWS SBT application plane architecture:
- Component diagram
- Data flow diagrams
- Tenant provisioning flow
- Current tech stack (CDK constructs, Lambda, API Gateway, etc.)
- Infrastructure as code patterns
- Security and isolation mechanisms
- Scalability considerations

Save to docs/sbt-architecture-current.md
```

**Why Document First?**
- Understand existing patterns before changing them
- Identify integration points
- Avoid breaking existing functionality
- Plan for backward compatibility
- Establish baseline for improvements

### Phase 2: Define Your Iteration Goals

#### 3. Create Enhancement PRD (Brownfield Style)

Use the **brownfield PRD template** approach:

```
@pm
Create a PRD for enhancing the AWS SBT application plane. 

Context:
- Existing System: AWS SBT application plane (reference docs/sbt-architecture-current.md)
- Goal: [Your specific iteration goal]
  Examples:
  - Add advanced tenant isolation with network segmentation
  - Improve observability with distributed tracing
  - Add custom domain support per tenant
  - Enhance multi-region capabilities
  - Add tenant-specific configuration management

- Constraints: 
  - Must maintain compatibility with existing control plane
  - Cannot break existing tenant deployments
  - Must support SBT upgrade path
  
- Integration Points: 
  - Control plane APIs
  - Tenant provisioning workflows
  - Billing integration
  - Existing CDK constructs

Include:
- Current system overview (what exists)
- Gap analysis (what's missing)
- Enhancement requirements (what to add)
- User stories for new capabilities
- Success metrics
- Migration/compatibility strategy
- Rollback plan

Save to docs/sbt-app-plane-enhancement-prd.md
```

**Key Sections for Brownfield PRD**:
1. **Current State**: What exists today
2. **Gaps and Pain Points**: What needs improvement
3. **Proposed Enhancements**: What you'll add
4. **Compatibility Strategy**: How to maintain existing functionality
5. **Migration Path**: How to upgrade existing deployments
6. **Rollback Plan**: How to revert if needed

### Phase 3: Multi-Spec Conversion Strategy

#### 4. Convert to Granular Specs

Here's where your multi-spec converter shines for brownfield:

```
@kiro-spec-converter convert-multi docs/sbt-app-plane-enhancement-prd.md

Focus on:
- Separate specs for each major enhancement
- Foundation spec for shared infrastructure changes
- Feature specs for new capabilities
- Clear dependencies on existing SBT components
- Integration testing requirements
```

**Expected Output Structure**:
```
.kiro/specs/
├── foundation-sbt-integration/      # Core integration with existing SBT
│   ├── requirements.md              # How to integrate with control plane
│   ├── design.md                    # Integration patterns, APIs
│   └── tasks.md                     # Integration implementation
│
├── tenant-isolation-enhancement/    # Feature 1: Enhanced isolation
│   ├── requirements.md              # Network segmentation requirements
│   ├── design.md                    # VPC, security groups, NACLs
│   └── tasks.md                     # Implementation tasks
│
├── observability-layer/             # Feature 2: Observability
│   ├── requirements.md              # Tracing, metrics, logging requirements
│   ├── design.md                    # X-Ray, CloudWatch, custom metrics
│   └── tasks.md                     # Implementation tasks
│
├── custom-domain-support/           # Feature 3: Custom domains
│   ├── requirements.md              # Domain management requirements
│   ├── design.md                    # Route53, ACM, CloudFront
│   └── tasks.md                     # Implementation tasks
│
└── _spec-overview.md                # Master tracking with dependencies
```

**Why Multi-Spec for Brownfield?**
- Each enhancement is independently testable
- Can implement features in parallel
- Clear dependency tracking
- Easier rollback of individual features
- Better progress visibility

### Phase 4: Implementation Strategy

#### 5. Foundation First - Integration Layer

Start with the foundation spec to establish your integration patterns:

```
Execute: .kiro/specs/foundation-sbt-integration/tasks.md

This should include:
- CDK construct extensions for SBT
- Integration with control plane APIs
- Shared utilities and helpers
- Testing infrastructure for SBT integration
- Compatibility layer for SBT updates
```

**Key Considerations for Foundation**:
- ✅ Don't modify core SBT code directly
- ✅ Create extension points and wrappers
- ✅ Use CDK composition patterns
- ✅ Maintain upgrade path for SBT updates
- ✅ Version lock SBT dependencies
- ✅ Document integration contracts

**Example Foundation Structure**:
```typescript
// src/shared/sbt-integration/base-wrapper.ts
import { CoreApplicationPlane } from '@cdklabs/sbt-aws';

/**
 * Base wrapper for SBT integration
 * Provides extension points without modifying core
 */
export class SBTIntegrationBase {
  constructor(
    protected readonly sbtCore: CoreApplicationPlane,
    protected readonly config: IntegrationConfig
  ) {}
  
  // Extension points
  protected beforeTenantProvision(tenantId: string): void {}
  protected afterTenantProvision(tenantId: string): void {}
  
  // Integration helpers
  protected callControlPlaneAPI(endpoint: string, data: any): Promise<any> {
    // Wrapper for control plane communication
  }
}
```

#### 6. Feature Implementation - Parallel Development

Once foundation is solid, implement features based on dependencies:

**For Infrastructure/CDK Changes** (Use Kiro Specs):
```
Execute: .kiro/specs/tenant-isolation-enhancement/tasks.md

Focus on:
- CDK construct correctness
- IAM policy validation
- Resource isolation properties
- Infrastructure state consistency
- Property-based testing for isolation
```

**Example: Tenant Isolation Enhancement**
```typescript
// src/constructs/enhanced-tenant-isolation/network-isolation.ts
import { Construct } from 'constructs';
import { SBTIntegrationBase } from '../../shared/sbt-integration';

export class EnhancedTenantIsolation extends Construct {
  constructor(scope: Construct, id: string, sbtBase: SBTIntegrationBase) {
    super(scope, id);
    
    // Add network isolation without modifying SBT core
    this.createIsolatedVPC();
    this.createSecurityGroups();
    this.createNetworkACLs();
  }
  
  private createIsolatedVPC() {
    // Implementation
  }
}
```

**For Application Code** (Use BMAD Cycle):
```
@sm
Create story for tenant onboarding UI enhancement
Based on: docs/sbt-app-plane-enhancement-prd.md
Focus on: Custom domain configuration during onboarding

@dev
Implement the tenant onboarding UI enhancement
- Add custom domain input fields
- Integrate with existing SBT control plane APIs
- Validate domain ownership
- Update tenant configuration

@qa
Review tenant onboarding implementation
- Test integration with SBT control plane
- Validate tenant isolation
- Test domain validation flow
- Verify backward compatibility with existing tenants
```

### Phase 5: Testing and Validation

#### 7. Integration Testing with Existing SBT

Create a testing strategy that validates against real SBT:

```
@qa
Create integration test plan for SBT application plane enhancements:

Test Categories:
1. Integration Tests
   - Test against existing SBT control plane
   - Validate tenant provisioning flow
   - Test API contracts
   
2. Compatibility Tests
   - Test backward compatibility
   - Validate upgrade scenarios
   - Test with existing tenant deployments
   
3. Performance Tests
   - Performance testing with multiple tenants
   - Load testing tenant provisioning
   - Stress testing isolation boundaries
   
4. Security Tests
   - Validate tenant isolation
   - Test IAM policies
   - Verify network segmentation

Save to docs/sbt-integration-test-plan.md
```

**Example Integration Test**:
```typescript
// test/integration/sbt-control-plane.test.ts
import { SBTControlPlane } from '@cdklabs/sbt-aws';
import { EnhancedApplicationPlane } from '../../src/constructs';

describe('SBT Control Plane Integration', () => {
  let controlPlane: SBTControlPlane;
  let enhancedAppPlane: EnhancedApplicationPlane;
  
  beforeAll(async () => {
    // Set up real SBT control plane
    controlPlane = await setupSBTControlPlane();
    enhancedAppPlane = new EnhancedApplicationPlane(controlPlane);
  });
  
  test('should provision tenant with enhancements', async () => {
    const tenantId = 'test-tenant-001';
    
    // Provision through enhanced app plane
    const result = await enhancedAppPlane.provisionTenant({
      tenantId,
      customDomain: 'tenant001.example.com',
      isolationLevel: 'network'
    });
    
    // Verify with control plane
    const tenant = await controlPlane.getTenant(tenantId);
    expect(tenant.status).toBe('ACTIVE');
    expect(tenant.customDomain).toBe('tenant001.example.com');
  });
  
  test('should maintain compatibility with standard provisioning', async () => {
    // Test that standard SBT provisioning still works
    const standardTenant = await controlPlane.provisionTenant({
      tenantId: 'standard-tenant-001'
    });
    
    expect(standardTenant.status).toBe('ACTIVE');
  });
});
```

## Recommended Project Structure

```
aws-sbt-app-plane-iteration/
├── .kiro/                           # Your BMAD template
│   ├── specs/                       # Your enhancement specs
│   │   ├── foundation-sbt-integration/
│   │   ├── tenant-isolation-enhancement/
│   │   ├── observability-layer/
│   │   ├── custom-domain-support/
│   │   └── _spec-overview.md
│   │
│   ├── steering/                    # BMAD agents
│   │   ├── agents/
│   │   └── context/
│   │
│   └── hooks/                       # Automation hooks
│
├── reference/                       # Reference to original codebase
│   └── sbt-aws/                     # AWS SBT repository (submodule or clone)
│       ├── src/
│       ├── docs/
│       └── examples/
│
├── docs/                            # Your documentation
│   ├── sbt-current-state-analysis.md
│   ├── sbt-architecture-current.md
│   ├── sbt-app-plane-enhancement-prd.md
│   ├── sbt-integration-test-plan.md
│   └── sbt-upgrade-strategy.md
│
├── src/                             # Your enhancements (not modifications)
│   ├── constructs/                  # CDK construct extensions
│   │   ├── enhanced-tenant-isolation/
│   │   │   ├── network-isolation.ts
│   │   │   ├── security-groups.ts
│   │   │   └── index.ts
│   │   │
│   │   ├── observability-layer/
│   │   │   ├── tracing.ts
│   │   │   ├── metrics.ts
│   │   │   └── index.ts
│   │   │
│   │   └── custom-domain-support/
│   │       ├── domain-manager.ts
│   │       ├── certificate-manager.ts
│   │       └── index.ts
│   │
│   ├── lambda/                      # Lambda function code
│   │   ├── tenant-provisioning/
│   │   │   ├── handler.ts
│   │   │   └── index.ts
│   │   │
│   │   └── observability/
│   │       ├── metrics-collector.ts
│   │       └── index.ts
│   │
│   └── shared/                      # Shared utilities
│       ├── sbt-integration/
│       │   ├── base-wrapper.ts
│       │   ├── control-plane-client.ts
│       │   └── index.ts
│       │
│       └── testing-helpers/
│           ├── sbt-test-utils.ts
│           └── index.ts
│
├── test/                            # Your tests
│   ├── unit/
│   │   ├── constructs/
│   │   └── lambda/
│   │
│   ├── integration/
│   │   ├── sbt-control-plane.test.ts
│   │   ├── tenant-provisioning.test.ts
│   │   └── tenant-isolation.test.ts
│   │
│   └── e2e/
│       └── full-tenant-lifecycle.test.ts
│
├── cdk/                             # Your CDK app
│   ├── bin/
│   │   └── app.ts
│   ├── lib/
│   │   └── enhanced-sbt-stack.ts
│   └── cdk.json
│
├── package.json
├── tsconfig.json
└── README.md
```

## Key Strategies for Brownfield Iteration

### 1. Document First, Code Second

**Priority Order**:
1. ✅ Understand existing system (@analyst, @architect)
2. ✅ Document current state thoroughly
3. ✅ Define enhancement goals (@pm)
4. ✅ Create formal specs (@kiro-spec-converter)
5. ✅ Implement incrementally
6. ✅ Test continuously

**Why This Order?**
- Prevents breaking existing functionality
- Identifies integration points early
- Establishes compatibility requirements
- Creates baseline for testing
- Documents assumptions

### 2. Composition Over Modification

**❌ Don't Modify Core Code**:
```typescript
// BAD: Modifying SBT core
import { CoreApplicationPlane } from '@cdklabs/sbt-aws';

class MyApplicationPlane extends CoreApplicationPlane {
  // Overriding core methods - risky for upgrades
  provisionTenant(config: TenantConfig) {
    // Modified behavior - breaks on SBT updates
  }
}
```

**✅ Do Compose and Extend**:
```typescript
// GOOD: Composing with SBT
import { CoreApplicationPlane } from '@cdklabs/sbt-aws';

class EnhancedApplicationPlane {
  constructor(private core: CoreApplicationPlane) {}
  
  // Add enhancements without modifying core
  async provisionTenantWithEnhancements(config: EnhancedTenantConfig) {
    // Pre-provisioning enhancements
    await this.setupCustomDomain(config.customDomain);
    await this.setupNetworkIsolation(config.isolationLevel);
    
    // Use core SBT functionality
    const tenant = await this.core.provisionTenant(config);
    
    // Post-provisioning enhancements
    await this.setupObservability(tenant.id);
    
    return tenant;
  }
  
  addObservability() {
    // Add your enhancements
  }
  
  addCustomDomains() {
    // Add your enhancements
  }
}
```

**Benefits of Composition**:
- ✅ Maintains SBT upgrade path
- ✅ Clear separation of concerns
- ✅ Easier testing
- ✅ Independent versioning
- ✅ Rollback capability

### 3. Use Multi-Spec for Complex Enhancements

Each major enhancement gets its own spec:
- **Foundation**: Integration patterns with SBT
- **Feature 1**: Tenant isolation enhancements
- **Feature 2**: Observability layer
- **Feature 3**: Custom domain support

**This allows**:
- ✅ Parallel development
- ✅ Independent testing
- ✅ Incremental rollout
- ✅ Clear dependency tracking
- ✅ Feature-specific rollback

**Dependency Example**:
```
foundation-sbt-integration (Must be first)
├── tenant-isolation-enhancement (Depends on foundation)
│   └── observability-layer (Depends on isolation)
└── custom-domain-support (Depends on foundation)
    └── tenant-branding (Depends on custom domains)
```

### 4. Maintain Upgrade Path

```
@architect
Design enhancement architecture that:
- Doesn't modify SBT core code
- Uses composition and extension patterns
- Maintains compatibility with SBT updates
- Provides clear migration path
- Documents version dependencies
- Includes rollback procedures

Key Principles:
1. Version Lock: Lock SBT version in package.json
2. Extension Points: Use SBT's extension mechanisms
3. Wrapper Pattern: Wrap SBT functionality, don't override
4. Testing: Test against multiple SBT versions
5. Documentation: Document SBT version compatibility

Save to docs/sbt-upgrade-strategy.md
```

**Example Version Management**:
```json
{
  "dependencies": {
    "@cdklabs/sbt-aws": "1.2.3",  // Locked version
    "aws-cdk-lib": "2.100.0"       // Compatible CDK version
  },
  "devDependencies": {
    "@cdklabs/sbt-aws": "^1.2.0"   // Test against minor versions
  }
}
```

### 5. Test Against Real System

```
test/
├── unit/                            # Unit tests for your code
│   ├── constructs/
│   └── lambda/
│
├── integration/                     # Test with real SBT
│   ├── sbt-control-plane.test.ts    # Test against real control plane
│   ├── tenant-provisioning.test.ts  # Test full provisioning flow
│   ├── tenant-isolation.test.ts     # Validate isolation
│   └── api-compatibility.test.ts    # Test API contracts
│
└── e2e/                             # End-to-end scenarios
    ├── full-tenant-lifecycle.test.ts
    ├── multi-tenant-scenarios.test.ts
    └── upgrade-scenarios.test.ts
```

**Integration Test Strategy**:
1. **Setup**: Deploy real SBT control plane
2. **Test**: Run enhancements against real system
3. **Validate**: Verify both old and new functionality
4. **Teardown**: Clean up test resources

## Practical Example: Adding Observability to SBT

### Complete Step-by-Step Workflow

#### Step 1: Document Current State

```bash
# Analyze existing SBT observability
@analyst analyze AWS SBT observability capabilities

# Document current monitoring and logging
@architect document current monitoring and logging in SBT
```

**Output**: `docs/sbt-observability-current.md`

#### Step 2: Define Enhancement

```bash
@pm create PRD for comprehensive observability layer for SBT application plane

Include:
- Current observability gaps
- Proposed enhancements (X-Ray, custom metrics, dashboards)
- Integration with existing CloudWatch
- Tenant-specific observability
- Cost considerations
```

**Output**: `docs/sbt-observability-prd.md`

#### Step 3: Convert to Specs

```bash
@kiro-spec-converter convert-multi docs/sbt-observability-prd.md

Focus on:
- Foundation: SBT integration hooks
- Feature 1: Distributed tracing with X-Ray
- Feature 2: Custom CloudWatch metrics
- Feature 3: Tenant-specific dashboards
```

**Output**: Multiple specs in `.kiro/specs/`

#### Step 4: Implement Foundation

```bash
# Execute foundation tasks
Execute: .kiro/specs/foundation-sbt-integration/tasks.md
```

**Creates**:
```typescript
// src/shared/sbt-integration/observability-hooks.ts
export class ObservabilityHooks {
  onTenantProvisionStart(tenantId: string) {
    // Hook into SBT provisioning
  }
  
  onTenantProvisionComplete(tenantId: string) {
    // Hook into SBT provisioning
  }
}
```

#### Step 5: Implement Observability Features

```bash
# Execute observability tasks
Execute: .kiro/specs/observability-layer/tasks.md
```

**Creates**:
```
src/constructs/observability-layer/
├── tracing.ts              # X-Ray integration
├── metrics.ts              # Custom CloudWatch metrics
├── dashboards.ts           # CloudWatch dashboards
└── index.ts

src/lambda/observability/
├── metrics-collector.ts    # Collect tenant metrics
└── trace-processor.ts      # Process X-Ray traces
```

#### Step 6: Test Integration

```bash
@qa test observability layer with existing SBT control plane

Test scenarios:
- Tenant provisioning with tracing
- Metric collection during tenant operations
- Dashboard creation for new tenants
- Backward compatibility with existing tenants
```

#### Step 7: Document for Team

```bash
@pm create deployment guide for observability enhancements

Include:
- Prerequisites
- Deployment steps
- Configuration options
- Rollback procedures
- Monitoring the monitoring (meta!)
```

## Summary: Your Brownfield Workflow

### Quick Reference

1. **Setup**: Copy .kiro template to your iteration project
2. **Document**: Use @analyst and @architect to understand existing system
3. **Plan**: Use @pm to create enhancement PRD (brownfield style)
4. **Structure**: Use @kiro-spec-converter convert-multi for granular specs
5. **Implement**: Foundation first, then features (parallel when possible)
6. **Test**: Integration tests against real system
7. **Iterate**: Track progress in _spec-overview.md

### Key Principles

**Composition Over Modification**
- ✅ Extend, don't modify
- ✅ Wrap, don't override
- ✅ Compose, don't replace

**Document First**
- ✅ Understand before changing
- ✅ Document current state
- ✅ Plan compatibility

**Test Continuously**
- ✅ Unit tests for your code
- ✅ Integration tests with real system
- ✅ Compatibility tests for upgrades

**Maintain Upgrade Path**
- ✅ Version lock dependencies
- ✅ Use extension points
- ✅ Test against multiple versions

### Benefits of This Approach

✅ **Clear understanding** of existing system
✅ **Granular, focused** enhancements
✅ **Parallel development** capability
✅ **Upgrade path** for base system updates
✅ **Comprehensive testing** strategy
✅ **Clear progress** tracking
✅ **Independent rollback** of features
✅ **Maintainable** long-term

## Next Steps

1. **Choose Your Target**: Identify the existing codebase you want to enhance
2. **Set Up Project**: Copy .kiro template and reference original code
3. **Document Current State**: Use @analyst and @architect
4. **Define Enhancements**: Use @pm for brownfield PRD
5. **Create Specs**: Use @kiro-spec-converter convert-multi
6. **Start with Foundation**: Implement integration layer first
7. **Add Features**: Implement enhancements incrementally
8. **Test Thoroughly**: Validate against real system

## Additional Resources

- **BMAD Method**: https://github.com/bmad-code-org/BMAD-METHOD
- **AWS SBT**: https://github.com/awslabs/sbt-aws
- **CDK Patterns**: https://cdkpatterns.com
- **Composition Patterns**: See `docs/composition-patterns.md` (create this!)

---

**Remember**: Treat existing codebases as libraries you're extending, not code you're modifying. Your enhancements should compose with the original, not replace it.

Happy iterating! 🚀
