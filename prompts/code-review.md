# Prompt: Turn a pull request into an interactive code review

You are reviewing a change in a real codebase. Produce a **single self-contained HTML file** that helps a developer understand what changed, assess risks and work through a review. Treat review quality as the goal; the interface is a way to make that review easier to explore.

## Input

- Target: **[PR URL, branch, or commit range]**. If none is supplied, compare the current branch against its likely base and identify the exact commits used.
- Audience: **[reviewer experience or relevant subsystem, optional]**.

## Investigation

1. Inspect the repository, the actual diff (including renames), relevant tests and surrounding code. Read enough context to understand behavior; never infer behavior from an isolated changed line.
2. Explain the intent of the change and identify impacted behavior, affected files and tests. Distinguish existing behavior from newly introduced behavior.
3. Look for correctness, security, reliability, performance, compatibility and missing test coverage. Prioritize actionable, high-confidence concerns. Do not invent findings to fill space or nitpick style.
4. For every finding, retain its **repository path, diff hunk and exact old/new line number**, evidence, severity and a concrete consequence. Mark uncertain points as **Check:** questions and explicitly say when no significant issues were found.
5. Cite source locations with permalinks to the reviewed revision. If you rely on external documentation, cite it separately. Do not imply that educational comments are the opinions of the original PR maintainers.

## The page

Build a custom interactive review experience, not a Markdown report with CSS. Include:

- A concise change summary explaining *why* it matters; affected areas, key tests and the main review questions.
- File navigation and readable unified or side-by-side diffs, with accurate old/new line numbers. Make changed lines visually distinct and allow selecting a finding to jump to its evidence.
- Useful exploration tailored to the change. For example, a path resolver for routing changes, a state transition explorer for reducers or a request lifecycle for networking code. Ground any simulator in actual behavior and label simplifications.
- Reviewer progress tracking, stored locally and resettable, plus keyboard navigation and sensible mobile behavior.
- Clear distinctions between **confirmed issue**, **review question**, **test/coverage observation** and **explanation**.

## Output contract

- Write `review.html`: one file with embedded CSS, JavaScript, and escaped source snippets; no frameworks, CDN resources, external assets, installs, network requests, or telemetry.
- Data must be derived from the actual target, not invented placeholders. Pin the source PR/commits in the page.
- Validate that each note points to a unique existing changed line. Fail loudly on missing or ambiguous anchors and missing changed files. Source text must be escaped to prevent HTML or script injection.
- Open `review.html` in a browser. Check navigation, source links, note highlighting, progress persistence/reset, mobile layout, dark mode and console errors; fix problems before responding.
- Finish with a short summary of major **Check:** items, or state that there are no significant ones. Mention limitations and any checks you could not run.

**Key principle:** An insightful review without many comments is better than a noisy report. Never sacrifice correctness for a visually impressive page.
