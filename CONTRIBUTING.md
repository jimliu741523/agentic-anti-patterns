# Contributing

Thanks for adding to the catalog. One PR = one anti-pattern. Use the template below.

## Entry template

Copy this into the README at the correct alphabetical or thematic slot (we'll renumber on merge).

```markdown
### AP-XX — <short name>

**TL;DR.** One sentence: what the failure is, in plain language.

**Symptom.** What an operator observes in logs, metrics, or user-visible behavior.

**Example.** A short reproduction — pseudocode, a real transcript, or a public-incident citation. Prefer something a reader can believe without taking your word for it.

**Root cause.** Why the failure happens. Architectural, prompt-level, or model-level reasons. Be specific.

**Mitigations.**
- 2–4 concrete practices. Ordered roughly by cost: cheap-and-prompt-level first, architectural last.

**Detection.**
- How to catch it in production — a metric, a log query, an eval.

**References.**
- Links: paper, blog, incident writeup, docs. At least one.
```

## Quality bar

Entries are merged when they are:

1. **Specific.** "Agents can hallucinate" is not an entry. "Agents emit tool-call names that aren't in the registered schema, especially after long chains" is.
2. **Reproducible or cited.** Either include a minimal reproduction, or cite a public incident / paper / writeup. Private war stories are great to *motivate* an entry; they aren't enough on their own.
3. **Actionable.** The mitigations section must contain things a reader can do tomorrow morning, not "use a more aligned model."
4. **Scannable.** If an entry doesn't fit in ~400 words across all sections, it's probably two entries.

## Not a fit

- Pure model-quality complaints ("the model is dumb about X").
- Vendor beef.
- Hypothetical failure modes nobody has actually observed.
- Duplicates of existing entries — extend the existing one instead.

## Style

- Present tense. Active voice.
- US English.
- Code samples in fenced blocks.
- External links inline, not as footnotes.
- No emoji in entry bodies.

## Process

1. Fork and branch: `ap-<shortname>`.
2. Add your entry to the README in the appropriate section, and update the catalog table at the top.
3. Open a PR. A reviewer will respond within a few days.
4. We may edit for tone and concision. Substantive changes get re-reviewed with you.
