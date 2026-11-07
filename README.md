# Password Strength Evaluator & Breached Credential Checker

A Python-based information security utility designed to evaluate credential complexity, calculate structural entropy scores, provide remediation suggestions, and verify passwords against known compromised dictionary wordlists (e.g., RockYou).

## Overview

Weak credentials represent one of the primary vectors in unauthorized authentication attacks, credential stuffing, and dictionary brute-force exploits. This utility evaluates user-supplied passwords against industry complexity baselines and scans local breach corpuses to warn users before adopting compromised credentials.

## Evaluation Criteria and Scoring Model

The password analysis engine tests the candidate string against five structural rules:

1. Length Baseline: Minimum length of 8 characters (mitigates low-entropy space).
2. Lowercase Alphabet: Presence of characters in range `[a-z]`.
3. Uppercase Alphabet: Presence of characters in range `[A-Z]`.
4. Numeric Characters: Presence of digits `[0-9]`.
5. Special Symbols: Presence of non-alphanumeric punctuation `[!@#$%^&*(),.?":{}|<>]`.

### Strength Classification

The complexity score is calculated as:

$$\text{Score} = 5 - \sum_{i=1}^{5} \mathbb{I}(\text{Rule}_i = \text{False})$$

- Weak (Score 0-2): Susceptible to instant automated brute-force attacks.
- Medium (Score 3-4): Meets basic thresholds but lacks full character diversity or length.
- Strong (Score 5): Fully compliant with all entropy criteria.

## Compromised Wordlist Verification

In addition to static structural entropy, the utility queries a localized breach dictionary (`rockyou.txt` or equivalent wordlist) using streaming line-by-line inspection to prevent excessive memory consumption. If the input password exists within the wordlist, a critical security advisory is displayed regardless of its structural score.


## Execution Preview

[![Execution Preview Status](https://img.shields.io/badge/CLI_Preview-Documentation_in_Progress-2563eb?style=for-the-badge&logo=python&logoColor=white)](https://github.com/ANTARTICA1/Password-Checker)

## Features

- Real-Time Heuristic Feedback: Returns granular improvement suggestions for each unmet security criterion.
- Memory-Efficient Wordlist Lookup: Streams dictionary entries without loading entire multi-gigabyte lists into RAM.
- Colored Terminal Interface: ANSI-compliant formatted console diagnostics powered by `colorama`.
- Zero Complex Setup: Lightweight Python codebase requiring minimal third-party dependencies.

## Project Structure

```
Password-Checker/
├── PasswordStrength.py     # Core complexity evaluator and wordlist search logic
└── README.md               # Technical documentation
```

## System Requirements

- Python 3.8 or higher
- Optional: `rockyou.txt` wordlist placed in the project directory for dictionary auditing

## Installation and Execution

1. Clone the repository:
   ```bash
   git clone https://github.com/ANTARTICA1/Password-Checker.git
   cd Password-Checker
   ```

2. Install dependencies:
   ```bash
   pip install colorama
   ```

3. (Optional) Provide `rockyou.txt`:
   Place a decompressed `rockyou.txt` file inside the root directory to activate breached password detection.

4. Run the tool:
   ```bash
   python PasswordStrength.py
   ```

5. Enter the target password when prompted. The tool outputs the complexity score, strength level, remediation suggestions, and wordlist match status.

## Author

Anak Agung Ngurah Krisna Artha Wibawa ([ANTARTICA1](https://github.com/ANTARTICA1))

## License

This project is open-source and licensed under the MIT License.