# Leave alone

Mask these before you scan or rewrite. Restore them verbatim.

## Never edit

- Fenced code blocks and indented code
- Inline code (`like_this`)
- Shell commands and their flags (`npx skills add`, `--agent cursor`)
- YAML / TOML / JSON / frontmatter
- Tables whose cells are commands, paths, or values
- URLs, emails, file paths, object keys
- Numbers, dates, versions, commit SHAs
- Skill names, product names, CLI names, model names
- Link targets: change visible link text only when the surrounding prose needs it; never change the destination
- Quoted third-party text (quotation marks, block quotes)
- License text and copyright lines

## Usually leave

- Heading slugs that would break existing links, unless the user asked to retitle
- Korean technical 한자어 that is the actual term of art, not decoration
- English words that are the conventional name in Korean prose (`Cursor`, `README`, `frontmatter`)

## Not a tell by itself

- One em dash in English when a writing sample uses dashes
- A three-item list that the content actually needs
- Formal 합니다-체 in a spec or API guide
- A comma in Korean that grammar requires

Density is the signal. One instance is not a rewrite trigger.

## After the rewrite

Unmask. Diff the protected spans against the source. If any of them moved, put them back and rewrite the sentence around them instead.
