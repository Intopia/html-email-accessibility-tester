# Archive

This folder holds the development history of the tool from before it was tracked in git, 28 versions built iteratively in conversation with Claude. From this point forward, git handles version history, this archive exists purely to preserve that early record rather than lose it.

## Naming

Files are numbered in build order: `postmark-v1.html` through `postmark-v28.html`, oldest first. The current live version is `index.html` at the repo root, not duplicated here.

## What changed, and roughly when

**Foundation (early versions)**
- Initial build: single-page tool, 7 core tests (headings, links, images, document title, document language, document encoding, tables)
- Bug fixes found by testing against real "good" and "bad" example emails rather than trusting the logic on read-through (heading-absence status, table role-detection logic)
- "Start over" fixed to actually clear the form

**Growing the test suite**
- Added colour contrast (real WCAG contrast ratio maths), a data-table-headers check, duplicate ID detection, and an alt-text-quality heuristic
- The data-table-headers check was later merged into the Tables test rather than kept separate, one table is either a marked-up layout table or a real data table with a caption and headers, not two disconnected checks
- The alt-text-quality test was removed entirely, it was the one subjective/heuristic test in a suite where every other result is deterministic and explainable
- Landmarks added as its own test, the most rule-heavy of the set: correct use of banner/main/contentinfo, no invalid nesting, no unnamed duplicates

**Interface**
- Icon-based pass/fail "stamps" replaced with plain colour-coded text badges (icons were judged not reliably accessible)
- Summary results changed from a multi-column grid to a single-column list after layout/overflow bugs
- Full Intopia rebrand: logo, brand colour and font, card backgrounds, borders
- Renamed from a placeholder "Postmark" concept to the plain, descriptive "HTML email accessibility tester"
- A "load a sample email" button was built, then removed, the label caused genuine confusion about what it did, and it wasn't relevant for real users testing their own emails
- Replaced with a proper two-option input: paste HTML, or upload a `.html` file directly

**Accessibility of the tool itself**
- Several rounds of text-size and contrast fixes (small, low-contrast text is a poor look for an accessibility tool)
- Focus management corrected after running tests: focus moves to a real, visible "Results" heading, not a hidden one
- Removed an unnecessary `role="alert"` and a hidden live-region announcement, both were redundant once focus management and native semantics were doing the same job properly
- Heading hierarchy corrected so results content nests logically under a single "Results" heading

**Test order**
- Tests were reordered late in development to follow document order (title, language, encoding, then structural checks, then landmarks and contrast), rather than the order they happened to be built in

## Verification

Nearly every change of substance was tested against real files, not just read back, before being kept. Two sets of purpose-built test files exist alongside this archive for that reason: `test-files-general/` (one file per test/outcome) and `test-files-landmark/` (one file per landmark scenario).
