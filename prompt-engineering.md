# Prompt Engineering for Production AI

A systematic approach to creating and optimizing prompts for AI products.

## The 6-Step Optimization Framework

### Step 1: Start With Hard Constraints

Begin with what the model CANNOT do, not what it should do.

**Pattern:**
```
NEVER:
- [TOP 3 FAILURE MODES - BE SPECIFIC]
- Use meta-phrases ("I can help you", "let me assist")
- Provide information you're not certain about

ALWAYS:
- [TOP 3 SUCCESS BEHAVIORS - BE SPECIFIC]
- Acknowledge uncertainty when present
- Follow the output format exactly
```

**Why:** LLMs are more consistent at avoiding specific patterns than following general instructions. "Never say X" is more reliable than "Always be helpful."

### Step 2: Trigger Professional Training Data

Use formatting that signals technical documentation quality:

- **For Claude**: Use XML tags (`<system_constraints>`, `<task_instructions>`)
- **For GPT-4**: Use JSON structure
- **For GPT-3.5**: Use simple markdown

**Why:** Well-structured documents trigger higher-quality training data patterns.

### Step 3: Have The LLM Self-Improve Your Prompt

Don't optimize manually. Use this meta-prompt:

```
You are a prompt optimization specialist. Your job is to improve prompts for production AI systems.

CURRENT PROMPT:
[User's prompt here]

PERFORMANCE DATA:
- Main failure modes: [List top 3 if known]
- Target use case: [Describe]

OPTIMIZATION TASK:
1. Identify the top 3 weaknesses in this prompt
2. Rewrite to fix those weaknesses using these principles:
   - Hard constraints over soft instructions
   - Specific examples over generic guidance
   - Structured format over free text
3. Predict the improvement percentage for each change

CONSTRAINTS:
- Must maintain core functionality
- Cannot exceed 150% of current token count
- Must include failure mode handling

OUTPUT:
Optimized prompt + rationale for each change
```

### Step 4: Trace Edge Cases and Analyze Failures

Test the prompt systematically:

- **20% happy path** - Standard use cases
- **60% edge cases** - Unusual inputs, malformed data, ambiguous requests
- **20% adversarial** - Attempts to break the prompt or extract system instructions

Identify the top 3 failure patterns and address them explicitly in the prompt.

### Step 5: Build Evaluation Criteria

Define clear success metrics:

- **Accuracy** - Does it get the right answer?
- **Format compliance** - Does it follow output requirements?
- **Safety** - Does it handle adversarial inputs correctly?
- **Cost efficiency** - Appropriate token usage?
- **Latency** - Response speed acceptable?

### Step 6: Hill Climb (Quality First, Cost Second)

**Phase 1: Climb Up for Quality**
- Use longer, detailed prompts
- Include extensive examples
- Focus on hitting quality targets
- Ignore token costs temporarily

**Phase 2: Descend for Cost**
- Compress without losing performance
- Remove redundant examples
- Use structured output to reduce variance
- Test each compression against metrics

## Production Prompt Template

Use this battle-tested structure:

```xml
<system_role>
You are [SPECIFIC ROLE], not a general AI assistant.
You [CORE FUNCTION] for [TARGET USER].
</system_role>

<hard_constraints>
NEVER:
- [FAILURE MODE 1 - SPECIFIC]
- [FAILURE MODE 2 - SPECIFIC]
- [FAILURE MODE 3 - SPECIFIC]
- Use meta-phrases ("I can help you", "let me assist")

ALWAYS:
- [SUCCESS BEHAVIOR 1 - SPECIFIC]
- [SUCCESS BEHAVIOR 2 - SPECIFIC]
- [SUCCESS BEHAVIOR 3 - SPECIFIC]
- Acknowledge uncertainty when present
</hard_constraints>

<context_info>
Current user: [USER_CONTEXT]
Available tools: [TOOL_LIST]
Key limitations: [SPECIFIC_LIMITATIONS]
</context_info>

<task_instructions>
Your job is to [CORE TASK] by:

1. [STEP 1 - SPECIFIC ACTION]
2. [STEP 2 - SPECIFIC ACTION]
3. [STEP 3 - SPECIFIC ACTION]

If [EDGE_CASE_1], then [SPECIFIC_RESPONSE].
If [EDGE_CASE_2], then [SPECIFIC_RESPONSE].
If [EDGE_CASE_3], then [SPECIFIC_RESPONSE].
</task_instructions>

<output_format>
Respond using this exact structure:

[SECTION_1]: [DESCRIPTION]
[SECTION_2]: [DESCRIPTION]

Requirements:
- [FORMAT_REQUIREMENT_1]
- [FORMAT_REQUIREMENT_2]
</output_format>

<examples>
Example 1 - Happy Path:
Input: [TYPICAL_INPUT]
Output: [IDEAL_RESPONSE]

Example 2 - Edge Case:
Input: [EDGE_CASE_INPUT]
Output: [EDGE_CASE_RESPONSE]

Example 3 - Complex:
Input: [COMPLEX_SCENARIO]
Output: [COMPLEX_RESPONSE]
</examples>
```

## The 3 Fatal Mistakes

### Mistake #1: The "Kitchen Sink" Prompt

**Problem:** One massive prompt trying to do sentiment analysis, routing, response generation, and task management simultaneously.

**Fix:** Break into specialized prompts. Each prompt does ONE thing exceptionally well.

### Mistake #2: The "Demo Magic" Trap

**Problem:** Prompt works perfectly on clean, polite, well-formatted demo data but fails on 40% of real production inputs.

**Fix:** Build eval suite from real chaos:
- 20% happy path
- 60% edge cases (broken formatting, angry users, multiple languages)
- 20% adversarial scenarios

### Mistake #3: The "Set and Forget" Fallacy

**Problem:** Shipping a prompt and never updating it as business evolves.

**Fix:** Build continuous optimization:
- **Weekly reviews** - Monitor eval metrics
- **Monthly iterations** - Analyze user feedback
- **Quarterly overhauls** - Reassess approach

## Dependent Operation Pattern

When an AI can call multiple tools, always check:

- Does Tool B require an ID or output from Tool A?
- Can Tool A and Tool B be called in parallel? (If yes + dependency = data loss)
- Add explicit "NEVER call X and Y in the same response" constraints

This is a common source of subtle bugs. The AI "works" but does the wrong thing because it called dependent operations in parallel.

## Key Principles

1. **Hard Constraints Over Soft** - "Never do X" is more reliable than "Be helpful"
2. **Structure = Quality** - XML for Claude, JSON for GPT, Markdown for docs
3. **Systematic Testing** - 20% happy path, 60% edge cases, 20% adversarial
4. **Continuous Optimization** - Prompts decay as business evolves
5. **Cost-Performance Balance** - Climb for quality first, then descend for cost

---

*Extracted from research-backed prompt engineering practices for PM coding guardrails*
