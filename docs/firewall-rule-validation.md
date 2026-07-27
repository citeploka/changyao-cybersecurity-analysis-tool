# Firewall Rule Validation

Freshservice issue: [INC-1](https://changyaozhi.freshservice.com/a/tickets/1?current_tab=details)

## Goal

Validate firewall rules before they are saved or applied so configuration errors do not cause deployment failures or unintended network exposure.

## Requirements

- Validate source and destination IPv4/IPv6 addresses and CIDR notation.
- Validate ports are between 1 and 65535.
- Reject port ranges whose start value exceeds the end value.
- Validate supported protocols such as TCP, UDP, and ICMP.
- Detect duplicate, conflicting, and shadowed rules.
- Warn about unrestricted sources such as `0.0.0.0/0` and `::/0`.
- Require explicit approval for overly broad rules.
- Return actionable errors that identify the rule, invalid field, and expected format.
- Prevent invalid rules from being saved or applied.

## Acceptance Criteria

- Valid existing rules continue to work without modification.
- Invalid rules are rejected before deployment.
- Duplicate, conflicting, and shadowed rules are detected.
- Broad-access rules generate a visible security warning.
- Validation behaves consistently through the user interface and API.
- Automated tests cover malformed CIDRs, invalid ports and ranges, unsupported protocols, duplicates, conflicts, shadowed rules, and unrestricted access.
