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

## Two Approaches

**4F Method works for both greenfield and existing codebases:**

### Greenfield (Building New)
Top-down specification → bottom-up implementation
- Start with requirements
- Recurse through architecture
- Build from dependencies up

### Existing Codebase (4F-EC)
Bottom-up understanding → risk-ordered fixes
- Reverse-engineer spec from code
- Find all related bugs
- Fix systematically (least risky → most risky)

[See 4F for Existing Codebases](4f-existing-codebase.md) for detailed methodology.

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

### Step 0: Define Your Profile

**Before starting, customize 4F for your skill level:**

The 4F Method adapts to developers of all backgrounds. Use the [User Profile Template](templates/user-profile.md) to:
- Define your code familiarity (new/learning/experienced/senior)
- Set your learning preferences (how much explanation you want)
- Establish safety requirements (personal/team/production)
- Configure "The Deal" with Claude (working norms)

**Recommended:** Copy the profile template to your project's `.claude.md` file before beginning.

[Learn more about The Deal](the-deal.md) - Working norms that reduce friction and improve output quality.

### Step 1: Project Setup
Create your project structure:
```
my-project/
├── .claude.md            ← Your profile and working norms
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

### Blog Platform Built with 4F

A complete blogging platform demonstrating the 4F Method:

**Project Level:**
- Clear problem definition (users need to publish and discover content)
- 4 distinct modules identified (Auth, Content, Comments, Search)
- Test strategy defined
- Bottom-up build order specified

**Module Level:**
- Each module has complete 4F treatment
- Sub-components clearly defined
- Implementation code included in instructions
- Tests written before implementation

**Results:**
- ~5,000 lines of code
- 45+ passing tests
- Clean modular architecture
- Built systematically with no rework

See EXAMPLES.md for detailed walkthrough.

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

**A:** Yes! Use [4F for Existing Codebases (4F-EC)](4f-existing-codebase.md) - a bottom-up methodology that reverses the process. Instead of spec → code, you do code → spec → systematic fixes. Great for bug hunts, legacy code, and inherited projects.

See [Daniel's Bug Hunt](examples/daniels-bug-hunt.md) for a real example: 8 bugs fixed in 90 minutes using 4F-EC.

### Q: I'm new to coding. Can I use 4F?

**A:** Absolutely. Start with the [User Profile Template](templates/user-profile.md) to customize 4F for your level. The method adapts - experienced developers move faster, learners get more explanation. The core process is the same.

### Q: What if requirements change?

**A:** Update the specs at the appropriate level, then regenerate affected code. The modular structure makes changes easier to isolate.

### Q: Do I always need all 4 functions?

**A:** For complete clarity, yes. But for tiny components, you might combine them. The key is having answers to: What? How? How to test? How to implement?

### Q: How deep should I recurse?

**A:** Until you can implement directly from the instructions. If you're writing pseudo-code that's basically real code, you've gone deep enough.

## Resources

### Core Methodology
- **[4F for Existing Codebases (4F-EC)](4f-existing-codebase.md)** - Bottom-up approach for legacy code, bug hunts, inherited projects
- **[The Deal](the-deal.md)** - Working norms with Claude (reduces friction, enables honest feedback)
- **[Meta-Automation](advanced/meta-automation.md)** - Apply 4F recursively to your productivity systems

### Templates & Workflows
- **[User Profile Template](templates/user-profile.md)** - Customize 4F for your skill level and learning style
- **[Bug Fix Workflow](templates/bug-fix-workflow.md)** - Step-by-step guide with prompts for fixing bugs systematically
- **Project Template** (included above) - Greenfield 4F structure
- **Module Template** (included above) - Component-level specification

### Examples
- **[Daniel's Bug Hunt](examples/daniels-bug-hunt.md)** - Real case study: 8 bugs fixed in 90 minutes with 4F-EC
- **Blog Platform Example** (see EXAMPLES.md) - Complete greenfield walkthrough with project + 4 modules fully specified

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
