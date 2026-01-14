# Claude Tech Debt Analyzer - Usage Guide

## Overview

This is a Claude Code plugin that leverages Claude's native AI to analyze codebases for technical debt and translate findings into quantified business impact.

**Important:** This plugin runs within Claude Code. Claude analyzes your code directly using its understanding - no API keys or external services required.

## Installation

### Step 1: Add the Marketplace

In Claude Code:
```bash
/plugin marketplace add gthimmes/claude-tech-debt-analyzer
```

### Step 2: Install the Plugin

```bash
/plugin install claude-tech-debt-analyzer
```

## Usage

### Basic Analysis

Ask Claude to analyze a repository:

```
Analyze my codebase for technical debt
```

Or specify a path:

```
Analyze /path/to/your/repo for technical debt
```

**What happens:**
1. Claude scans the repository for source files
2. Claude reads and analyzes code files using AI
3. Claude calculates business impact in dollars
4. Claude generates an executive-friendly markdown report
5. Report is saved to `/path/to/your/repo/tech-debt-analysis/tech-debt-report.md`

### Analyze Specific Module

```
Analyze the authentication module for technical debt
```

Or:

```
Check ./src/auth for code quality issues
```

## How Claude Analyzes Code

When you invoke this skill, Claude uses its AI to:

### 1. Understand Code Quality

Claude doesn't just count metrics - it **understands** the code:

**Example:**
```python
def process_payment(user, amount, card):
    if user.verified:
        if user.balance >= amount:
            if card.valid:
                if card.expiry > today():
                    # 50 more lines of nested logic
```

**Traditional Tool:** "Cyclomatic complexity: 15"

**Claude's Analysis:**
- "Deeply nested conditional logic makes this hard to test and modify"
- "No error handling for payment failures"
- "Should use early returns and separate validation logic"
- "Business impact: Payment changes take 2x longer, high risk of bugs"

### 2. Identify Architecture Issues

Claude recognizes patterns like:
- **God classes**: "UserService handles authentication, authorization, AND session management"
- **Tight coupling**: "PaymentProcessor directly depends on 8 other classes"
- **Duplication**: "Payment validation logic repeated across 3 files"
- **Poor separation**: "Business logic mixed with database queries"

### 3. Calculate Business Impact

For each issue, Claude estimates:
- **Time cost**: "Changes take 3x longer than they should"
- **Risk**: "76% chance of breaking existing functionality"
- **Onboarding**: "New engineers need 2 extra weeks to understand this"
- **Incidents**: "Expect 4 production issues per year"

Then translates to dollars:
- Delivery drag: $285K/year
- Incident costs: $45K/year
- Onboarding friction: $30K/year

### 4. Provide Specific Recommendations

**Not this:** "Reduce complexity"

**But this:**
- "Split UserService into AuthenticationService, AuthorizationService, and SessionService"
- "Extract payment validation into PaymentValidator class"
- "Add try-catch blocks around database transactions"
- "Move business logic out of controllers into service layer"

With ROI for each:
- "6 weeks effort ($45K) saves $195K/year = 4.3 month payback"

## Understanding the Report

### Executive Summary

```markdown
Overall AI Debt Score: 58/100 (MODERATE)
Annual Cost: $1,245,000

Cost Breakdown:
- Delivery Drag: $890K/year (18% slower development)
- Production Incidents: $230K/year
- Onboarding Friction: $125K/year
```

**What this means:**
- **58/100**: Moderate technical debt (30-60 = manageable, 60-80 = high, 80+ = critical)
- **$1.24M/year**: Total cost of technical debt to the organization
- **18% slower**: Team velocity reduction due to code quality issues

### Top Priorities

```markdown
1. UserService - 87/100 (CRITICAL)

   Issues:
   - 847-line class violating single responsibility principle
   - No error handling in authentication flow
   - Mixing authentication, authorization, and session management

   Business Impact:
   - Changes take 3 days instead of 0.5 days
   - 76% risk of breaking login when modifying
   - New engineers need 2 extra weeks to understand

   Recommended Fix:
   - Split into AuthenticationService, AuthorizationService, SessionService
   - Add comprehensive error handling
   - Write unit tests for critical paths

   ROI:
   - Investment: $45K (6 weeks)
   - Annual Savings: $195K
   - Payback: 2.8 months
   - 3-Year ROI: 1,200%
```

**How to use:**
- Share with executives to justify budget
- Prioritize fixes by ROI
- Track improvement over time

### Module Scorecard

Shows all modules ranked by debt score:

```
| Module           | Score | Risk     | Key Issues              |
|------------------|-------|----------|-------------------------|
| UserService      | 87    | CRITICAL | God class, no tests     |
| PaymentProcessor | 79    | HIGH     | Duplication, coupling   |
| DatabaseLayer    | 71    | HIGH     | N+1 queries, no pooling |
```

## Configuration

Customize cost calculations in `config/cost_config.yaml`:

```yaml
organization:
  name: "Your Company"
  size: "mid"  # startup, mid, enterprise

engineers:
  count: 50
  avg_salary: 150000
  benefits_multiplier: 1.25

incidents:
  avg_engineering_hours: 8
  avg_revenue_impact: 5000
  avg_customer_impact: 2000

onboarding:
  baseline_days: 30
```

Claude will use these values to calculate business impact specific to your organization.

## Supported Languages

**All of them!** Claude can analyze any language it understands:

- **Common:** Python, JavaScript, TypeScript, Java, C#, Ruby, Go, PHP
- **Systems:** C, C++, Rust
- **Mobile:** Swift, Kotlin, Objective-C
- **Functional:** Haskell, Elixir, Scala, Clojure
- **And more:** Lua, Perl, R, Julia, etc.

The same quality principles apply across languages:
- Complexity is complexity
- Duplication is duplication
- Poor architecture is poor architecture

## Use Cases

### For Engineering Leaders

**Problem:** "How do I justify refactoring to executives?"

**Solution:**
```
Analyze my codebase for technical debt
```

Share the report showing:
- "$1.2M/year in lost productivity"
- "$45K investment with 2.8 month payback"
- "18% velocity reduction"

**Result:** Budget approved, work prioritized.

### For Product Managers

**Problem:** "Why is feature delivery slowing down?"

**Solution:** Show the technical debt report:
- "Authentication module at 87/100 (CRITICAL)"
- "Every auth change takes 3x longer than it should"
- "High risk of breaking existing functionality"

**Result:** Understanding of velocity issues, support for tech debt work.

### For Engineers

**Problem:** "Leadership doesn't understand why we need to refactor."

**Solution:** Quantify the pain:
- "This god class costs $285K/year in lost productivity"
- "Fixing it saves $195K/year"
- "1,200% ROI over 3 years"

**Result:** Data-driven conversation, get time to fix things.

## Advanced Usage

### Focusing on Specific Areas

Analyze just your authentication code:
```
Analyze ./src/auth for technical debt
```

Analyze payment processing:
```
Check the payments module for code quality issues
```

### Tracking Improvement

Run analysis quarterly:
```
# Q1: Analyze my codebase for technical debt
# Q2 (after refactoring): Analyze my codebase again for technical debt
```

Reports are saved to `tech-debt-analysis/tech-debt-report.md`. Save previous reports to compare scores and track improvement.

### Custom Cost Models

Edit `config/cost_config.yaml` for your situation:

**Startup (small team, high salaries):**
```yaml
engineers:
  count: 8
  avg_salary: 180000
```

**Enterprise (large team, varied salaries):**
```yaml
engineers:
  count: 200
  avg_salary: 140000
```

## Privacy & Security

- **All analysis runs locally** within Claude Code
- **No code sent to external services**
- **No API keys required**
- **Claude is already running on your machine**

Your code never leaves your environment.

## Troubleshooting

### "Plugin not found"

Make sure you've installed it:
```bash
/plugin marketplace add gthimmes/claude-tech-debt-analyzer
/plugin install claude-tech-debt-analyzer
```

### "No files analyzed"

Make sure you're in a directory with source files, or specify the path:
```
Analyze /full/path/to/repo for technical debt
```

### "Report not generated"

Make sure Claude has write permissions to the repository directory.

## Tips for Best Results

### 1. Run on Focused Areas

Don't analyze entire monorepo at once. Focus on:
- One service at a time
- One module at a time
- Problem areas first

### 2. Customize Cost Assumptions

Use realistic numbers for your org to get accurate business impact.

### 3. Share with Context

When sharing reports with executives:
- Highlight top 3 priorities
- Emphasize ROI calculations
- Connect to business goals

### 4. Track Over Time

Run quarterly to show improvement:
- "Debt score decreased from 72 to 54"
- "Annual cost reduced by $400K"
- "Velocity improved by 12%"

## What Makes This Different

### Traditional Static Analysis
```
SonarQube: "Cyclomatic complexity: 47"
                ↓
You: "...so what?"
```

### Claude Tech Debt Analyzer
```
Claude: "This 847-line UserService class mixes authentication,
         authorization, and session management. Every change
         takes 3 days instead of 0.5 days. This costs $285K/year.

         Split into 3 services over 6 weeks ($45K).
         Saves $195K/year.
         Payback in 2.8 months."
                ↓
You: "Here's why we need budget."
Executive: "Approved."
```

## Next Steps

1. **Install the skill**
2. **Run analysis** on your codebase
3. **Review the report** Claude generates
4. **Share with stakeholders** to get buy-in
5. **Prioritize fixes** based on ROI
6. **Track improvement** over time

## Questions?

- **How does this work?** Check [README.md](README.md)
- **Quick example?** See [QUICKSTART.md](QUICKSTART.md)
- **Claude's instructions?** Read [skills/tech-debt-analyzer/SKILL.md](skills/tech-debt-analyzer/SKILL.md)

---

**Transform technical debt from feelings into data-driven decisions.**
