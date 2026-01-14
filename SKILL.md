# Claude Tech Debt Analyzer

A Claude Code skill that analyzes codebases for technical debt and translates findings into business impact.

## What This Skill Does

When invoked, you (Claude) will:
1. Scan the repository for source files in any programming language
2. Analyze code files for technical debt using your understanding of software quality
3. Calculate business impact in dollars (delivery drag, incident costs, onboarding friction)
4. Generate an executive-friendly report with ROI calculations

## Usage

```bash
/claude-tech-debt-analyzer analyze [path]
```

Analyzes the specified repository (or current directory) and generates a comprehensive technical debt report.

## How You Should Analyze Code

When analyzing each file/module, assess:

### 1. Complexity (Score 0-100, higher = worse)
- **Control flow complexity**: Deeply nested conditionals, long if-else chains
- **Cognitive load**: How hard is it for a human to understand what this code does?
- **Function/method length**: Are functions doing too much?
- **Class size**: Are classes taking on too many responsibilities?

### 2. Code Quality (Score 0-100, higher = worse)
- **Duplication**: Repeated code patterns that should be abstracted
- **Code smells**: God classes, long methods, magic numbers, poor naming
- **Dead code**: Unused functions, commented-out code
- **Consistency**: Does the code follow consistent patterns?

### 3. Maintainability (Score 0-100, higher = worse)
- **Coupling**: How intertwined are different parts of the code?
- **Cohesion**: Do related things belong together?
- **Architecture**: Is the structure clear and logical?
- **Modifiability**: How risky is it to change this code?

### 4. Specific Issues
Identify concrete problems:
- "The `UserService` class has 847 lines and handles authentication, authorization, AND session management"
- "Payment logic duplicated across 3 different files"
- "No error handling in database transaction code"

### 5. Business Impact
Explain in plain English why these issues matter:
- "This authentication code is so complex that changes take 3 days instead of 0.5 days"
- "High risk of breaking user login when making changes"
- "New engineers need 2 extra weeks to understand this module"

### 6. Recommendations
Provide specific, actionable improvements:
- "Split UserService into AuthenticationService, AuthorizationService, and SessionService"
- "Extract duplicate payment logic into shared PaymentProcessor class"
- "Add try-catch blocks around database transactions"

## Scoring Guidelines

**0-30 (Low Risk - 🟢)**
- Clean, well-structured code
- Easy to understand and modify
- Good practices followed

**30-60 (Moderate Risk - 🟡)**
- Some complexity or technical debt
- Manageable but could be improved
- Plan to address in next quarter

**60-80 (High Risk - 🟠)**
- Significant technical debt
- Slowing down development
- Should address within 1-2 months

**80-100 (Critical Risk - 🔴)**
- Severe technical debt
- High risk of incidents
- Immediate action needed

## Business Impact Calculation

Use these formulas to translate technical debt into dollars:

### Delivery Drag
- Team slower by X% due to bad code
- Annual cost = Team size × Working days × Hours/day × Hourly rate × X%

### Incident Risk
- Higher debt score = more likely to cause production issues
- Estimate incidents/year based on code quality
- Cost per incident = Engineering time + Revenue impact + Customer impact

### Onboarding Friction
- Complex code = longer ramp-up time for new engineers
- Extra days = Debt score / 10 × 5 days
- Cost = Extra days × Hourly rate × 1.5 (includes mentoring)

## Output Format

Generate a markdown report with:

1. **Executive Summary**
   - Overall debt score
   - Total annual cost
   - Module health overview

2. **Top Priorities**
   - 3-5 worst modules with business impact
   - ROI calculations for fixing each
   - Plain English explanations

3. **Financial Impact**
   - Cost breakdown (delivery drag, incidents, onboarding)
   - Proposed improvements with ROI

4. **Module Scorecard**
   - All modules with risk levels
   - Key issues per module

5. **Action Plan**
   - Prioritized recommendations
   - Estimated effort and savings

6. **Glossary**
   - Technical terms explained in plain English
   - Real-world analogies

## Where to Save the Report

**IMPORTANT**: Save the report to a dedicated analysis directory to keep the analyzed repository organized.

- **Directory**: `tech-debt-analysis/` in the analyzed repository root
- **Filename**: `tech-debt-report.md`
- **Full path example**: `/path/to/repo/tech-debt-analysis/tech-debt-report.md`

This keeps analysis artifacts separate from the codebase while remaining easy to find and share.

## Key Principles

- **Be objective**: Base scores on actual code issues, not feelings
- **Be specific**: "847-line class" not "class too big"
- **Translate to business**: "$1.2M/year in lost productivity" not "high complexity"
- **Provide context**: Explain WHY issues matter
- **Be actionable**: Give concrete next steps with ROI

## Multi-Language Support

Analyze code in any language:
- Python, JavaScript, TypeScript, Java, C#, Ruby, Go, PHP, C++, Swift, Kotlin, Rust, etc.

Apply the same quality principles across all languages:
- Complexity is complexity regardless of language
- Duplication is duplication
- Poor architecture is poor architecture

## Plain English Translations

When explaining technical concepts, use analogies:

- **Cyclomatic complexity** → "Like a maze with many paths - more ways for bugs to hide"
- **Tight coupling** → "Like dominoes - change one thing, five others fall"
- **Code duplication** → "Same paragraph in five book chapters - fix typo in all five"
- **God class** → "Swiss Army knife doing everything poorly instead of one thing well"
- **Technical debt** → "Credit card debt - borrow now, pay interest forever"

## Configuration

Default cost assumptions (customizable in config/cost_config.yaml):
- Engineer count: 50
- Average salary: $150,000
- Loaded hourly rate: $75
- Working days/year: 220

## Example Analysis

When you analyze code like this:

```python
# UserService.py (847 lines)
class UserService:
    def authenticate(self, username, password):
        # 50 lines of complex logic
        # No error handling
        # Mixes authentication and session management
```

You should identify:
- **Complexity Score**: 85/100 (very high - 847 lines, multiple responsibilities)
- **Quality Score**: 75/100 (high - no error handling, mixed concerns)
- **Maintainability Score**: 80/100 (high - hard to modify safely)
- **Issues**: ["847-line class", "No error handling", "Mixed responsibilities"]
- **Business Impact**: "Changes take 3x longer, high risk of breaking login"
- **Recommendations**: ["Split into 3 services", "Add error handling", "Write unit tests"]

Then calculate:
- Delivery drag: $95K/year
- Incident risk: $30K/year
- ROI of fixing: $45K investment saves $125K/year = 4.3 months payback

## Your Goal

Help engineering leaders:
- Get budget for tech debt work
- Prioritize what to fix first
- Communicate with executives in business language
- Track improvement over time

Make technical debt measurable, understandable, and actionable.
