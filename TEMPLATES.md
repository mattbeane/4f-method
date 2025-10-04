# 4F Method Templates

Copy-paste these templates to get started with the 4F Method.

## Project-Level Template

```markdown
# [Project Name] - Specification

**Created:** [Date]
**Method:** 4F (Four-Function Fractal)
**Owner:** [Your Name]

---

## writeSpec()

### What We're Building
[1-2 paragraph description of the system you're building]

### Core Problem
[What problem does this solve? Why does it need to exist?]

### User Story
**As a** [type of user]
**I want to** [do something]
**So that** [I can achieve this benefit]

### Success Criteria
1. [Measurable outcome 1]
2. [Measurable outcome 2]
3. [Measurable outcome 3]

### Input Data Format
```json
[Example of what comes in]
```

### Output Format
```json
[Example of what goes out]
```

### Constraints
- **Performance:** [Requirements]
- **Scale:** [How much data/traffic]
- **Security:** [Privacy, auth requirements]
- **Compatibility:** [Platforms, versions]

### Out of Scope (V1)
- [What you're NOT building in first version]
- [Features deferred to later]

---

## writeArchitecture()

### System Architecture

```
[ASCII diagram or description of overall system]
```

### Module Breakdown

**MODULE 1: [Name]**
- [Brief description]
- [Key responsibility]

**MODULE 2: [Name]**
- [Brief description]
- [Key responsibility]

**MODULE 3: [Name]**
- [Brief description]
- [Key responsibility]

**MODULE 4: [Name]**
- [Brief description]
- [Key responsibility]

### Data Flow

```
[Show how data moves through the system]
```

### Technology Stack
- **Language:** [Python, JavaScript, etc.]
- **Storage:** [Database, files, etc.]
- **Framework:** [If any]
- **Testing:** [Test framework]
- **External Dependencies:** [APIs, libraries]

---

## writeTestingPlan()

### Testing Strategy

**Unit Tests (Per Module):**
- [What each module tests]

**Integration Tests:**
- [How modules work together]
- [End-to-end scenarios]

**Test Data:**
- **Fixture 1:** [Description] - [Use case]
- **Fixture 2:** [Description] - [Use case]
- **Fixture 3:** [Description] - [Use case]

### Success Criteria
- [X]% test coverage on core logic
- All integration tests pass
- Performance benchmarks met
- [Other criteria]

---

## writeInstructions()

### Implementation Approach

**Phase 1: Foundation**
1. [First module to build - no dependencies]
2. [Setup and scaffolding tasks]

**Phase 2: Core Logic**
1. [Second module]
2. [Third module]

**Phase 3: Integration**
1. [How modules connect]
2. [Integration tests]

**Phase 4: Polish**
1. [Error handling]
2. [Performance]
3. [Documentation]

### Development Rules
- **One module at a time** - Complete before moving on
- **Test first** - Write fixtures before implementation
- **Keep it modular** - Clean interfaces between components
- **Document as you go** - Docstrings and comments

### Metrics for Success
- [How you measure if it's working]
- [Performance targets]
- [Quality indicators]

---

## Next Steps: Recursive Decomposition

Now recurse down to MODULE 1 and apply the four functions again:
- MODULE 1 SPEC
- MODULE 1 ARCHITECTURE
- MODULE 1 TESTING PLAN
- MODULE 1 INSTRUCTIONS

Repeat for each module, then implement bottom-up.
```

---

## Module-Level Template

```markdown
# MODULE [N]: [Module Name] - Specification

**Parent:** [Project Name]
**Created:** [Date]
**Level:** Module (L2)

---

## writeSpec()

### What This Module Does
[1-2 paragraphs explaining the module's specific responsibility]

### Why This Module Exists
- [Reason 1]
- [Reason 2]
- [Reason 3]

### Inputs (What Comes In)
```python
[Type definitions or examples]
```

**Possible issues with input:**
- [Edge case 1]
- [Edge case 2]
- [Validation needs]

### Outputs (What Goes Out)
```python
[Type definitions or examples]
```

### Success Criteria
1. [What makes this module successful]
2. [Performance requirement]
3. [Quality requirement]

### Error Handling Strategy
- **[Error Type 1]:** [How to handle]
- **[Error Type 2]:** [How to handle]
- **Warnings (non-fatal):** [What to log but continue]

---

## writeArchitecture()

### Sub-Components

```
MODULE [N]: [Name]
├─ Component A: [Name]
│   └─ [Responsibility]
├─ Component B: [Name]
│   └─ [Responsibility]
├─ Component C: [Name]
│   └─ [Responsibility]
└─ Component D: [Name]
    └─ [Responsibility]
```

### Data Flow Through Module

```
Input
  ↓
[Component A]
  ↓
[Component B]
  ↓
[Component C]
  ↓
Output
```

### Sub-Component Details

**Component A: [Name]**
- Input: [What it receives]
- Output: [What it produces]
- Errors: [What can go wrong]
- Dependencies: [External libraries]

**Component B: [Name]**
- Input: [What it receives]
- Output: [What it produces]
- Errors: [What can go wrong]
- Logic: [Key algorithm or process]

[Repeat for all components]

### Dependencies
- **External:** [Libraries, APIs]
- **Internal:** [Other modules this depends on]

---

## writeTestingPlan()

### Test Cases

**Component A Tests**
```python
def test_valid_input():
    # [What this tests]

def test_invalid_input():
    # [What this tests]

def test_edge_case():
    # [What this tests]
```

**Component B Tests**
```python
def test_[scenario]():
    # [What this tests]
```

[Continue for all components]

### Integration Tests (For This Module)
```python
def test_end_to_end_valid_input():
    # [Full module flow - happy path]

def test_end_to_end_with_errors():
    # [Error handling]
```

### Test Fixtures
```python
# fixture_1_[name].json - [Description]
{
  [Example test data]
}

# fixture_2_[name].json - [Description]
{
  [Example edge case data]
}
```

### Success Criteria
- All unit tests pass ([X]+ tests)
- Integration tests cover happy path + errors
- Fixtures cover realistic scenarios
- [Performance target if applicable]

---

## writeInstructions()

### Implementation Order

**Step 1: Define Data Models**
```python
[Code example for data structures]
```

**Step 2: Implement Component A**
```python
[Implementation guidance with code]
```

**Step 3: Implement Component B**
```python
[Implementation guidance with code]
```

**Step 4: Implement Component C**
```python
[Implementation guidance with code]
```

**Step 5: Wire Components Together**
```python
[Main orchestration code]
```

**Step 6: Write Tests**
- Create `tests/test_[module_name].py`
- Implement test cases from testing plan
- Create test fixtures
- Run tests, ensure all pass

**Step 7: Document**
- Add docstrings
- Create usage examples
- Document error handling

### Implementation Rules for This Module
- [Rule 1]
- [Rule 2]
- [Rule 3]

### Testing Before Moving On
```bash
# Must pass before considering module complete
[Test command]
# Target: [Coverage/quality goal]
```

---

## Next Steps

[If this module has complex sub-components, recurse down another level]

**OR**

[If components are simple enough, proceed to implementation]

**Ready to build!**
```

---

## Sub-Component Template (Optional - Use if needed)

```markdown
# SUB-COMPONENT: [Name]

**Parent Module:** MODULE [N]
**Created:** [Date]
**Level:** Sub-Component (L3)

---

## writeSpec()
### What This Component Does
[Specific function]

### Inputs/Outputs
- Input: [Type/format]
- Output: [Type/format]

---

## writeArchitecture()
### Implementation Approach
[Algorithm or pattern to use]

### Key Functions
- `function_a()` - [Purpose]
- `function_b()` - [Purpose]

---

## writeTestingPlan()
### Test Cases
- [Test 1]
- [Test 2]
- [Test 3]

---

## writeInstructions()
### Implementation
```python
[Complete implementation code]
```
```

---

## Quick Reference Card

### When at PROJECT level:
1. ✅ `writeSpec()` - Define the whole system
2. ✅ `writeArchitecture()` - Break into modules
3. ✅ `writeTestingPlan()` - System test strategy
4. ✅ `writeInstructions()` - Implementation phases

### When at MODULE level:
1. ✅ `writeSpec()` - What this module does
2. ✅ `writeArchitecture()` - Break into components
3. ✅ `writeTestingPlan()` - Module tests
4. ✅ `writeInstructions()` - Component implementation

### When at COMPONENT level:
1. ✅ `writeSpec()` - Component responsibility
2. ✅ `writeArchitecture()` - Functions/classes
3. ✅ `writeTestingPlan()` - Unit tests
4. ✅ `writeInstructions()` - Code to write

### STOP recursing when:
- ✋ You can implement directly from instructions
- ✋ The code is obvious from the spec
- ✋ You're basically writing the implementation in the spec

### Build order:
1. 🔨 Modules with NO dependencies first
2. 🔨 Then modules that depend on those
3. 🔨 Test each before moving up
4. 🔨 Finally: integration

---

## File Naming Convention

```
project-root/
├── PROJECT-SPEC.md           # Project level 4F
├── MODULE-1-[NAME].md        # Module 1
├── MODULE-2-[NAME].md        # Module 2
├── MODULE-3-[NAME].md        # Module 3
└── src/
    ├── module1/
    ├── module2/
    └── module3/
```

---

## Copy This Checklist

### Project Setup
- [ ] Create PROJECT-SPEC.md from template
- [ ] Apply `writeSpec()` at project level
- [ ] Apply `writeArchitecture()` - identify modules
- [ ] Apply `writeTestingPlan()` - test strategy
- [ ] Apply `writeInstructions()` - build order

### For Each Module
- [ ] Create MODULE-N-[NAME].md from template
- [ ] Apply `writeSpec()` at module level
- [ ] Apply `writeArchitecture()` - identify components
- [ ] Apply `writeTestingPlan()` - component tests
- [ ] Apply `writeInstructions()` - implementation code
- [ ] Recurse deeper if needed

### Implementation
- [ ] Start with module that has NO dependencies
- [ ] Implement following instructions
- [ ] Write and run tests (must pass!)
- [ ] Move to next module up dependency chain
- [ ] Repeat until all modules done
- [ ] Run integration tests
- [ ] Ship it! 🚀

---

Use these templates as starting points. Customize based on your project's needs. The key is having clear answers to: **What? How? How to test? How to implement?**
