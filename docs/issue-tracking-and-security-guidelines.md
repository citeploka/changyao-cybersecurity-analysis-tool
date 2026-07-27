# Issue Tracking and Cybersecurity Guidelines

## Purpose

This document defines how Freshservice and GitHub are used to track cybersecurity features, bugs, confirmed findings, remediation work, and development progress.

## Freshservice Issue Workflow

### 1. Create an Issue

Create a Freshservice ticket before beginning a feature, bug fix, or vulnerability remediation. Include:

- A clear title
- Requirements or reproduction steps
- Expected and actual results
- Security impact and priority
- Acceptance criteria
- Sanitized evidence with sensitive information removed

Example titles:

```text
Implement security log incident detection
Implement local vulnerability assessment tool
Vulnerability: possible exposed credential in configuration file
Bug: malformed log entry terminates analysis
```

### 2. Track Status

- Open: investigation or development is active.
- Pending: waiting for review, testing, or additional information.
- Resolved: implementation is complete, tests pass, and the pull request has been merged.
- Closed: the resolution has been verified and no additional work is required.

Freshservice may not provide a separate In Progress value. In this project, Open represents active work.

### 3. Reference Tickets in GitHub Commits

Every related GitHub commit must reference the Freshservice ticket number:

```bash
git commit -m "Refs INC-3: improve vulnerability assessment checks"
```

Add the complete Freshservice URL to the extended commit description or pull request when useful.

Use Refs INC-x instead of Fixes #x. The Fixes #x syntax targets a GitHub issue and could close an unrelated GitHub issue.

### 4. Create a Pull Request

Create pull requests from feature branches into development. The description should include:

- Summary of the change
- Freshservice reference such as Refs INC-3
- Security impact and limitations
- Test commands and results
- Follow-up work

### 5. Resolve the Freshservice Issue

After testing and merging the pull request, add a resolution note containing:

- Work completed
- GitHub branch, commit, and pull request
- Test results
- Security impact
- Known limitations
- Required follow-up work

Example resolution note:

```text
The requested cybersecurity feature has been implemented and validated.

Resolution details:
- GitHub commits reference this Freshservice issue.
- Automated tests completed successfully.
- Usage instructions and security limitations were documented.
- The feature was reviewed and merged into the development branch.
- No intrusive or external network scanning was performed.
```

Change the Freshservice status to Resolved only after the implementation and verification are complete.

## Vulnerability Documentation Procedure

Create a separate Freshservice ticket for each distinct, confirmed vulnerability. Do not create real vulnerability tickets for synthetic sample findings.

Each ticket should include:

### Summary

A concise description of the weakness and affected component.

### Severity

Use Critical, High, Medium, Low, or Informational.

### Evidence

Record the affected file or component, line number, detection rule, sanitized evidence, tool version or commit, and detection date.

Never include passwords, tokens, private keys, personal information, or complete sensitive logs.

### Reproduction

Document safe steps that confirm the finding without exploiting an external system.

### Impact

Explain what could happen if the weakness remains unresolved.

### Remediation

Provide a specific corrective action, such as rotating an exposed credential, restricting permissions, replacing an insecure configuration, validating untrusted input, or updating a vulnerable dependency.

### Verification

1. Run the assessment again after remediation.
2. Confirm the original finding is no longer reported.
3. Run the complete automated test suite.
4. Reference the ticket in the corrective commit.
5. Add the commit or pull request link to Freshservice.
6. Change the ticket to Resolved after verification.

## Cybersecurity Procedures

### Authorization

Analyze only logs, files, applications, and systems that the user owns or is explicitly authorized to assess.

### Non-Intrusive Testing

The vulnerability tool is limited to local static analysis. It must not exploit vulnerabilities, attempt authentication, scan external hosts, bypass access controls, modify assessed files without approval, or execute scanned content.

### Sensitive Data Handling

- Use synthetic data for tests and demonstrations.
- Remove credentials and personal information from evidence.
- Do not commit production logs, API keys, passwords, private keys, or session tokens.
- Rotate any real credential discovered during testing.
- Add sensitive and generated files to .gitignore.

### Secure Input Processing

- Treat logs and configuration files as untrusted input.
- Never execute scanned content.
- Handle malformed input safely.
- Apply file-size limits where appropriate.
- Skip binary files, .git, virtual environments, and generated directories.
- Validate file paths before reading them.

### Finding Quality

Every finding should contain a stable rule identifier, severity, file and line number, detection reason, sanitized evidence, and recommended remediation. Review possible false positives before confirming a vulnerability.

## Verification Before Commit

Run tests:

```bash
python3 -m unittest discover -s tests -v
```

Review staged changes for secrets and unintended files:

```bash
git diff --cached
```

Confirm that the commit references the correct Freshservice ticket and contains no sensitive sample data.

## Branch and Release Process

- feature/log-analysis contains log-analysis work.
- feature/vulnerability-scan contains vulnerability-assessment work.
- Feature pull requests target development.
- A separately reviewed pull request may promote tested development changes into main.
