# Changyao Cybersecurity Analysis Tool

A modular Python toolkit for security log analysis, local vulnerability assessment, and repeatable defensive cybersecurity investigations.

## Features

### Security Log Analysis

- Analyze security log files for suspicious activity.
- Detect repeated failed logins, unauthorized access, privilege escalation indicators, and unusual error patterns.
- Handle malformed entries safely without executing log content.
- Produce readable findings and optional structured output when implemented.

### Vulnerability Assessment

- Perform safe, local static checks on user-selected files and directories.
- Identify possible exposed secrets, unsafe permissions, and insecure configuration settings.
- Report severity, evidence, and remediation guidance.
- Do not exploit vulnerabilities or perform intrusive network scanning.

## Project Structure

```text
src/
├── log_analysis.py
└── vulnerability_assessment.py

tests/
├── test_log_analysis.py
└── test_vulnerability_assessment.py

docs/
├── log-analysis.md
├── vulnerability-assessment.md
└── issue-tracking-and-security-guidelines.md

samples/
├── security.log
└── vulnerable-config.txt
```

The files under samples must contain synthetic test data only and must never contain real credentials or confidential production logs.

## Requirements

- Python 3.10 or later
- Git
- A GitHub account
- Access to the project Freshservice workspace

## Setup

Clone the repository:

```bash
git clone https://github.com/citeploka/changyao-cybersecurity-analysis-tool.git
cd changyao-cybersecurity-analysis-tool
```

Confirm Python is available:

```bash
python3 --version
```

Optional: create an isolated environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## Running the Log Analyzer

Run the analyzer against the sanitized sample log:

```bash
python3 src/log_analysis.py samples/security.log
```

View supported options after the command-line interface is implemented:

```bash
python3 src/log_analysis.py --help
```

## Running the Vulnerability Assessment

Run the local assessment against the synthetic sample:

```bash
python3 src/vulnerability_assessment.py samples/vulnerable-config.txt
```

Or assess an authorized local project directory:

```bash
python3 src/vulnerability_assessment.py .
```

View supported options after the command-line interface is implemented:

```bash
python3 src/vulnerability_assessment.py --help
```

Only scan files and systems that you own or are explicitly authorized to assess.

## Running Tests

Run the complete test suite:

```bash
python3 -m unittest discover -s tests -v
```

## Branching Strategy

- main: stable, production-ready code.
- development: integration branch for ongoing development.
- feature/log-analysis: log-analysis development.
- feature/vulnerability-scan: local vulnerability-assessment development.
- feature/*: other isolated features.

Before pushing changes, synchronize the selected branch:

```bash
git fetch origin
git switch feature/vulnerability-scan
git pull --rebase origin feature/vulnerability-scan
```

Commits must reference the related Freshservice ticket:

```bash
git commit -m "Refs INC-3: document setup and cybersecurity workflow"
git push -u origin feature/vulnerability-scan
```

Use Refs INC-x instead of Fixes #x so GitHub does not interpret the Freshservice number as a GitHub issue.

## Issue Tracking

Freshservice is used to track new features, development bugs, confirmed security findings, false positives, remediation work, testing, and documentation tasks.

See [Issue Tracking and Cybersecurity Guidelines](docs/issue-tracking-and-security-guidelines.md) for the complete workflow.

## Cybersecurity Guidelines

- Analyze only authorized systems and data.
- Use synthetic or sanitized samples for testing.
- Never commit passwords, tokens, private keys, production logs, or personal information.
- Treat logs and configuration files as untrusted input.
- Do not execute content found in assessed files.
- Prefer non-intrusive local static analysis.
- Review findings for false positives before marking vulnerabilities as confirmed.
- Include severity, evidence, remediation, and verification steps in every confirmed finding.

## Current Status

The repository contains the project structure and documentation for the planned tools. Verify that implementations and automated tests are complete before treating either tool as production-ready.

## Responsible Use

This project is intended for defensive cybersecurity education and authorized analysis. Do not use it to access systems without permission, bypass controls, exploit detected weaknesses, or collect unnecessary sensitive data.
