# Claude Tech Debt Analyzer - Quick Start

## What Is This?

A Claude Code plugin that uses **Claude's AI** to analyze your codebase and quantify technical debt in business terms.

**Key Point:** This runs IN Claude Code. Claude analyzes your code directly using its understanding - no API keys, no external calls.

## Get Started in 30 Seconds

### Step 1: Add the Marketplace

In Claude Code:
```bash
/plugin marketplace add gthimmes/claude-tech-debt-analyzer
```

### Step 2: Install the Plugin

```bash
/plugin install claude-tech-debt-analyzer
```

### Step 3: Analyze Your Code

Just ask Claude:
```
Analyze my codebase for technical debt
```

### Step 4: Get Results

```
Overall AI Debt Score: 58/100 (MODERATE)
Annual Cost: $1,245,000

Top Priorities:
  1. UserService (87/100 - CRITICAL)
     Issue: 847-line class mixing concerns
     Fix: $45K → Saves $195K/year (1,200% ROI)
```

Plus a detailed markdown report saved to `tech-debt-analysis/tech-debt-report.md`!

## What You Get

### AI-Powered Analysis
- **Claude reads your code** in any programming language
- **Understands context** not just syntax patterns
- **Identifies real issues** like architecture problems, not just "high complexity"

### Business Translation
- **$1.2M/year** in lost productivity (not "code is bad")
- **$45K investment** with 2.8 month payback (not "should refactor")
- **18% slower delivery** with specific causes (not "technical debt")

### Actionable Insights
- **Specific recommendations**: "Split UserService into 3 services"
- **ROI calculations**: "$45K fix saves $195K/year"
- **Priority ranking**: Fix UserService first, then PaymentProcessor

## How It Works

```
You: Analyze my codebase for technical debt

Claude: [Uses Read tool to examine source files]
        [Analyzes code using AI understanding]
        [Calculates business impact]
        [Generates executive report]

Done! Report saved to ~/my-project/tech-debt-analysis/tech-debt-report.md
```

## Example Analysis

### What Claude Sees:
```python
class UserService:  # 847 lines
    def authenticate(self, username, password):
        # 50 lines of nested if/else
        # No error handling
        # Mixes auth + sessions + authorization
```

### What Claude Reports:
- **Score**: 85/100 (CRITICAL)
- **Issues**: God class, no error handling, mixed concerns
- **Impact**: "$285K/year - changes take 3x longer"
- **Fix**: "Split into 3 services - 6 weeks, $45K"
- **ROI**: "Saves $195K/year = 4.3 month payback"

## Why This Is Better

### Traditional Tools
- Count "if" statements → complexity number
- Regex pattern matching
- Generic "reduce complexity" advice
- Limited language support

### Claude Tech Debt Analyzer
- Understand WHAT code does → quality assessment
- AI comprehension of architecture
- Specific "split UserService" recommendations
- Works with ANY language

## Configuration

Customize for your org in `config/cost_config.yaml`:

```yaml
organization:
  engineer_count: 50
  avg_salary: 150000
```

Claude will calculate costs specific to your team.

## Requirements

- Claude Code installed
- That's it! No API keys, no dependencies

## Privacy

- All analysis runs locally in Claude Code
- No code sent to external services
- Claude is already running on your machine

## What Makes This Special

This isn't a static analysis tool with Claude integration.

This is **Claude analyzing your code** using its understanding of software quality, then translating findings into business language.

That's why it:
- Works with any language
- Understands context
- Gives specific advice
- Explains in plain English

## Get Started Now

```bash
/plugin marketplace add gthimmes/claude-tech-debt-analyzer
/plugin install claude-tech-debt-analyzer
```

Then just ask: "Analyze my codebase for technical debt"

**Transform "the code is terrible" into "$1.2M/year in lost productivity"**

---

Questions? Check [README.md](README.md) for full documentation.
