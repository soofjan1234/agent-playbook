---
name: fuck-u-code-analysis
description: Run `fuck-u-code analyze` on a repo or subdirectory, interpret the quality report, and turn the output into actionable engineering judgment. Use when the user wants a code-quality scan, wants to compare frontend/backend quality, wants help understanding the worst files or metrics, or wants prompt/planning input grounded in `fuck-u-code` results.
---

# fuck-u-code analysis

Run this skill when the user wants fast repo-local code-quality evidence from `fuck-u-code`, especially before planning refactors, writing implementation prompts, or judging whether a subsystem is risky.

## Quick workflow

1. Confirm the scope.
   - Use the exact path the user named.
   - If they did not name a path, default to the current repo root.
   - For split repos, prefer analyzing `frontend`, `backend`, or another concrete subdirectory separately before analyzing the whole repo.

2. Run the analyzer.
   - Basic scan:

     ```powershell
     fuck-u-code analyze <path>
     ```

   - Chinese output when the surrounding conversation is Chinese:

     ```powershell
     fuck-u-code analyze <path> -l zh
     ```

   - Use verbose mode only when you need extra function- or language-level detail:

     ```powershell
     fuck-u-code analyze <path> -l zh -v
     ```

   - Use `-t <n>` when the repo is large and you want a deeper hotspot list:

     ```powershell
     fuck-u-code analyze <path> -l zh -t 20
     ```

3. Interpret the result in this order.
   - Overall score and quality level.
   - Metric outliers.
   - Top hotspot files.
   - Whether the hotspots are localized or systemic.

4. Convert the report into engineering judgment.
   - Distinguish structural risk from cosmetic issues.
   - Call out whether the worst files are in hot runtime paths, glue code, plugin bridges, CLI/build logic, or leaf UI.
   - Use the file ranking to decide whether a future prompt should demand minimal edits, targeted refactor, or phased migration.

## How to read the output

### Overall score

- `90+`: healthy enough for targeted work; do not invent a rewrite justification.
- `80-89`: workable, but expect concentrated smells in a few subsystems.
- `70-79`: medium risk; prompts should include stronger guardrails and narrower scope.
- `<70`: do not let agents roam freely; force staged work and stronger validation.

### Metrics

Prioritize metrics in this order when writing conclusions:

1. `Error Handling`
   - High error-handling smell usually means hidden failure states, fragile async flow, or operational risk.
2. `Complexity` and `Cognitive Complexity`
   - High values usually mean poor change safety.
3. `Duplication`
   - Important when the same bug or policy drift can repeat across files.
4. `Structure Analysis`
   - Useful for spotting swollen files, nesting, or poor boundaries.
5. `Comment Ratio`
   - Treat this as low-priority unless the code is also complex; do not overreact to low comments alone.

### Hotspot files

Read the top files as a risk map, not just a style list.

- Runtime bridge / plugin / event files -> likely high regression risk.
- API glue / CLI parsing / setup builders -> likely user-flow or integration risk.
- Large composables / page orchestration -> likely future prompt should enforce thinner boundaries.
- Leaf presentational components -> usually lower architectural risk even if ugly.

## How to turn results into a useful answer

Use this structure by default:

1. `结果`
   - One short paragraph or 2-4 bullets.
2. `关键证据`
   - Score, bad metrics, top files.
3. `判断`
   - What the report actually implies for the user's goal.
4. `下一步`
   - What to refactor, what to postpone, or how to shape the next prompt.

## Prompt-writing guidance based on the report

When the user asks you to produce a prompt after analysis:

- If hotspots are concentrated in a shared subsystem, tell the implementer to patch the shared layer instead of page-local workarounds.
- If a file has very high complexity or cognitive complexity, instruct the agent to keep edits minimal unless explicit refactor is requested.
- If `Error Handling` is a major smell, require visible failure-state handling and forbid swallowing errors.
- If next-page composables or route-level views appear in the hotspot list, require thinner page composition and split logic into smaller composables/components.
- If plugin/runtime bridge files dominate, treat them as compatibility-sensitive and require extra caution before deleting or bypassing legacy surfaces.

## Constraints

- Prefer `fuck-u-code analyze`, not `ai-review`, unless the user explicitly asks for AI review.
- Do not claim code is bad just because the tool uses humorous wording.
- Summarize decisive lines instead of pasting the full report.
- Keep recommendations grounded in the report and the actual files it names.
- If the user asks for comparison, run separate scans per subsystem instead of guessing from one aggregate score.

## Useful command patterns

Frontend vs backend comparison:

```powershell
fuck-u-code analyze frontend -l zh
fuck-u-code analyze backend -l zh
```

Top hotspots for prompt preparation:

```powershell
fuck-u-code analyze frontend -l zh -t 15
```

Exclude obvious noise if needed:

```powershell
fuck-u-code analyze . -l zh -e "**/*.test.ts"
```

Markdown export when the user wants a saved report:

```powershell
fuck-u-code analyze . -l zh -f markdown -o fuck-u-code-report.md
```
