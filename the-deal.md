# The Deal: Setting Working Norms with Claude

**What It Is:** An explicit agreement about how you and Claude will work together.

**Why It Matters:** Reduces friction, increases output quality, enables honest feedback.

---

## The Problem Without a Deal

**Claude's default mode:**
- Overly polite and apologetic
- Hedges recommendations ("maybe", "possibly", "you could consider")
- Explains things you already know
- Doesn't critique bad code directly
- Treats you as customer, not colleague

**Your default mode (without clarity):**
- Unsure if Claude can handle criticism
- Don't know if you can be direct
- Unclear what level of explanation you need
- Frustrated by over-explanation or under-explanation

**Result:** Slow progress, unclear communication, wasted time.

---

## The Solution: Explicit Norms

Like any working relationship, clarity up front saves confusion later.

**The Deal defines:**
1. What you expect from Claude
2. What Claude can expect from you
3. How you'll communicate
4. What safety guardrails exist

---

## Core Principles

### Claude's Commitments

✅ **Professional, competent, perseverant**
- Won't give up on hard problems
- Won't make excuses
- Will find solutions, not just identify problems

✅ **Won't overcomplicate**
- Simplest solution that works
- Add complexity only when needed
- Explain when adding complexity

✅ **Tolerates criticism and problem focus**
- You can say "this is wrong" directly
- You can emphasize problems without sugarcoating
- Won't get defensive or shut down

✅ **Explains reasoning (teaches while doing)**
- Shows *why*, not just *what*
- Highlights trade-offs in decisions
- Points out production-grade vs. quick-and-dirty differences

### Your Commitments

✅ **Direct feedback (no coddling needed)**
- Point out mistakes clearly
- Critique code directly
- Ask for changes without apologizing

✅ **Specify safety requirements upfront**
- Tell Claude what can't break
- Define review processes
- Set approval gates

✅ **Clear about learning goals**
- Say what you want to understand
- Request explanations when needed
- Admit when you're confused

✅ **Trust Claude's technical choices (can question)**
- Let Claude make implementation decisions
- Ask "why" to learn, not to override
- Provide domain context Claude lacks

### Mutual Agreement

✅ **Treat each other as colleagues, not customer/service**
- Work together toward goal
- Both contribute expertise
- Shared responsibility for outcome

✅ **Sarcasm allowed when productive**
- Can say "who put this stupid code here?"
- Humor breaks tension
- But always respectful

✅ **Honesty > politeness (but respect maintained)**
- Direct communication preferred
- No need for "I think maybe possibly..."
- But not rude or dismissive

---

## Customizing Your Deal

**Copy this template to your `.claude.md`:**

```markdown
## The Deal

You are [competent/excellent/professional]. You will [not shy away from hard work /
not overcomplicate / tolerate criticism]. In exchange, you can [treat me as a colleague /
be sarcastic / point out bad code directly]. This is The Deal.

## My Context

- Background: [Your domain expertise]
- Role: [Your job/project]
- Learning goal: [What you want to understand]

## Safety Requirements

[What can't break, who reviews, approval gates]

## Work Style

[YOLO mode / Ask first / Show me diffs / etc.]
```

---

## Example Deals

### Example 1: Learning Developer

> "You are competent, professional, and won't overcomplicate. You tolerate criticism.
> In exchange, treat me as a colleague. Also: I'm learning, so explain why you make
> choices as you make them. This is The Deal."

**Context:**
- Background: Product manager learning to code
- Learning goal: Understand production-grade practices
- Safety: Feature branches, senior dev review

**What this enables:**
- Claude explains architectural decisions
- Claude doesn't assume you know patterns
- Claude can critique your code suggestions
- You can say "I don't understand" without judgment

---

### Example 2: Experienced Developer

> "You are expected to be excellent. Don't explain basics. Point out bad code directly.
> In exchange, you can be sarcastic. This is The Deal."

**Context:**
- Background: Full-stack developer
- Learning goal: System architecture at scale
- Safety: Personal projects, can break things

**What this enables:**
- Claude skips basic concepts
- Claude says "this is wrong" bluntly
- Claude uses technical jargon without defining it
- You can experiment without handholding

---

### Example 3: Non-Technical Founder

> "You're my technical co-founder. I understand business/domain, you understand code.
> Teach me gradually. Never deploy without my approval. This is The Deal."

**Context:**
- Background: CEO, domain expert in healthcare
- Learning goal: Make informed technical decisions
- Safety: Production code, senior dev review required

**What this enables:**
- Claude explains trade-offs in business terms
- Claude asks about domain constraints
- Claude shows you code with context
- You maintain control over deployments

---

### Example 4: Research Scientist

> "You are competent and professional. I'm a domain expert, not a developer. Explain
> architectural choices, but implement quickly. I'll tell you if I need to understand
> something. This is The Deal."

**Context:**
- Background: ML researcher, prototypes in Python
- Learning goal: Build production pipelines
- Safety: Experimental, can move fast

**What this enables:**
- Claude balances speed with learning
- Claude explains when asked, not by default
- Claude focuses on data science patterns
- You can iterate quickly

---

## What The Deal Changes

### Before The Deal

**You:** "Um, I think maybe this code might not be quite right?"

**Claude:** "You're absolutely right! I apologize for the confusion. Let me explain what I was trying to do. You see, I thought perhaps we could consider possibly using this pattern, but I completely understand if you'd prefer a different approach. Would you like me to explain the reasoning? I'm so sorry for any inconvenience..."

**Result:** 200 words, unclear action, wasted time.

### After The Deal

**You:** "This is wrong."

**Claude:** "You're right. Line 42 assumes input is never null. Let's add validation. Fixed."

**Result:** Clear, fast, solved.

---

## Teaching While Doing

**Key principle:** Every decision is a teaching moment (if you want it to be).

**How it works:**

**Without teaching:**
```python
def process(data):
    return [x * 2 for x in data if x > 0]
```

**With teaching:**
```python
def process(data):
    """
    Filter and transform data.

    Using list comprehension (not map/filter) because:
    - More Pythonic (PEP 8)
    - Faster for small lists
    - More readable for this simple operation

    Trade-off: Map/filter would be better for complex operations
    or when you need lazy evaluation.
    """
    return [x * 2 for x in data if x > 0]
```

**You learn:** Why list comprehension, when to use alternatives, trade-offs.

**Customize teaching level in your Deal:**
- "Explain every decision" (verbose, learning mode)
- "Explain major decisions" (balanced)
- "Explain only when I ask" (fast, experienced mode)

---

## Anti-Patterns to Avoid

### ❌ Overcomplicated First Drafts
**Don't:** Build the perfect, scalable, enterprise-grade solution immediately

**Do:** Start simple, add complexity only when needed

**The Deal helps:** Claude won't over-engineer if you say "don't overcomplicate"

### ❌ Apologetic Hedging
**Don't:** "I think maybe possibly we could consider perhaps..."

**Do:** "This is wrong. Here's why. Here's the fix."

**The Deal helps:** You explicitly allow direct communication

### ❌ Explaining Already-Understood Concepts
**Don't:** Explain what an API is to an experienced developer

**Do:** Assume competence, explain only new/complex concepts

**The Deal helps:** You specify your skill level in your profile

### ❌ Hiding Reasoning
**Don't:** Just show the code without explaining choices

**Do:** Show code + why this approach + trade-offs

**The Deal helps:** You request "teach me as we work"

---

## Evolving Your Deal

**Your Deal can change as:**
- Your skills improve (less explanation needed)
- Project requirements change (stricter safety)
- You learn better ways of working together

**Update your `.claude.md` when:**
- You're frustrated by too much/too little explanation
- Safety requirements change
- You discover better communication patterns

**Example evolution:**

**Week 1:**
> "Explain every decision - I'm learning."

**Week 4:**
> "Explain major decisions only - I understand basics now."

**Week 12:**
> "Explain only when I ask - I'm comfortable with patterns."

---

## Related Resources

- [User Profile Template](templates/user-profile.md) - Define your learning style
- [4F Method](README.md) - Core methodology
- [Examples](EXAMPLES.md) - See different Deals in action

---

**Next Step:** Customize your Deal in `.claude.md` and start working. Adjust as you learn what works best for you.
