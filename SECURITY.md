# Security Policy

## Supported Versions

We provide security updates for the `main` branch and the latest published release of our projects.

## Reporting a Vulnerability

**Please do not open a public issue for a security vulnerability.**

Report it privately through GitHub instead: go to the affected repository, open the **Security** tab,
and choose **Report a vulnerability**. That opens a private advisory visible only to you and the
maintainers, so nothing is disclosed while a fix is being prepared. It needs no email address and no
account beyond the one you already have.

If that option is not available on the repository in question, open an issue containing **only** a
request for a private channel — no details, no reproduction steps, no proof of concept — and a
maintainer will open one for you.

## What to expect

- **Acknowledgement** that the report was received, so you are not left guessing.
- **An assessment**, including a plain statement if we conclude it is not exploitable and why.
- **Credit** in the advisory and the release notes, unless you would rather stay anonymous.

## Scope

These projects orchestrate AI sessions and developer tooling that run with real permissions on real
machines, so we are particularly interested in:

- anything that lets one project's session read or write another's files;
- anything that escalates what a session may execute beyond what the operator granted;
- credential, token or secret exposure — in logs, in configuration written to disk, or over the wire;
- supply-chain vectors: dependency confusion, install-time or lifecycle script execution, and code
  that executes without anyone choosing to run it.

Please tell us what you found and how to reproduce it. A clear report gets fixed faster than a
clever one.
