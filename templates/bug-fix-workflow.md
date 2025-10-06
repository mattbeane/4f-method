# Bug Fix Workflow (4F-EC Applied)

**Use this template when:** Fixing bugs in existing code, especially critical production issues.

**Based on:** [4F Method for Existing Codebases](../4f-existing-codebase.md)

---

## Quick Start

**Have a bug to fix?** Copy these prompts and work through them with Claude in order.

**Time commitment:** ~90 minutes for comprehensive bug hunt (faster for single bugs)

---

## Phase 1: Reverse Engineer Spec (15 min)

### Prompt:
```
I have [codebase/module/file] with [problem description].

Help me reverse-engineer the original spec. What was this supposed to do?
Read the code and document the intended behavior.

Create a SPEC.md file with:
1. Purpose: What problem does this solve?
2. Expected behavior: What should happen?
3. Inputs: What data comes in?
4. Outputs: What data goes out?
5. Edge cases: What special conditions should be handled?
```

### Expected Output:
- `SPEC.md` file with reverse-engineered specification
- Clear description of intended behavior
- Understanding of what "correct" looks like

### Success Check:
- [ ] I understand what this code was supposed to do
- [ ] I can explain the intended behavior in my own words
- [ ] I know what inputs/outputs are expected

---

## Phase 2: Document Current Architecture (15 min)

### Prompt:
```
Now document the actual architecture. Map the key files, functions, and
data flows. Show me what it *actually* does vs. what it should do per the spec.

Create ARCHITECTURE.md with:
1. Key components: Main files/classes/functions
2. Data flow: How data moves through the system
3. Dependencies: What depends on what?
4. Entry points: Where does execution start?
5. Divergence points: Where does reality differ from spec?
```

### Expected Output:
- `ARCHITECTURE.md` with system structure
- Visual diagram or clear description of data flow
- Identified gaps between intent and reality

### Success Check:
- [ ] I know which files/functions are involved
- [ ] I understand the data flow
- [ ] I can see where spec and reality diverge

---

## Phase 3: Identify All Related Bugs (20 min)

### Prompt:
```
Given this spec and architecture, find ALL related bugs - not just the one
reported. Look for:

- Edge cases (null, empty, invalid inputs)
- Race conditions (concurrent access)
- Type mismatches (string vs int, etc.)
- Logic errors (wrong comparisons, off-by-one)
- Security issues (injection, validation)
- Performance issues (N+1 queries, memory leaks)

Create BUG-INVENTORY.md with:
1. Bug ID
2. Description
3. Root cause
4. Severity (Critical/High/Medium/Low)
5. Files affected
6. Example scenario where it breaks
```

### Expected Output:
- `BUG-INVENTORY.md` with comprehensive bug list
- Root cause analysis for each bug
- Severity rankings

### Success Check:
- [ ] Found the reported bug
- [ ] Found related bugs in similar code
- [ ] Understand root cause for each bug
- [ ] Know which bugs are critical vs. nice-to-fix

---

## Phase 4: Create Risk-Ordered Fix Plan (10 min)

### Prompt:
```
Create modular fixes for each bug. Order them least risky → most risky.
Each fix should be one commit. Show dependencies.

Create FIX-PLAN.md with for each fix:
1. Fix ID (matches Bug ID)
2. Description (one-line summary)
3. Risk level (Low/Medium/High) with reasoning
4. Dependencies (what must be fixed first)
5. Test strategy (how to verify)
6. Rollback plan (how to undo if it breaks)

Risk assessment criteria:
- Low: Isolated change, clear fix, easy to test
- Medium: Touches multiple places, or complex logic
- High: Core functionality, concurrency, data migration
```

### Expected Output:
- `FIX-PLAN.md` with ordered list of fixes
- Risk justification for each fix
- Clear test strategy

### Success Check:
- [ ] Fixes are ordered least risky → most risky
- [ ] Each fix is modular (one commit)
- [ ] Dependencies are clear
- [ ] I know how to test each fix

---

## Phase 5: Execute Fixes (Varies)

### For Each Fix:

#### Step 1: Implement
```
Let's implement Fix #[N]: [description]

Reminder:
- Single, focused change
- Follows risk: [Low/Med/High]
- Tests: [test strategy from plan]

Show me the code change.
```

#### Step 2: Review
- Read the code change
- Verify it matches the fix plan
- Check for unintended side effects

#### Step 3: Test
```
Run tests for this fix:
[Paste test strategy from FIX-PLAN.md]

Show me:
1. Test commands to run
2. Expected output
3. How to verify the fix works
```

#### Step 4: Commit
```
Create git commit with this message format:

Fix #[N]: [Brief description] (Risk: [Low/Med/High])

- Root cause: [Why it was broken]
- Solution: [What changed]
- Testing: [How verified]
- Files: [List of changed files]

Then run: git commit -am "[message]"
```

#### Step 5: Verify
- Run full test suite
- Check nothing else broke
- If breaks: `git reset --hard HEAD~1` and re-assess

#### Step 6: Next Fix
- Move to next fix in sequence
- Repeat steps 1-5

---

## Phase 6: Final Review & Ship (10 min)

### Prompt:
```
All fixes are implemented. Let's review:

1. Run full test suite
2. Check diff of all changes: git diff [original-commit]..HEAD
3. Verify each bug is fixed
4. Check for any new issues

Create COMPLETION-REPORT.md with:
- Bugs fixed (list with IDs)
- Commits made (list with hashes)
- Test results (all passing?)
- Known issues remaining (if any)
- Recommendations for future (prevent similar bugs)
```

### Expected Output:
- `COMPLETION-REPORT.md` with summary
- All tests passing
- Clean git history (one commit per fix)

### Success Check:
- [ ] All bugs fixed
- [ ] All tests pass
- [ ] Git history is clean
- [ ] Ready for senior review

---

## Safety Checklist

Before shipping to production:

- [ ] All tests pass (automated + manual)
- [ ] Code reviewed by senior developer
- [ ] Changes tested in staging environment
- [ ] Rollback plan documented
- [ ] Monitoring/alerts configured
- [ ] Team notified of changes

---

## Example: Real Bug Hunt

### Context
API server with reported null pointer exception in user login.

### Phase 1: Reverse Engineer (15 min)
**Created:** `SPEC.md` describing login flow
- User submits email/password
- System validates credentials
- Returns JWT token on success
- Returns error on failure

### Phase 2: Document Architecture (15 min)
**Created:** `ARCHITECTURE.md` mapping flow
```
Route: POST /login
  → Controller: AuthController.login()
    → Service: AuthService.validateUser()
      → Database: Users.findByEmail()
    → Service: TokenService.generateJWT()
  → Response: {token, user}
```

### Phase 3: Find All Bugs (20 min)
**Created:** `BUG-INVENTORY.md` with 4 bugs
1. **Critical:** Null pointer when user not found (reported bug)
2. **High:** No rate limiting (brute force vulnerability)
3. **Medium:** JWT expiry not validated
4. **Low:** Email comparison is case-sensitive

**Root causes identified:**
- Missing null checks after database queries
- No security middleware
- Token validation incomplete

### Phase 4: Risk-Ordered Plan (10 min)
**Created:** `FIX-PLAN.md` ordering:
1. Fix null check (Low risk - straightforward)
2. Fix email case sensitivity (Low risk - simple)
3. Fix JWT validation (Medium risk - touches auth)
4. Add rate limiting (High risk - new middleware)

### Phase 5: Execute (30 min)
**Implemented** 4 fixes as 4 commits:
```bash
git log --oneline
a1b2c3d Fix #4: Add rate limiting middleware (Risk: High)
e4f5g6h Fix #3: Validate JWT expiry (Risk: Medium)
i7j8k9l Fix #2: Case-insensitive email comparison (Risk: Low)
m0n1o2p Fix #1: Add null check after user lookup (Risk: Low)
```

**All tests passing:** ✅

### Phase 6: Ship (5 min)
**Created:** `COMPLETION-REPORT.md`
- 4 bugs fixed
- 4 commits made
- All tests pass
- Shipped to senior dev for review

**Senior dev feedback:** Approved, merged to main

**Total time:** 1 hour 35 minutes (including breaks)

---

## Troubleshooting

### "I found too many bugs, overwhelmed"
**Solution:** Start with just the reported bug. Fix it. Then do another bug hunt for related issues.

### "High-risk fix broke things"
**Solution:** `git reset --hard HEAD~1` to rollback. Re-assess the fix. Maybe split into smaller pieces.

### "Not sure which fixes are high vs low risk"
**Solution:** Ask Claude: "Rate this fix's risk and explain why." Err on side of caution.

### "Tests don't exist"
**Solution:** Write basic tests first, then fix bugs. Or manually test each fix thoroughly.

### "Senior dev unavailable for review"
**Solution:** Use Draft PRs. Document thoroughly. Wait for review before merge.

---

## Next Steps

**After your first bug hunt:**
1. Review what worked / what didn't
2. Update this template with your learnings
3. Share your `COMPLETION-REPORT.md` as example
4. Contribute improvements via PR

**Related:**
- [4F Existing Codebase](../4f-existing-codebase.md) - Full methodology
- [The Deal](../the-deal.md) - Setting working norms
- [Examples](../EXAMPLES.md) - More real-world cases

---

**Ready?** Copy the Phase 1 prompt and start your bug hunt! 🐛🔨
