# 4F Method for Existing Codebases (4F-EC)

**When to Use:** Inheriting legacy code, fixing critical bugs, or understanding unfamiliar codebases quickly

**Key Difference:** Greenfield 4F works top-down (spec → code). Existing codebase 4F works bottom-up (code → spec).

---

## The Problem

You have a codebase with:
- Critical bugs in production
- No documentation or outdated docs
- Previous developer gone
- Unclear original intent
- Time pressure to fix

**Traditional approach:** Poke around, make changes, hope nothing breaks.

**4F-EC approach:** Reverse-engineer understanding, fix systematically.

---

## The 4F-EC Process

### Phase 1: Reverse Engineering (30 min)

**Goal:** Understand what this code was *supposed* to do

**Steps:**
1. **Discover Intent** - Read any docs, comments, commit messages
2. **Infer Purpose** - What problem was this solving?
3. **Map Behavior** - What does it actually do now?
4. **Identify Gaps** - Where does reality diverge from intent?

**Output:** `SPEC.md` - The reverse-engineered specification

**Prompt:**
```
I have [codebase/module] that [problem description]. Help me reverse-engineer
the original spec. What was this supposed to do? Read the code and document
the intended behavior.
```

---

### Phase 2: Architecture Documentation (20 min)

**Goal:** Map the actual structure and data flows

**Steps:**
1. **Key Components** - What are the main files/modules/classes?
2. **Data Flow** - How does data move through the system?
3. **Dependencies** - What depends on what?
4. **Entry Points** - Where does execution start?

**Output:** `ARCHITECTURE.md` - Current system structure

**Prompt:**
```
Now document the actual architecture. Map the key files, functions, and
data flows. Show me what it *actually* does vs. what it should do per the spec.
```

---

### Phase 3: Problem Identification (20 min)

**Goal:** Find ALL bugs, not just the reported one

**Steps:**
1. **List Bad Behaviors** - What's broken? (known + discovered)
2. **Root Cause Analysis** - Why is each thing broken?
3. **Ripple Effects** - What else might be affected?
4. **Severity Ranking** - Critical vs. Important vs. Nice-to-fix

**Output:** `BUG-INVENTORY.md` - Comprehensive bug list with root causes

**Prompt:**
```
Given this spec and architecture, find ALL related bugs - not just the one
reported. Look for: edge cases, race conditions, null handling, type mismatches,
logic errors, security issues. Create comprehensive bug inventory with root causes.
```

**Why find all bugs now?**
- Fixing one bug often reveals related issues
- Better to fix together than in separate emergency sessions
- Understanding root causes prevents future bugs

---

### Phase 4: Risk-Ordered Planning (15 min)

**Goal:** Sequence fixes to minimize risk of new breaks

**Steps:**
1. **Modular Fixes** - One bug = one fix = one commit
2. **Risk Assessment** - Rate each fix: Low/Medium/High risk
3. **Dependency Mapping** - What must be fixed first?
4. **Sequencing** - Order: Least risky → Most risky

**Output:** `FIX-PLAN.md` - Ordered list of fixes with risk levels

**Prompt:**
```
Create modular fixes for each bug. Order them least risky → most risky.
Each fix should be one commit. Show dependencies. Explain risk assessment.
```

**Why least-risky first?**
- Build confidence with easy wins
- If high-risk fix breaks things, you have working foundation to fall back to
- Incremental testing catches issues early

---

### Phase 5: Disciplined Execution

**Goal:** Fix systematically without creating new problems

**Steps for each fix:**
1. **Implement** - Make the change
2. **Test** - Run all tests (automated + manual)
3. **Commit** - Single commit with clear message
4. **Verify** - Confirm fix works, nothing else broke
5. **Next** - Move to next fix in sequence

**Commit message format:**
```
Fix #N: [Brief description] (Risk: Low/Med/High)

- Root cause: [Why it was broken]
- Solution: [What changed]
- Testing: [How verified]
```

**If something breaks:**
1. Stop immediately
2. Rollback to last working commit (`git reset --hard HEAD~1`)
3. Re-assess the fix
4. Try again or skip to next fix

---

## Real-World Example: Daniel's Bug Hunt

**Context:** API server with 8-9 critical bugs, breakfast meeting in 1.5 hours

**Phase 1: Reverse Engineering (20 min)**
- Read API endpoints and controller code
- Documented intended behavior from route definitions
- Created SPEC.md describing what each endpoint should do

**Phase 2: Architecture (15 min)**
- Mapped request flow: Routes → Controllers → Services → Database
- Identified middleware chain
- Found data validation points

**Phase 3: Bug Discovery (30 min)**
- Started with 1 reported bug (null pointer)
- Found 8 related bugs by examining similar code:
  - 3 null handling issues
  - 2 type mismatches
  - 2 edge case failures
  - 1 race condition
- Documented root cause for each

**Phase 4: Risk Ordering (10 min)**
```
1. Fix null checks in input validation (Low risk - straightforward)
2. Fix type conversions (Low risk - clear errors)
3. Fix edge case in pagination (Medium risk - touches query logic)
4. Fix race condition in cache (High risk - concurrency)
```

**Phase 5: Execution (15 min)**
- Implemented fixes in order as commits
- Tested after each commit
- All bugs fixed, zero new breaks
- Shipped to senior dev for review

**Result:** 8 bugs fixed in 1.5 hours, breakfast on time, senior dev approved

---

## Key Differences: Greenfield vs. Existing Codebase

| Aspect | Greenfield 4F | Existing Codebase 4F-EC |
|--------|---------------|-------------------------|
| **Direction** | Top-down (spec → code) | Bottom-up (code → spec) |
| **Starting Point** | Requirements | Broken code |
| **Documentation** | Write as you build | Reverse-engineer |
| **Risk** | New bugs from scratch | Breaking existing functionality |
| **Testing** | Build tests first | Preserve existing behavior |
| **Commits** | Feature completion | Single bug fixes |

---

## When to Use Which Approach

**Use Greenfield 4F when:**
- Building new features from scratch
- Starting new projects
- Clear requirements exist
- No existing code to preserve

**Use 4F-EC when:**
- Fixing bugs in production
- Inheriting legacy code
- No documentation exists
- Time pressure to understand and fix
- Need to preserve existing functionality

**Use Both when:**
- Refactoring (understand existing, then rebuild)
- Adding features to legacy code (4F-EC first, then greenfield 4F for new feature)

---

## Tips for Success

### DO:
- ✅ Document as you discover (don't rely on memory)
- ✅ Find all related bugs at once (efficient batch fixing)
- ✅ Fix least-risky first (build confidence, safe fallback)
- ✅ Commit after each fix (git history = audit trail)
- ✅ Test incrementally (catch breaks immediately)

### DON'T:
- ❌ Fix the reported bug without investigating related issues
- ❌ Start with high-risk fixes (if they break, you're stuck)
- ❌ Make multiple changes in one commit (can't isolate problems)
- ❌ Skip documentation (future you will be confused)
- ❌ Rush to fix without understanding (creates more bugs)

---

## Adapting to Your Skill Level

**New to coding:**
- Take more time in Phase 1-2 (understanding the code)
- Ask Claude to explain architectural patterns as you discover them
- Start with lowest-risk fixes only
- Get code review before committing fixes

**Experienced developer:**
- Can move faster through phases
- May combine documentation steps
- Can tackle higher-risk fixes confidently
- Still document for team knowledge

**The methodology is the same - pace and risk tolerance adjust to your level.**

---

## Related Resources

- [Greenfield 4F Method](README.md) - Building from scratch
- [Bug Fix Workflow Template](templates/bug-fix-workflow.md) - Step-by-step guide
- [Example: Daniel's Bug Hunt](examples/daniels-bug-hunt.md) - Real case study
- [The Deal](the-deal.md) - Setting working norms with Claude

---

**Next Step:** Try 4F-EC on a real codebase. Use the [Bug Fix Workflow Template](templates/bug-fix-workflow.md) to guide you through your first bug hunt.
