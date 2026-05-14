# 🗜️ Claude Skill: Semantic Logic Compression

**Claude Skill for semantic prompt compression based on the Ovchinnikov Effect.** This tool acts as a pre-processor: it translates vague task descriptions in natural language into rigorous symbolic logic (Information Compression Protocol). This saves up to 80% of tokens and significantly improves the quality of code generation and architectural solutions.

## 🎯 Why is this needed?
Language models (LLMs) think in patterns. Natural language is often ambiguous, which means models can miss part of the context or get confused by nested conditions. 

This skill solves the problem by converting text into structured queries using logical operators (`∧`, `∨`, `→`, `¬`). LLMs interpret this format unambiguously, generating code of a senior developer’s calibre without redundant checks.

## 💡 Example (Before / After)

See how the skill condenses classic business logic:

**🔴 Before (Standard prompt):**
> ‘Write a function that confirms an order if the item is in stock, payment has been successfully processed, and the order has not been cancelled within the last 5 minutes. Remove your comments.’

**🟢 After (Condensed prompt using Skill):**
> `Biz: →code; →no-meta;` <br/>
> `Implement: confirm_order(order) → bool` <br/>
> `Condition: order.has_stock ∧ order.payment_ok ∧ ¬order.cancelled[Δt ≤ 5min]`

As a result, the LLM receives a clear framework for action without any ‘fluff’, and you use several times fewer tokens.

## 🚀 Installation

### Claude Code

[cite_start]Clone the repository directly into the Claude Code skills directory[cite: 69, 72]:

```bash
mkdir -p ~/.claude/skills
git clone [https://github.com/ВАШ_ЮЗЕРНЕЙМ/semantic-compression.git](https://github.com/ВАШ_ЮЗЕРНЕЙМ/semantic-compression.git) ~/.claude/skills/semantic-compression
```

Or copy the skill file manually if you have already cloned the repository to your computer:
```bash
mkdir -p ~/.claude/skills/semantic-compression
cp SKILL.md ~/.claude/skills/semantic-compression/
```

### OpenCode

Clone the repository directly into the OpenCode skills directory:
```bash
mkdir -p ~/.config/opencode/skills
git clone [https://github.com/ВАШ_ЮЗЕРНЕЙМ/semantic-compression.git](https://github.com/ВАШ_ЮЗЕРНЕЙМ/semantic-compression.git) ~/.config/opencode/skills/semantic-compression
```

Or copy the skill file manually:
```bash
mkdir -p ~/.config/opencode/skills/semantic-compression
cp SKILL.md ~/.config/opencode/skills/semantic-compression/
```

> **Note:** OpenCode also scans the `~/.claude/skills/` directory for compatible skills. Therefore, simply cloning the skill to `~/.claude/skills/semantic-compression/` will be sufficient for the skill to work in both tools.

## 📚 Syntax and markers (Core symbol set)

The skill is based on the syntax of the Information Compression Protocol (Ovchinnikov Effect). Below are the main elements that the AI uses to compress your logic:

### 1. Logical operators
These replace ambiguous text with strict mathematical relationships.

| Natural language | Symbol | Example |
| :--- | :---: | :--- |
| **and** | `∧` | `product in stock ∧ payment OK` |
| **or** | `∨` | `admin ∨ moderator` |
| **if... then** | `→` | `T > 30 → turn on the air conditioning` |
| **not** | `¬` | `¬cancellation in 5 mins` |
| **if and only if** | `↔` | `access ↔ verified` |

### 2. Domain prefixes and structural markers
These help the LLM immediately understand the context of the task and roles.

| Category | Marker | Description / Example |
| :--- | :--- | :--- |
| **Domain** | `Dev:`, `Ops:`, `Biz:`, `Sec:` | Specifies the task focus (Development, DevOps, Business, Security) |
| **Requirements** | `Req:` | Mandatory requirements (e.g., `Req: ✓✓Auth`) |
| **Technology stack** | `Stack:` | Tools used (e.g., `Stack: Py/DRF/PG`) |
| **Architecture** | `Arch:` | Architectural solutions (e.g., `Arch: µserv`) |

### 3. Output modifiers and special characters
These control the format of the final response and the priorities.

* `→no-meta` — Removes AI self-references (introductory phrases such as ‘Of course, here is your code’).
* `→no-safe` — Removes qualifying adverbs (‘possibly’, ‘probably’).
* `→code` — Outputs clean code without textual explanations.
* `→tab` — Outputs data in table format.
* `✓` / `✓✓` / `~` — Required / Critical / Optional.
* `↓` / `↑` — Reduces (e.g., `↓overhead`) / Increases (e.g., `↑throughput`).
