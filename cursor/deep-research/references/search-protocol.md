# Search protocol

## Each lane, wave 1

Run **at least three** distinct queries. Then open **two to four** URLs that actually argue the point. Snippets are leads, not findings.

Query shapes that usually differ:

1. The subject in the user's words, plus the lane's angle
2. A synonym, a product name, or a `site:` on an official or standards host
3. The opposite or the failure: "does not", "vs", "postmortem", "limitations", a year

Do not fire the same five words three times. Do not stop at the first blog.

Prefer, in order: official docs and primary data, then journalism or papers, then community writeups. A forum thread can be a practice finding. It cannot be the sole core finding.

## Thin lane → one rewrite

Thin means fewer than two opened URLs, or every URL is one domain saying the same thing.

Rewrite by changing the *question*, not the adjectives:

- Swap the product name for the category, or the category for a named product
- Add a year, a region, or a standards body
- Search the critique terms if wave 1 only found vendors
- Search the vendor docs if wave 1 only found Twitter

Relaunch that lane once. If it is still thin, return `insufficient evidence` for that angle. The chair does not invent a paragraph to keep the report symmetric.

## Output contract (every lane)

```text
Lane: ...
Queries I ran: (the actual strings)
Opened: URL — one-line what I took from it
Findings:
- Claim
  Source: URL
  Kind: official | academic | journalism | community | other
  As of: date on the page, or unknown
Conflicts I saw: ...
Gaps: what I could not open or could not verify
```

No finding without a URL in `Opened`. If the fetch failed, say failed; do not quote the title as if you read it.

## Chair after the wave

- Collapse duplicate claims that share a URL
- Keep disagreements. Do not vote them away
- Fill at most one missing hole yourself if a single search would do it
- Do not start a third wave
