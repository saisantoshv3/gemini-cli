🧠 Gemini CLI Skills Library
This repository contains a collection of .md skill files designed to extend the capabilities of the Gemini CLI. These files allow the AI to perform complex, domain-specific tasks like data standardization, local file manipulation, and cross-platform automation.

📂 Repository Structure
skills/: Contains all logic-heavy Markdown files.

skills/assets/: Centralized storage for reference data (CSVs, JSONs, Templates).

scripts/: Python or Shell helper scripts referenced by the skills.

🛠 How to Use a Skill
To load a skill into your Gemini CLI session, point the tool to the specific directory:

Bash
gemini --skill ./skills/district-standardization.md "Standardize the attached file"
📝 Skill Development Standards
To ensure skills are portable and token-efficient, follow these formatting rules:

1. Relative Pathing
Never use absolute paths (e.g., /Users/username/...). Always use relative paths from the repository root.

✅ path: ./assets/dictionary.csv

❌ path: /Users/apple/projects/assets/dictionary.csv

2. Structured Headers
The Gemini CLI uses headers to prioritize context. Use this hierarchy:

# SKILL NAME: Title.

## ENVIRONMENT: Dependencies and file requirements.

## ACTION: Step-by-step logic.

## ERROR HANDLING: What to do when things fail.

🌟 Example: District Standardization
Below is an example of a well-optimized SKILL.md located in this repo.

Markdown
# SKILL: district-standardization

> Standardizes raw district names against LGD standards.

## ENVIRONMENT
- **Reference:** `./assets/district_dictionary.csv`
- **Logic:** Python (pandas + fuzzywuzzy)

## ACTION: MAP_DATA
1. **Load Reference:** Open `./assets/district_dictionary.csv`.
2. **State Filter:** Match the `district` input only against rows sharing the same `state` value.
3. **Fuzzy Match:** Use a score threshold of 90+ to map raw names to `district_as_per_lgd`.
4. **Append:** Add `lgd_code` to the output file.

## ERROR HANDLING
- If a match score is < 90, stop execution and log the offending row.
- Do not "hallucinate" or guess district names.
🤝 Contributing
Lint your Markdown: Ensure no broken headers.

Test Cross-Platform: Ensure forward slashes / are used for paths (compatible with Windows & Mac).

Minimize Tokens: Use bullet points and imperative verbs instead of long paragraphs.
