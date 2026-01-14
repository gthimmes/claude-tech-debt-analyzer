# Claude Tech Debt Analyzer

A Claude Code skill that uses Claude's AI to analyze codebases for technical debt and translate findings into quantified business impact.

**Transform "the code is terrible" into "$1.2M/year in lost productivity"** - language executives understand.

## 🎯 What This Is

This is a **Claude Code skill** - it runs inside Claude Code and uses **Claude's native understanding of code** to analyze technical debt across any programming language.

- ✅ **No API keys required** - Claude (running the skill) does the analysis
- ✅ **No external services** - Everything runs within Claude Code
- ✅ **Any programming language** - Claude understands them all
- ✅ **True AI analysis** - Not regex patterns, but actual code comprehension

## 🚀 Installation

### Install via URL in Claude Code (Recommended)

```bash
/install https://github.com/yourusername/claude-tech-debt-analyzer
```

Once installed, use it directly in Claude Code:
```bash
/claude-tech-debt-analyzer analyze /path/to/your/repo
```

### Manual Installation

1. Clone this repository
2. Copy to your Claude Code skills directory:
   ```bash
   cp -r claude-tech-debt-analyzer ~/.claude/skills/
   ```
3. Use in Claude Code:
   ```bash
   /claude-tech-debt-analyzer analyze .
   ```

## ⚡ Quick Start

**In Claude Code:**

```
User: /claude-tech-debt-analyzer analyze /path/to/my/project

Claude: [Analyzes your codebase using AI]
        [Generates comprehensive report]

Overall AI Debt Score: 58/100 (MODERATE)
Annual Cost: $1,245,000

Top Priorities:
  1. UserService (Score: 87/100 - CRITICAL)
     Issue: 847-line class mixing authentication and session management
     Fix: $45K investment → $195K/year savings
     ROI: 1,200% over 3 years
```

## 🎯 What This Does

When you invoke this skill, Claude will:

1. **Scan the repository** for source files in any programming language
2. **Analyze each file** using AI to understand:
   - Code complexity and cognitive load
   - Quality issues (duplication, code smells, architecture problems)
   - Maintainability and modifiability risks
3. **Calculate business impact** in dollars:
   - Delivery drag (how much slower the team is)
   - Incident costs (expected production issues)
   - Onboarding friction (extra time for new engineers)
4. **Generate an executive-friendly report** with:
   - Overall debt score (0-100 scale)
   - Top priority improvements with ROI
   - Specific, actionable recommendations
   - Plain English explanations

## 📊 Example Analysis

### Input: UserService.py
```python
class UserService:  # 847 lines
    def authenticate(self, username, password):
        # 50 lines of complex conditional logic
        # No error handling
        # Mixes authentication, authorization, and session management
```

### Claude's AI Analysis:
- **Complexity Score**: 85/100 - Very high due to mixed responsibilities
- **Quality Score**: 75/100 - No error handling, god class pattern
- **Issues Identified**:
  - "847-line class violates single responsibility principle"
  - "No error handling in authentication flow"
  - "Mixing authentication, authorization, AND session management"
- **Business Impact**: "Changes take 3x longer, 76% risk of breaking login"
- **Recommendations**:
  - "Split into AuthenticationService, AuthorizationService, SessionService"
  - "Add comprehensive error handling"
  - "Write unit tests for critical paths"
- **ROI**: $45K fix → $195K/year savings = 4.3 month payback

## 💡 How It Works

Unlike traditional static analysis tools that use regex patterns, this skill leverages **Claude's understanding of code**:

```
Traditional Tool: Counts "if" statements → complexity score
Claude Skill: Reads actual code → understands WHAT it does → assesses quality
```

**This means Claude can:**
- Understand business logic, not just syntax
- Identify architectural issues that regex can't find
- Provide context-aware recommendations
- Explain issues in plain English
- Analyze ANY programming language

## 🔍 Supported Languages

**All of them!** Claude can analyze:
- Python, JavaScript, TypeScript, Java, C#, Ruby, Go, PHP
- C++, Swift, Kotlin, Rust, Scala, Elixir, Haskell
- Any language Claude understands

The same quality principles apply across all languages:
- Complexity is complexity
- Duplication is duplication
- Poor architecture is poor architecture

## 📖 What You Get

### Technical Assessment
- **Complexity scores** based on AI understanding of code difficulty
- **Quality analysis** identifying specific code smells and anti-patterns
- **Maintainability assessment** evaluating how risky changes are
- **Architecture review** spotting structural issues

### Business Translation
- **Annual delivery drag**: "$890K/year from 18% slower development"
- **Incident costs**: "$230K/year from expected production issues"
- **Onboarding friction**: "$125K/year from complex codebase"
- **Total tech debt tax**: Combined annual cost

### Actionable Insights
- **Prioritized recommendations** based on ROI
- **Specific fix suggestions** (not vague advice)
- **Effort estimates** in engineer-weeks
- **ROI calculations** with payback periods

### Plain English Explanations
- **No jargon**: "Like dominoes - change one thing, five others fall"
- **Real analogies**: "Swiss Army knife doing everything poorly"
- **Business context**: Why it matters to executives

## ⚙️ Configuration

Customize cost assumptions in `config/cost_config.yaml`:

```yaml
organization:
  name: "Your Company"
  engineer_count: 50
  avg_salary: 150000

incidents:
  avg_engineering_hours: 8
  avg_revenue_impact: 5000
```

Claude will use these values to calculate business impact specific to your organization.

## 🎓 Use Cases

### For Engineering Leaders
- **Get budget** for tech debt work with quantified ROI
- **Justify refactoring** to executives in business terms
- **Prioritize** what to fix first based on impact
- **Track improvement** over time with metrics

### For Executives
- **Understand** hidden costs of "just ship it"
- **Make informed** trade-off decisions
- **See ROI** of engineering investments
- **Compare** to industry benchmarks

### For Engineers
- **Quantify** pain points with objective data
- **Get buy-in** for improvements from leadership
- **Focus effort** on high-impact work
- **Reduce frustration** from legacy code

## 🔒 Privacy & Security

- **All analysis runs locally** within Claude Code
- **No code sent to external services** (Claude is already running locally)
- **No API keys required**
- **Your data stays yours**

## 📚 Documentation

- **[SKILL.md](SKILL.md)** - Detailed instructions for Claude on how to analyze code
- **[QUICKSTART.md](QUICKSTART.md)** - Get started in 30 seconds
- **[USAGE-GUIDE.md](USAGE-GUIDE.md)** - Detailed usage guide
- **[docs/skill-design-plan.md](docs/skill-design-plan.md)** - Original design document

## 🎯 Key Insight

This skill bridges the gap between engineering and business by translating:

- **"This code is terrible"** → **"$1.2M/year in lost productivity"**
- **"We need to refactor"** → **"$45K investment, $195K savings, 2.8 month payback"**
- **"High technical debt"** → **"18% slower delivery, 12 incidents/year expected"**

Language that gets budgets approved and work prioritized.

## 🏗️ How It's Different

### Traditional Static Analysis Tools
- Use regex patterns and AST parsing
- Count complexity metrics mechanically
- Limited to languages they support
- Can't understand business logic
- Generic recommendations

### Claude Tech Debt Analyzer
- Uses AI to understand code
- Assesses quality contextually
- Works with any language
- Understands business impact
- Specific, actionable recommendations

## 💻 Requirements

- **Claude Code** installed
- **No API keys** needed
- **No external dependencies** required
- **Optional**: `pyyaml` for YAML config support

## 🤝 Contributing

This skill is designed to be extended:
- Add new cost models
- Customize scoring weights
- Add industry-specific benchmarks
- Enhance report formats

See `docs/skill-design-plan.md` for the original vision and future enhancements.

## 📄 License

MIT License - use freely in your organization.

## 🌟 Example Session

```
User: Can you analyze my codebase for technical debt?

User: /claude-tech-debt-analyzer analyze ~/my-project

Claude: I'll analyze your codebase for technical debt using AI.

[Scans repository - finds 150 source files]
[Analyzes code quality using AI understanding]
[Calculates business impact]
[Generates report]

Analysis complete! Here's what I found:

Overall AI Debt Score: 58/100 (MODERATE)
Annual Cost: $1.24M

Top Issues:
1. UserService.java - 87/100 (CRITICAL)
   - 847 lines mixing authentication, authorization, and sessions
   - No error handling in critical paths
   - Changes take 3x longer than they should
   - Annual cost: $285K
   - Fix: $45K → Saves $195K/year (1,200% ROI)

2. PaymentProcessor.java - 79/100 (HIGH)
   - Duplicate payment logic across 3 files
   - 38 different exception cases without strategy
   - 3 incidents last quarter
   - Annual cost: $210K
   - Fix: $30K → Saves $145K/year (1,350% ROI)

I've saved a detailed report to ~/my-project/tech-debt-analysis/tech-debt-report.md

Would you like me to explain any of these findings in more detail?
```

## 🚀 Get Started

```bash
# Install in Claude Code
/install https://github.com/yourusername/claude-tech-debt-analyzer

# Use it
/claude-tech-debt-analyzer analyze /path/to/your/repo
```

**Transform technical debt from feelings into data-driven decisions.**

---

Built as a Claude Code skill that leverages Claude's native code understanding • No API keys required • Works with any programming language
