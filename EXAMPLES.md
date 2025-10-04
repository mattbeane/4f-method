# 4F Method Examples

Real-world examples of the 4F Method in action.

## Example 1: Blog Platform

**Project:** Multi-user blogging platform with posts, comments, and search

### How 4F Was Applied

#### Project Level
- **writeSpec()**: Defined problem (users need to publish and discover content), success criteria (fast loading, good UX, scalable)
- **writeArchitecture()**: Identified 4 modules (Auth, Content Management, Comments, Search)
- **writeTestingPlan()**: Defined test fixtures (sample posts, users, comments)
- **writeInstructions()**: Specified bottom-up build (Auth → Content → Comments → Search)

#### Module Level (Applied to each of 4 modules)
Each module got full 4F treatment:

**MODULE 1: Auth Module**
- writeSpec(): User registration, login, session management
- writeArchitecture(): 3 sub-components (User Repository, Password Hasher, Session Manager)
- writeTestingPlan(): Test valid/invalid credentials, session expiry, password strength
- writeInstructions(): Use bcrypt for passwords, JWT for sessions

**MODULE 2: Content Module**
- writeSpec(): Create, edit, delete, publish posts with rich text
- writeArchitecture(): 4 sub-components (Post Repository, Markdown Parser, Image Uploader, Draft Manager)
- writeTestingPlan(): Test CRUD operations, markdown rendering, image handling
- writeInstructions(): SQLite for storage, markdown-it for parsing

**MODULE 3: Comments Module**
- writeSpec(): Threaded comments on posts, moderation
- writeArchitecture(): 3 sub-components (Comment Repository, Thread Builder, Moderation Engine)
- writeTestingPlan(): Test threading, nested replies, spam filtering
- writeInstructions(): Tree structure for threads, simple keyword filter

**MODULE 4: Search Module**
- writeSpec(): Full-text search across posts and comments
- writeArchitecture(): 3 sub-components (Indexer, Query Parser, Ranker)
- writeTestingPlan(): Test relevance, typo tolerance, filters
- writeInstructions(): SQLite FTS5 for simple implementation

### Results
- **Lines of Code**: ~5,000
- **Test Coverage**: 45+ tests, all passing
- **Time to Build**: 2 development sessions
- **Architecture**: Clean, modular, easy to extend

### Key Takeaway
By fully speccing all 4 modules before coding, implementation became straightforward execution. Each module was built independently, tested thoroughly, then integrated seamlessly.

---

## Example 2: TODO Productivity System

**Project:** Paper/digital hybrid TODO tracking with automated reconciliation

### 4F Application

#### Project Level (Simplified)

**writeSpec()**
```markdown
### What: Hybrid TODO system
- Physical paper card for dopamine (Sharpie crossing off)
- Digital tracking for analytics
- Automated reconciliation via webcam
- GTD project expansion for complex tasks

### Success Criteria:
1. Daily sprint card prints at 9 AM
2. Paper TODO reconciles to digital at 4:50 PM
3. Complexity/value tracking for analytics
4. Project vs simple task detection
```

**writeArchitecture()**
```markdown
### Modules:
1. Print Module: Generate daily sprint cards
2. Capture Module: Webcam photo of paper TODO
3. Reconcile Module: Update digital TODO.md
4. Analytics Module: Dashboard with metrics
5. Project Expansion Module: GTD clarification
```

**writeTestingPlan()**
```markdown
- Test print formatting (no Unicode issues)
- Test OCR/manual entry flow
- Test task classification (simple vs project)
- Test analytics calculations
```

**writeInstructions()**
```markdown
Phase 1: Build print module (simplest, no deps)
Phase 2: Build capture + reconcile (depends on print format)
Phase 3: Build analytics (depends on TODO format)
Phase 4: Build project expansion (depends on reconcile)
```

#### Module Level: Reconcile Module

**writeSpec()**
```markdown
### What: Reconcile paper TODO with digital TODO.md
- Input: Photo of paper TODO, existing TODO.md
- Output: Updated TODO.md with completed tasks moved to archive
- Handle: Project detection, simple task identification
```

**writeArchitecture()**
```markdown
Sub-components:
1. Task Parser: Extract tasks from manual input
2. Project Detector: Identify if task is simple vs project
3. GTD Expander: Break projects into actions
4. TODO Updater: Modify TODO.md atomically
```

**writeInstructions()**
```bash
# Step 1: Implement task parser
# Step 2: Implement project detector with heuristics
if [[ "$line" =~ ^(Setup|Create|Build) ]]; then
    IS_LIKELY_PROJECT="yes"
fi
# Step 3: Prompt user for confirmation
# Step 4: Update TODO.md
```

### Result
Working system with:
- Automated daily printing
- Manual reconciliation with AI assist
- Analytics dashboard
- Project expansion workflow

---

## Example 3: E-Commerce Product Search (Hypothetical)

Let's walk through how 4F would be applied to a product search feature.

### Project Level

#### writeSpec()
```markdown
### What: Intelligent product search with filters
Users can search products by text, filter by category/price, sort results

### Success Criteria:
1. Search returns relevant results in <200ms
2. Filters work in combination (AND logic)
3. Handles typos and synonyms
4. Results paginated (20 per page)
```

#### writeArchitecture()
```markdown
### Modules:
1. Query Parser: Parse search string, extract filters
2. Search Engine: Execute search against product DB
3. Ranking Module: Sort by relevance
4. Result Formatter: Format for UI display
```

#### writeTestingPlan()
```markdown
Test Fixtures:
- fixture_simple_search.json: "red shoes"
- fixture_filtered_search.json: "shoes category:running price:<100"
- fixture_typo.json: "sheos" → "shoes"
- fixture_empty_results.json: "asdfasdf"
```

#### writeInstructions()
```markdown
Phase 1: Build Query Parser (no dependencies)
Phase 2: Build Search Engine (depends on parser output)
Phase 3: Build Ranking (depends on search results)
Phase 4: Build Formatter (depends on ranked results)
```

### Module Level: Query Parser

#### writeSpec()
```markdown
### What: Parse search query into structured format
Input: "red running shoes price:<100 category:athletic"
Output: {
  text: "red running shoes",
  filters: {
    price: { max: 100 },
    category: "athletic"
  }
}

### Error Handling:
- Invalid filter syntax → ignore filter, keep text
- Empty query → return error
```

#### writeArchitecture()
```markdown
Sub-components:
1. Text Extractor: Separate text from filters
2. Filter Parser: Parse filter expressions
3. Validator: Validate filter values
4. Normalizer: Lowercase, trim, etc.
```

#### writeTestingPlan()
```python
def test_simple_text_query():
    # "red shoes" → {text: "red shoes", filters: {}}

def test_text_with_price_filter():
    # "shoes price:<100" → {text: "shoes", filters: {price: {max: 100}}}

def test_invalid_filter():
    # "shoes price:abc" → {text: "shoes", filters: {}}
```

#### writeInstructions()
```python
# Step 1: Implement text extractor
def extract_text(query: str) -> tuple[str, list[str]]:
    # Regex to find filter patterns
    filters = re.findall(r'(\w+):([<>]=?\d+|\w+)', query)
    text = re.sub(r'\w+:[<>]=?\d+|\w+', '', query).strip()
    return text, filters

# Step 2: Implement filter parser
def parse_filters(filter_list: list) -> dict:
    # Convert filter tuples to dict
    # Handle price operators (<, >, <=, >=)
    ...

# Step 3: Wire together
def parse_query(query: str) -> dict:
    text, filter_list = extract_text(query)
    filters = parse_filters(filter_list)
    return {"text": text, "filters": filters}
```

### Result
Clear implementation path from spec to code. Each component is testable independently.

---

## Example 4: API Rate Limiter (Small but Complete)

Even small components benefit from 4F.

### writeSpec()
```markdown
### What: Rate limiter for API endpoints
- Limit requests per user per time window
- Return 429 if limit exceeded
- Track by API key

### Success Criteria:
- Accurately enforces limits (100 req/min per user)
- Handles concurrent requests correctly
- Minimal performance overhead (<1ms)
```

### writeArchitecture()
```markdown
Components:
1. Request Counter: Track requests per user
2. Window Manager: Sliding window logic
3. Decision Engine: Allow or deny request
4. Response Builder: Return appropriate status
```

### writeTestingPlan()
```python
def test_under_limit():
    # 50 requests in 1 min → all succeed

def test_over_limit():
    # 101 requests in 1 min → last one fails

def test_window_sliding():
    # 100 req at t=0, 1 req at t=61 → succeeds

def test_concurrent_requests():
    # Parallel requests don't double-count
```

### writeInstructions()
```python
# Use Redis with sliding window
def check_rate_limit(api_key: str, limit: int, window_sec: int) -> bool:
    now = time.time()
    window_start = now - window_sec

    # Count requests in current window
    count = redis.zcount(f"rate:{api_key}", window_start, now)

    if count >= limit:
        return False

    # Record this request
    redis.zadd(f"rate:{api_key}", {now: now})
    redis.expire(f"rate:{api_key}", window_sec)

    return True
```

---

## Common Patterns Across Examples

### Pattern 1: Input → Process → Output
Most modules follow this flow:
1. **Input Module**: Validate and normalize
2. **Processing Module**: Core logic
3. **Output Module**: Format results

### Pattern 2: Bottom-Up Dependencies
Always build in this order:
1. Modules with no dependencies
2. Modules that depend on #1
3. Integration layer

### Pattern 3: Test-First Thinking
Define test cases during `writeTestingPlan()`, not after implementation.

### Pattern 4: Stop Recursing Wisely
- ✅ Stop when you can code directly from instructions
- ❌ Don't spec individual functions (that's the code itself)
- ✅ Stop at component level for most projects
- ❌ Don't recurse to every tiny detail

---

## Anti-Patterns to Avoid

### ❌ Starting to Code Too Early
```markdown
# BAD
## writeSpec()
### What: Build a search thing

[Starts coding without finishing architecture/tests/instructions]
```

### ❌ Over-Specification
```markdown
# BAD - Too detailed
## writeInstructions()

def function_a(param1: str, param2: int) -> dict:
    # Step 1: Initialize empty dict
    result = {}
    # Step 2: Check if param1 is None
    if param1 is None:
        return result
    # Step 3: Convert param1 to lowercase
    param1_lower = param1.lower()
    ...
[This is just writing code in markdown]
```

### ❌ Top-Down Implementation
```markdown
# BAD
Phase 1: Build UI (depends on everything)
Phase 2: Build business logic (depends on data layer)
Phase 3: Build data layer

[This causes integration hell]
```

### ✅ Right Amount of Detail
```markdown
# GOOD
## writeInstructions()

def parse_query(query: str) -> dict:
    # Extract filter expressions using regex
    # Parse each filter into structured format
    # Handle invalid filters gracefully
    # Return {text: str, filters: dict}

[Enough guidance to implement, not literal code]
```

---

## Scaling 4F

### Small Projects (1-2 hours)
- Project level: Quick 4F pass
- Maybe 1-2 modules
- Components might be implementable directly

### Medium Projects (1-2 days)
- Full project-level 4F
- 3-5 modules, each with 4F
- Some components recurse one level

### Large Projects (weeks/months)
- Detailed project-level 4F
- Many modules (10+)
- Sub-components often get their own 4F
- May recurse 3-4 levels deep

### Key: Stop at the Right Depth
You know you've gone deep enough when:
- ✅ You can estimate implementation time
- ✅ Test cases are obvious
- ✅ You could start coding right now
- ✅ The instructions are clear enough for someone else (or AI) to implement

---

## Using 4F with Different Languages

The method works regardless of language:

### Python
```python
# Clean class-based modules
class InputParser:
    def parse(self, raw_input: str) -> ParsedData:
        ...
```

### JavaScript/TypeScript
```typescript
// Functional modules
export function parseInput(rawInput: string): ParsedData {
    ...
}
```

### Go
```go
// Package-based modules
package parser

func Parse(rawInput string) (*ParsedData, error) {
    ...
}
```

### Rust
```rust
// Module-based with error handling
pub fn parse(raw_input: &str) -> Result<ParsedData, ParseError> {
    ...
}
```

The 4F principles are language-agnostic. What matters is:
- Clear module boundaries
- Defined inputs/outputs
- Testability
- Bottom-up construction

---

## Next Steps

1. **Study the PR Interaction Report Generator** as a reference implementation
2. **Copy the templates** and adapt for your project
3. **Start small** - pick a feature or module to try 4F
4. **Share your results** - what worked, what didn't

Happy building with 4F! 🚀
