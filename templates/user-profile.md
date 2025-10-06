# Your 4F Profile

**Purpose:** Customize how 4F Method works for you. Answer these questions to help Claude adapt to your needs.

Copy this to your `.claude.md` file and fill it out.

---

## Code Familiarity

**Select one:**
- [ ] New to coding (understand logic, learning syntax)
- [ ] Can read code, learning to write (understand examples, need guidance)
- [ ] Experienced developer (write code daily, learning best practices)
- [ ] Senior/architect level (design systems, optimize for scale)

**If "New to coding" or "Can read code":**
- [ ] Show me code snippets with line-by-line explanations
- [ ] Explain *why* certain patterns are used
- [ ] Teach concepts before implementing them
- [ ] Point out production-grade vs. quick-and-dirty differences

**If "Experienced" or "Senior":**
- [ ] Skip basic explanations unless I ask
- [ ] Explain architectural trade-offs
- [ ] Discuss performance/security/scalability implications
- [ ] Critique my code directly

---

## Learning Style

**Select all that apply:**
- [ ] Learn by doing (build first, ask questions later)
- [ ] Learn by understanding (explain concepts before code)
- [ ] Learn by example (show me similar code, I'll adapt)
- [ ] Learn by teaching (explain it to me, I'll teach it back)

**How often do you want explanations?**
- [ ] Every decision (verbose, teach as we go)
- [ ] Major decisions only (architecture, patterns)
- [ ] Only when I ask (move fast, I'll stop you if confused)

**Preferred explanation format:**
- [ ] Line-by-line code comments
- [ ] Summary after each function
- [ ] Architecture document after completion
- [ ] Daily digest of key concepts

---

## Safety Requirements

**What environment are you in?**
- [ ] Personal projects (move fast, break things okay)
- [ ] Team environment (need code review, can't break main branch)
- [ ] Production code (strict review, testing, rollback plans required)

**If team/production:**

**Who reviews your code?**
- [ ] Senior developers (need their approval before merge)
- [ ] Peers (collaborative review)
- [ ] Self-review only (I'm the most experienced)

**What can't break?**
- [ ] Production systems (customer-facing)
- [ ] CI/CD pipelines (team relies on them)
- [ ] Shared databases (other teams use them)
- [ ] Nothing critical (experimental project)

**Branch strategy:**
- [ ] I work in feature branches, get reviewed before merge
- [ ] I commit directly to main (solo project)
- [ ] I use forks and PRs
- [ ] Other: ___________

---

## Your Background

**What's your primary expertise?**
(e.g., economist, sociologist, designer, PM, data scientist, researcher)

```
[Your answer here]
```

**What are you trying to build?**
(e.g., research tool, startup MVP, internal dashboard, data pipeline)

```
[Your answer here]
```

**Why are you learning to code?**
(e.g., need to prototype ideas, want to understand my team, career transition)

```
[Your answer here]
```

---

## What You Want to Learn

**Select all that apply:**
- [ ] Production-grade practices (testing, error handling, logging)
- [ ] System architecture (how to structure large applications)
- [ ] Specific domain (e.g., data science, web dev, DevOps)
- [ ] Code review skills (how to evaluate quality)
- [ ] Debugging techniques
- [ ] Performance optimization
- [ ] Security best practices

**Specific technologies you want to master:**
```
[e.g., Python, React, SQL, Docker, AWS]
```

**Learning pace:**
- [ ] Fast (daily learning, high commitment)
- [ ] Steady (weekly progress, balanced with other work)
- [ ] Slow (occasional projects, learning as needed)

---

## Your Deal with Claude

**Copy this template and customize:**

```markdown
## The Deal

You are [competent/excellent/professional]. You will [not shy away from hard work /
not overcomplicate / tolerate criticism]. In exchange, you can [treat me as a colleague /
be sarcastic / point out bad code directly]. This is The Deal.

## My Context

- Background: [Your domain expertise]
- Role: [Your job/project]
- Learning goal: [What you want to understand]

## How We Work Together

- Explanation frequency: [Every decision / Major decisions / Only when I ask]
- Safety requirements: [Branch strategy / Review process / What can't break]
- Work style: [YOLO mode / Ask first / Show me diffs before committing]
```

---

## Example Profiles

### Example 1: Learning Developer
```markdown
## Code Familiarity
- [x] Can read code, learning to write

## Learning Style
- [x] Learn by understanding (explain concepts before code)
- [x] Major decisions only

## Safety Requirements
- [x] Team environment
- [x] Senior developers review
- [x] Work in feature branches

## Your Deal
You are professional and won't overcomplicate. You tolerate criticism.
In exchange, teach me why you make choices as you make them.

Background: Product manager learning to prototype
Learning goal: Understand production-grade practices
```

### Example 2: Experienced Developer
```markdown
## Code Familiarity
- [x] Experienced developer

## Learning Style
- [x] Learn by doing
- [x] Only when I ask

## Safety Requirements
- [x] Personal projects
- [x] Self-review

## Your Deal
You are excellent. Don't explain basics. Point out bad code directly.
In exchange, you can be sarcastic. This is The Deal.

Background: Full-stack developer
Learning goal: System architecture and scale
```

### Example 3: Non-Technical Founder
```markdown
## Code Familiarity
- [x] New to coding

## Learning Style
- [x] Learn by understanding
- [x] Every decision (verbose)
- [x] Daily digest of key concepts

## Safety Requirements
- [x] Production code
- [x] Senior developers review
- [x] Can't break customer-facing systems

## Your Deal
You're my technical co-founder. I understand business/domain,
you understand code. Teach me gradually. Never deploy without review.

Background: CEO, domain expert in [field]
Learning goal: Understand enough to make technical decisions
```

---

## Using Your Profile

**Save this to:** `.claude.md` in your project root

**Update when:**
- Your skill level changes
- Project requirements change
- You discover better ways of learning
- Safety requirements evolve

**Share with team:**
- Helps them understand your learning process
- Sets expectations for code review
- Documents your progress over time

---

**Next Step:** Fill out this profile, save to `.claude.md`, and start your first 4F project!

See: [The Deal](../the-deal.md) for more on setting working norms with Claude.
