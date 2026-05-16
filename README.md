# Microsoft Style Skill for Claude Code

A Claude Code skill that audits and rewrites technical documentation to align with the [Microsoft Writing Style Guide](https://learn.microsoft.com/style-guide/). Built and maintained by [PowerStacks](https://powerstacks.com) for our own product documentation; published openly because it might help others writing in the Microsoft ecosystem.

## What it does

When invoked, the skill reviews technical content for divergences from Microsoft's published style guidance and either flags or rewrites them. The rule set is optimized for:

- IT-administrator audiences reading technical content at a desk
- Step-by-step installation, configuration, and troubleshooting documentation
- Product and feature docs for software in the Microsoft ecosystem
- API references and admin guides

It is not optimized for marketing copy, blog posts, or mobile-specific content.

## Rules covered

**Highest priority (the procedure rules):**

- Step-by-step instructions — sentence structure, anchor-then-action, verbs for UI interactions
- The full Microsoft input-neutral verb set (`select`, `open`, `close`, `go to`, `select and hold`, `enter`, `clear`, `choose`, `switch / turn on / turn off`, `move / drag`, `zoom`)
- The "don't talk about the UI, talk about what to do" rule
- The comprehensive Elements and Conventions table (buttons, dialogs, menus, panes, tabs, toggles, file names, key combinations, mathematical variables, products, URLs, user input — every element with the right formatting convention)
- Multi-input-method patterns

**Word choice:**

- UI verbs: `click → select`, `tap → select`, `hit → press / select`, `login → sign in`, etc.
- Microsoft product terminology: `Azure AD → Microsoft Entra ID`, `O365 → Microsoft 365`, `MECM → Configuration Manager`, etc.
- Security terminology: `whitelist → allowlist`, `blacklist → blocklist`
- Plain-language replacements: `utilize → use`, `in order to → to`, `simply → (delete)`, etc.
- Anthropomorphism rules: `the app wants → the app needs/requires`
- Direction references: `above → preceding`, `below → following`

**Capitalization:**

- Sentence-style as the default everywhere
- Proper nouns, UI element names matched verbatim
- The narrow set of title-style exceptions

**Bold usage (the rule most technical writers get wrong):**

Microsoft uses bold as a structural signal, not for emphasis. The skill enforces:

- **Use bold for:** UI elements the customer interacts with (buttons, menu items, tab names, checkbox labels, dialog names, form field labels, pane names, palettes, toggles, windows when referenced by name), database names, titles inside body content, keyboard shortcuts (`Ctrl+Alt+Del`), key names (`F5`, `Spacebar`), commands, and user-typed input.
- **Don't use bold for:** emphasis (use italics sparingly instead), entire sentences or paragraphs, "important" callouts (use Note / Tip / Warning admonition blocks), person names, or product names (capitalization handles those).
- **Don't talk about the UI element type** unless clarity demands it. `Select Save` not `Click the Save button`. The label is bold; the type is implied.
- **Match the UI exactly** for the bold label, including punctuation. Drop trailing colons and ellipses (`Select Save as` not `Select Save as…`).

**Italic — sparingly:**

- Emphasis (rarely; usually rewriting is better)
- Mathematical constants and variables (`a² + b² = c²`)
- New terms on first mention if you're going to define them immediately

**Capitalization extras:**

- No ALL CAPS for emphasis. No all-lowercase as a design choice. No internal capitalization (`AutoScale`, `e-Book`) unless it's an established brand name.

**Voice and tone:**

- Second person (`you`)
- Active voice
- Present tense
- Contractions encouraged (`you'll`, `don't`)

**Headings and titles, search writing, punctuation, acronyms** — each gets a section.

## How to install

1. Clone or download this repository.
2. Copy the `SKILL.md` file to your Claude Code skills directory:

    ```bash
    # macOS / Linux
    mkdir -p ~/.claude/skills/microsoft-style
    cp SKILL.md ~/.claude/skills/microsoft-style/SKILL.md
    ```

    ```powershell
    # Windows PowerShell
    New-Item -ItemType Directory -Force -Path "$HOME\.claude\skills\microsoft-style"
    Copy-Item SKILL.md "$HOME\.claude\skills\microsoft-style\SKILL.md"
    ```

3. Restart Claude Code (or start a new session) so it picks up the new skill.

## How to use

Once installed, invoke the skill from any Claude Code session by referencing it in your request. Examples:

- "Apply Microsoft style to this docs page"
- "Run the microsoft-style skill on `installation/getting-started.md`"
- "Use microsoft-style in detect mode on this paragraph" (audits without rewriting)

The skill has two modes:

- **`rewrite`** (default) — produces an audit list and a fixed version of the content with a diff summary
- **`detect`** — produces only the audit list, useful when you want to see what's flagged before deciding what to change

## Pairing with avoid-ai-writing

This skill works well alongside an "avoid AI writing" skill that targets AI-generated patterns (`delve`, `leverage`, em dashes, "It's not X — it's Y" constructions, etc.). Recommended order:

1. Run an avoid-AI-writing pass first to strip AI-isms.
2. Run microsoft-style second to align terminology, formatting, and procedure structure.

The two rule sets overlap modestly (both dislike unnecessary words) but focus on different problems. The combined pass produces tighter, more Microsoft-aligned docs.

## Sources

Every rule in this skill is grounded in Microsoft's publicly published style guidance:

- [Microsoft Writing Style Guide overview](https://learn.microsoft.com/style-guide/)
- [Procedures and instructions checklist](https://learn.microsoft.com/style-guide/checklists/procedures-and-instructions-checklist)
- [Writing step-by-step instructions](https://learn.microsoft.com/style-guide/procedures-instructions/writing-step-by-step-instructions)
- [Describing interactions with the UI](https://learn.microsoft.com/style-guide/procedures-instructions/describing-interactions-with-ui)
- [Formatting text in instructions](https://learn.microsoft.com/style-guide/procedures-instructions/formatting-text-in-instructions)
- [Multiple input methods and branching within procedures](https://learn.microsoft.com/style-guide/procedures-instructions/describing-alternative-input-methods#multiple-input-methods-and-branching-within-procedures)
- [Word choice checklist](https://learn.microsoft.com/style-guide/checklists/word-choice-checklist)
- [A–Z word list and term collections](https://learn.microsoft.com/style-guide/a-z-word-list-term-collections/)
- [Capitalization](https://learn.microsoft.com/style-guide/capitalization)
- [Capitalization checklist](https://learn.microsoft.com/style-guide/checklists/capitalization-checklist)
- [Formatting titles](https://learn.microsoft.com/style-guide/text-formatting/formatting-titles)
- [Formatting common text elements](https://learn.microsoft.com/style-guide/text-formatting/formatting-common-text-elements)
- [Text formatting checklist](https://learn.microsoft.com/style-guide/checklists/text-formatting-checklist)
- [Search writing](https://learn.microsoft.com/style-guide/search-writing)
- [Person (use second-person pronouns)](https://learn.microsoft.com/style-guide/grammar/person)
- [Dashes and hyphens](https://learn.microsoft.com/style-guide/punctuation/dashes-hyphens)
- [Acronyms](https://learn.microsoft.com/style-guide/acronyms)
- [Brand voice: above all, simple and human](https://learn.microsoft.com/style-guide/brand-voice-above-all-simple-human)

## What this is not

- **Not a static linter.** This is a skill for Claude Code — it depends on the language model to apply the rules with judgement. A given paragraph might be rewritten differently across runs depending on context.
- **Not an authoritative Microsoft product.** Microsoft hasn't endorsed or published this skill. It's a community effort to make Microsoft's published style accessible to people writing technical content with Claude Code.
- **Not a replacement for the official style guide.** When the rules here disagree with what Microsoft publishes today, defer to Microsoft. This skill captures a snapshot; the upstream may evolve.

## Contributing

Issues and pull requests are welcome. The skill content lives in [`SKILL.md`](SKILL.md). When proposing changes:

- Cite the specific Microsoft Writing Style Guide URL that supports the change.
- Keep the IT-administrator audience in mind. Don't add rules for mobile, gaming, or marketing copy contexts.
- Preserve the two-mode design (`rewrite` and `detect`).

## License

MIT. See [LICENSE](LICENSE) for full text.

## Maintained by

[PowerStacks](https://powerstacks.com) — Microsoft endpoint management intelligence platform.
