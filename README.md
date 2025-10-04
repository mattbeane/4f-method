# The 4F Method
## Four-Function Fractal Software Development

> **Build complex software by recursively applying four simple functions until you can code.**

The 4F Method is a recursive approach to software development created by **Daniel Rock** that emphasizes complete specification before implementation. By applying four core functions fractally—from project level down to implementable components—you achieve clarity, modularity, and build confidence before writing a single line of code.

## Why 4F?

**The Problem:** Jumping straight into coding complex systems leads to:
- Unclear requirements and scope creep
- Tangled architecture that's hard to modify
- Missing edge cases discovered too late
- Difficulty onboarding team members

**The 4F Solution:** Specify everything recursively first, then build bottom-up:
- ✅ Complete clarity at every level before coding
- ✅ Modular architecture emerges naturally
- ✅ Test cases defined upfront
- ✅ Implementation becomes straightforward execution

## The Four Functions

Apply these four functions at each level of your system:

### 1. `writeSpec()`
**What and Why**
- What needs to be built
- Why it exists (the problem it solves)
- Success criteria
- Inputs and outputs
- Non-functional requirements

### 2. `writeArchitecture()`
**How it's structured**
- Break down into sub-components
- Define data flow between components
- Identify dependencies
- Choose technologies/patterns

### 3. `writeTestingPlan()`
**How to verify it works**
- Unit test cases for each component
- Integration test scenarios
- Test fixtures and data
- Success/failure conditions

### 4. `writeInstructions()`
**How to implement it**
- Step-by-step implementation order
- Code examples and templates
- Gotchas and edge cases
- Performance considerations

## The Recursive Process

```
PROJECT LEVEL
├─ writeSpec()          → What is the whole system?
├─ writeArchitecture()  → Break into Modules
├─ writeTestingPlan()   → How to test the system?
└─ writeInstructions()  → Implementation phases
    │
    ├─ MODULE LEVEL (for each module)
    │   ├─ writeSpec()          → What does this module do?
    │   ├─ writeArchitecture()  → Break into Sub-components
    │   ├─ writeTestingPlan()   → Module test plan
    │   └─ writeInstructions()  → Component implementation
    │       │
    │       └─ SUB-COMPONENT LEVEL (if needed)
    │           ├─ writeSpec()
    │           ├─ writeArchitecture()
    │           ├─ writeTestingPlan()
    │           └─ writeInstructions()
    │
    └─ STOP when components are simple enough to just code
```

**Key Insight:** Recurse as deep as needed. Stop when the task is small enough to implement directly from the instructions.

## Implementation Strategy

### Spec Phase (Top-Down)
1. Start at project level
2. Apply all 4 functions
3. Identify modules
4. Recurse into each module
5. Apply 4 functions again
6. Continue until components are implementable

### Build Phase (Bottom-Up)
1. Start with modules that have **no dependencies**
2. Implement following the instructions
3. Test thoroughly before moving up
4. Integrate modules layer by layer
5. Final system integration

## Quick Start Guide

### Step 1: Project Setup
Create your project structure:
```
my-project/
├── PROJECT-SPEC.md
├── MODULE-1-[NAME].md
├── MODULE-2-[NAME].md
├── MODULE-3-[NAME].md
└── src/
    └── (implementation goes here)
```

### Step 2: Apply 4F at Project Level

**Example: PROJECT-SPEC.md**
```markdown
# My Project - Specification

## writeSpec()
### What We're Building
[Describe the system]

### Why This Exists
[The problem it solves]

### Success Criteria
1. [Measurable outcome 1]
2. [Measurable outcome 2]

### Inputs/Outputs
- Input: [What comes in]
- Output: [What goes out]

## writeArchitecture()
### Module Breakdown
- Module 1: [Name] - [Purpose]
- Module 2: [Name] - [Purpose]
- Module 3: [Name] - [Purpose]

### Data Flow
[Diagram or description]

## writeTestingPlan()
### Test Strategy
- Unit tests: [Approach]
- Integration tests: [Scenarios]
- Test fixtures: [What data]

## writeInstructions()
### Implementation Order
Phase 1: Build Module 3 (no dependencies)
Phase 2: Build Module 1
Phase 3: Build Module 2 (depends on 1, 3)
Phase 4: Integration
```

### Step 3: Recurse to Module Level

**Example: MODULE-1-NAME.md**
```markdown
# Module 1: [Name] - Specification

## writeSpec()
### What This Module Does
[Specific functionality]

### Why This Module Exists
[Its role in the system]

### Inputs/Outputs
- Input: [Data structures]
- Output: [Data structures]

## writeArchitecture()
### Sub-Components
1. Component A: [Purpose]
2. Component B: [Purpose]
3. Component C: [Purpose]

### Data Flow
[How data moves through components]

## writeTestingPlan()
### Component A Tests
- test_valid_input()
- test_invalid_input()
- test_edge_case()

### Component B Tests
[...]

## writeInstructions()
### Implementation Order
Step 1: Implement Component A
```python
def component_a(input):
    # Implementation guide
    pass
```

Step 2: Implement Component B
[...]
```

### Step 4: Implement Bottom-Up

Start with the module that has no dependencies:

```python
# Implement Module 3 first (depends on nothing)
# Test it thoroughly
# Then implement Module 1
# Test it thoroughly
# Then implement Module 2 (depends on 1 and 3)
# Test it thoroughly
# Finally, integration test
```

## Real-World Example

See the **PR Interaction Report Generator** project for a complete 4F implementation:
- 📁 [GitHub Repository](https://github.com/mattbeane/pr-interaction-report)
- Built in one session using 4F
- 4 modules, 61 tests, all passing
- Complete specs → working code

### What It Demonstrates

**Project Level:**
- Clear problem definition (analyze AI-assisted coding sessions)
- 4 distinct modules identified
- Test strategy defined
- Bottom-up build order specified

**Module Level:**
- Each module has complete 4F treatment
- Sub-components clearly defined
- Implementation code included in instructions
- Tests written before implementation

**Results:**
- 8,421 lines of code
- 61 passing tests
- Clean modular architecture
- Built in a single development session

## Templates

### Project Template

```markdown
# [Project Name] - Specification

## writeSpec()
### What We're Building
### Why This Exists
### Success Criteria
### Inputs/Outputs
### Constraints

## writeArchitecture()
### Module Breakdown
### Data Flow
### Dependencies
### Technology Stack

## writeTestingPlan()
### Test Strategy
### Test Fixtures
### Success Criteria

## writeInstructions()
### Implementation Order
### Development Rules
### Metrics for Success
```

### Module Template

```markdown
# Module [N]: [Name] - Specification

## writeSpec()
### What This Module Does
### Why This Module Exists
### Inputs
### Outputs
### Success Criteria
### Error Handling

## writeArchitecture()
### Sub-Components
### Data Flow
### Dependencies

## writeTestingPlan()
### Test Cases
### Integration Tests
### Test Fixtures

## writeInstructions()
### Implementation Order
### Code Examples
### Implementation Rules
```

## Best Practices

### ✅ Do This

1. **Be Complete, Not Perfect**: Specs don't need to be exhaustive, but should cover the essentials
2. **Stop at the Right Level**: Don't over-recurse. If you can implement it from the instructions, stop
3. **Build Dependencies First**: Always implement modules with no dependencies before dependent modules
4. **Test Each Layer**: Don't move up until current layer tests pass
5. **Keep Specs Updated**: If implementation reveals issues, update the spec

### ❌ Avoid This

1. **Don't Skip Functions**: All 4 functions matter at each level
2. **Don't Jump to Code**: Resist the urge to start coding before specs are done
3. **Don't Spec Too Deep**: Recursing to every tiny function defeats the purpose
4. **Don't Build Top-Down**: You'll have integration issues. Build bottom-up.
5. **Don't Abandon Specs**: They're living documentation, not write-once artifacts

## When to Use 4F

**Perfect for:**
- ✅ Complex systems with multiple modules
- ✅ Team projects (specs align everyone)
- ✅ Learning new domains (specs force clarity)
- ✅ High-stakes projects (catch issues early)
- ✅ AI-assisted coding (gives AI clear instructions)

**Overkill for:**
- ❌ Simple scripts (<100 lines)
- ❌ Prototypes/experiments
- ❌ Well-understood patterns you've done 100x

## Working with AI (Like Claude)

The 4F Method works exceptionally well with AI coding assistants:

### AI + 4F Workflow

1. **You write the specs** (or work with AI to write them)
2. **AI helps with architecture** (suggests module breakdowns)
3. **You define test cases** (AI can help generate edge cases)
4. **AI implements from instructions** (straightforward execution)

### Why This Works

- AI excels at implementation when given clear specs
- Reduces hallucination (everything is specified)
- Easy to verify (tests are pre-defined)
- Iterative refinement (update specs, regenerate code)

### Example Prompt

```
I'm using the 4F Method. Here's my MODULE-2 spec:

[paste spec]

Please implement Component A following the instructions in
writeInstructions(). The tests are defined in writeTestingPlan().
```

## FAQ

### Q: How long does the spec phase take?

**A:** Usually 20-30% of total project time. A project that would take 10 hours to code might take 2-3 hours to spec fully. But you save that time (and more) by avoiding rework.

### Q: Can I use 4F for existing projects?

**A:** Yes! Apply it to new modules or when refactoring. Create specs for what exists, then recurse for new components.

### Q: What if requirements change?

**A:** Update the specs at the appropriate level, then regenerate affected code. The modular structure makes changes easier to isolate.

### Q: Do I always need all 4 functions?

**A:** For complete clarity, yes. But for tiny components, you might combine them. The key is having answers to: What? How? How to test? How to implement?

### Q: How deep should I recurse?

**A:** Until you can implement directly from the instructions. If you're writing pseudo-code that's basically real code, you've gone deep enough.

## Resources

### Examples
- **PR Interaction Report Generator**: [GitHub](https://github.com/mattbeane/pr-interaction-report)
  - Complete 4F implementation
  - Project + 4 modules fully specified
  - 61 tests, all passing

### Templates
- Project Template (included above)
- Module Template (included above)
- Copy and customize for your needs

### Community
- Share your 4F projects
- Contribute templates and patterns
- Report what works (and what doesn't)

## Credits

**Created by:** Daniel Rock ([@danielrock](https://github.com/danielrock))

**Documented by:** Matt Beane, with Claude Code

**Method Philosophy:**
> "Spec everything recursively first, then build bottom-up. When done right, implementation becomes straightforward execution."

## License

This methodology documentation is shared freely. Use it, remix it, share it.

---

## Get Started

1. **Copy the templates** above
2. **Pick a project** (start small!)
3. **Apply 4F at project level** (all 4 functions)
4. **Recurse to modules** (all 4 functions again)
5. **Stop when implementable** (don't over-spec)
6. **Build bottom-up** (dependencies first)
7. **Test each layer** (green tests before moving up)

**Remember:** The goal is clarity, not perfection. Spec enough to code confidently, then ship.

🚀 **Happy building with 4F!**
