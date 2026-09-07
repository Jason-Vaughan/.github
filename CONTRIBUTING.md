# Global Contribution Guidelines

Welcome! This is the default contribution guide for all open-source projects managed by this account.

By participating in any of our repositories, you agree to abide by our Code of Conduct and by the
architecture rules of the individual project. Where a repository ships its own `CONTRIBUTING.md`,
that file wins — it is more specific than this one, and it is the one you should read.

## The Developer Experience

**Be prepared for rigorous review.** We value contributions immensely, but maintaining a secure,
zero-telemetry, local-first ecosystem requires strict discipline. Expect meaningful back-and-forth:
we will ask you to justify your architecture, defend your dependencies, and adhere to our governance
policies. That is the same bar the maintainers hold themselves to, and a contribution that clears it
is genuinely valued.

## Security & Contribution Guidelines

**Supply chain security and PR review standards.**

We operate under a "Zero Trust" model to protect the integrity of our projects and our users' local
hardware. We do not keep our security protocols a secret — transparency is our first line of
defence, and knowing the rules up front is what lets a good contribution get in.

<!-- BEGIN mirrored-security-rules -->
1. **The Clean Room Reconstruction Standard (Dual-Key Review).** Pull requests from contributors we do not know are reviewed as **raw text diffs** through a strict dual-key process:
   - **First Pass (Macro Filter):** The Coordinator session performs the initial security audit, explicitly checking for supply chain attacks, `package.json` tampering, and broad logical soundness.
   - **Second Pass (Micro Filter):** If the PR passes the Coordinator, the Builder session performs an independent raw-text audit to catch subtle logic bombs or regressions before execution.
   
   Maintainers will not check out your branch or run your code on their own machines. If your contribution clears both audits, the Builder re-implements the logic from scratch on `main` and **credits you as the author**. We merge ideas, not raw bytes.

   To be precise, because this is a security claim and a vague one is worthless: *continuous
   integration does run your tests* when a repository's workflows are triggered by pull requests.
   Those runs are sandboxed by GitHub, with a read-only token and no access to repository secrets.
   The commitment is that no maintainer executes your code on their own hardware.

2. **Because we reconstruct it, your explanation is worth more than your code.** The most valuable
   pull request describes the bug precisely, says why it happens, and explains the approach. A clear
   description gets reconstructed and shipped. A large, clever, unexplained diff does not, however
   good it is.

3. **Scope.** One issue per pull request, and nothing outside it. A diff that touches files
   unrelated to the issue will be closed regardless of quality — from the outside, scope overrun and
   probing are indistinguishable.

4. **Forbidden files.** Core infrastructure is off-limits unless an issue explicitly asks for a
   change there: CI workflows (`.github/workflows/`), build scripts and `Makefile`s, install or
   deploy scripts, git hooks, and orchestrator configuration. What these have in common is that they
   execute **without anyone choosing to run them**, which is what separates them from ordinary
   source. Unexplained modifications there are treated as payload and the pull request is closed.

5. **Reviewable text only.** No binary files, and no generated, minified or vendored code — none of
   them can be read as a diff, and a diff is the only review we perform.

   For the same reason, source must contain no **bidirectional control characters**, no
   **zero-width or invisible characters**, and no **non-ASCII homoglyphs standing in for ASCII in
   identifiers**. Those three make a diff *render* differently from what it *executes*
   ("Trojan Source", CVE-2021-42574) — an attack aimed precisely at a text-based review, which
   defeats our method by construction rather than by degree. Ordinary Unicode in prose, comments and
   string literals is fine: it is the invisible and the disguised that are the problem, not the
   non-English.

6. **No new dependencies.** Adding third-party libraries, npm packages or PyPI dependencies
   introduces supply-chain risk that these projects have deliberately designed out. Unless an issue
   explicitly asks for a new dependency, do not add one — and note that some of our repositories are
   strictly zero-dependency, where adding one is an automatic rejection. A solution built on the
   standard library is vastly preferred over importing a new package.

7. **No obfuscation.** Code must be clear and readable. Base64 payloads, hidden network requests,
   dynamic `eval`/`require` of constructed strings, or deliberately obscured logic will result in an
   immediate ban. This is the one rule where we assume intent, because none of those happen by
   accident.

<!-- END mirrored-security-rules -->
## Branch & PR conventions

- **Branch from `main`** with a typed name (e.g. `feat/`, `fix/`, `docs/`, `chore/`).
- **Keep commits small and focused.**
- **Open a pull request** describing the *What*, the *Why*, and the *Test Plan*.

Thank you for helping us build secure, reliable, and sovereign software!
