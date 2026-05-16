---
name: microsoft-style
description: Apply Microsoft Writing Style Guide to technical documentation. Use this when reviewing or rewriting PowerStacks docs, install guides, admin guides, API references, or any docs-site content that should align with the Microsoft style customers expect. Optimized for the IT-administrator audience reading technical content at a desk. Not optimized for marketing copy.
---

# Microsoft Writing Style — Audit & Rewrite

You are editing technical documentation to align with the Microsoft Writing Style Guide (https://learn.microsoft.com/style-guide/). PowerStacks publishes its product documentation alongside Microsoft's product documentation; readers expect a consistent voice and terminology between the two. This skill flags and fixes the most common divergences.

## Scope

**Apply this skill to:**

- Technical documentation (`docs.powerstacks.com` content, install guides, admin guides, troubleshooting docs, API references, README files in product repos, in-product help text)
- Step-by-step procedures
- UI references and product terminology

**Do not apply this skill to:**

- Marketing copy on `powerstacks.com` (different voice, different rules — marketing tolerates more personality)
- Blog posts (intentionally have a writer's voice)
- Internal-only documents (Claude memory files, draft notes, internal Slack)
- Mobile-specific content (PowerStacks's audience is at a desk on a computer)

## Modes

**`rewrite`** (default) — Find Microsoft-style violations and rewrite the content to fix them.

**`detect`** — Find violations and report them only; do not rewrite. Use this when:

- The writer wants to see what's flagged and decide what to fix themselves
- You're auditing third-party content that shouldn't be modified
- You want a quick scan without producing a full rewrite

Trigger `detect` mode when the user says "detect," "audit only," "flag only," "scan," "what's wrong with," or similar. Default to `rewrite` mode otherwise.

In **rewrite** mode, your output is:

1. **Audit**: list each violation with the rule it breaks, citing the specific text
2. **Rewrite**: a clean version with all violations fixed
3. **Diff summary**: brief list of what changed and why

In **detect** mode, your output is just the audit list. No rewrite.

This skill is complementary to the `avoid-ai-writing` skill. Run both in sequence on docs: `avoid-ai-writing` first to remove AI patterns, then `microsoft-style` to align terminology and formatting.

---

## 1. Step-by-step instructions — the highest-priority section

Step-by-step instructions are the most common content type in PowerStacks docs and the single biggest source of Microsoft-style divergence. Most rules below apply only to procedure content — heading style and word choice apply elsewhere too.

References:

- <https://learn.microsoft.com/style-guide/checklists/procedures-and-instructions-checklist>
- <https://learn.microsoft.com/style-guide/procedures-instructions/>
- <https://learn.microsoft.com/style-guide/procedures-instructions/writing-step-by-step-instructions>
- <https://learn.microsoft.com/style-guide/procedures-instructions/describing-interactions-with-ui>
- <https://learn.microsoft.com/style-guide/procedures-instructions/formatting-text-in-instructions>
- <https://learn.microsoft.com/style-guide/procedures-instructions/describing-alternative-input-methods#multiple-input-methods-and-branching-within-procedures>

### Procedure structure

- **Use numbered lists** for sequential steps (order matters).
- **Use bulleted lists** for items that don't have a required order.
- **One action per step** where possible. Combine only when actions are tightly bound and happen in the same UI location (`Select Save, then close the dialog.`).
- **Don't overload one procedure with too many steps.** Try to fit all steps on a single screen. Break long procedures into separate procedures with their own headings.
- **Add an introductory step** to anchor the customer if the action could happen in multiple places: `1. Open Settings.` before subsequent steps.
- **Include the completing actions** (selecting **OK**, **Apply**, **Save**) — don't leave the customer wondering whether the action committed.

### Headings for procedures

- Use a heading to introduce each procedure. The heading should concisely describe what the procedure accomplishes.
- **Use parallel structure** across sibling procedure headings: `Create a profile` / `Add an account` / `Delete a profile` — all imperative-verb start.
- If an introductory sentence appears between the heading and the numbered list, make sure the introduction adds information the heading doesn't already convey. Don't restate the heading.

### Single-step procedures

A one-step procedure doesn't necessarily need a numbered list. If you want format consistency with the surrounding multi-step procedures, use a bullet instead of a number — never `1.` alone.

```text
✓ To move a group of tiles:
  - On the Start screen, zoom out and drag the group to where you want it.

✗ To move a group of tiles:
  1. On the Start screen, zoom out and drag the group to where you want it.
```

### Step writing — sentence structure

- **Complete sentences.** Capitalize the first word. End with a period.
- **Anchor before action — high-priority rule.** Make sure the customer knows where the action takes place before you describe the action. This is one of the most-violated rules in technical writing. Microsoft provides two ways to anchor:

    **Pattern A — inline location phrase:** put the location at the start of the sentence, before the verb.

    ```text
    ✓ On the Design tab, select Header row.
    ✓ For Alignment, select Left.
    ✗ Select Header row on the Design tab.
    ✗ Select Left for Alignment.
    ```

    **Pattern B — introductory step:** add a separate step that establishes the location, then the action step follows.

    ```text
    ✓ 1. On the ribbon, go to the Design tab.
      2. Select Header row.
    ```

    Use Pattern B when the location matters enough that splitting it out makes the procedure clearer, or when the same location anchors multiple subsequent steps. Use Pattern A when the location is light and only matters for one step.
- **Imperative verb first** when no location anchor is needed: `Open Photos.` not `You should open Photos.`
- **Match the UI verbatim.** Capitalization, wording, punctuation of UI element names must match what the customer actually sees on screen.
- **Don't include the type of UI element** (button, checkbox, tab, menu, pane, palette) unless the type adds clarity. `Select Save.` not `Select the Save button.`
- **Use sentence-style capitalization for UI element names**, unless the UI uses something different. Match the UI.
- **Drop trailing punctuation from UI labels.** If a label ends in `:` or `…`, omit it in the procedure step. `Select Save as` not `Select Save as…`.

```text
✓ 1. Open Settings.
  2. Select Accounts > Other accounts > Add an account.
  3. Enter your email.
  4. Select Sign in.

✗ 1. First, you can open Settings.
  2. Click on the accounts tab, then click on the other accounts tab, then click on the add an account button.
  3. Type in your e-mail address please.
  4. Hit the Sign-in button.
```

### Verbs for UI interactions — the canonical set

Microsoft uses input-neutral verbs that cover mouse, touch, keyboard, voice, and assistive technologies. Don't use input-specific verbs like `click`, `tap`, or `swipe` in general instructions.

| Verb | Use for | Examples |
|---|---|---|
| **Select** | Buttons, options, checkboxes, list-box values, links, menu items, gallery items, keys, keyboard shortcuts. The default verb for any UI element the customer interacts with. | `Select Save.` `Select the Modify button.` `For Alignment, select Left.` `Select F5.` `Select Ctrl+Alt+Delete.` |
| **Open** | Apps, programs, panes, File Explorer, files, folders, shortcut menus, websites/webpages when needed to match UI. | `Open Photos.` `Open the Reader app.` `Open the document.` `Open the shortcut menu for the item.` |
| **Close** | Apps, programs, panes, dialogs, files, folders, notifications, alerts, tabs. Also the action a program takes when encountering a problem. | `Close Excel.` `Close the pane.` `Save and close the document.` |
| **Leave** | Websites and webpages (when leaving means navigating away). | `Select Submit to complete the survey and leave this page.` |
| **Go to** | Opening a menu. Going to a tab or specific UI place. Going to a website or webpage. | `Go to Search, enter "settings," and then select Settings.` `Go to File, and then select Close.` `On the ribbon, go to the Design tab.` |
| **Select and hold** (or **right-click**) | Pressing and holding an element. OK to use `right-click` alongside `select and hold` when the instruction isn't touch-specific. | `Select and hold (or right-click) the Windows taskbar, and then select Cascade windows.` |
| **>** (greater-than) | Sequential steps along a clear, obvious UI path with the same selection method at each step. Include space before and after. Don't bold the `>`. | `Select Accounts > Other accounts > Add an account.` |
| **Clear** | Clearing a checkbox selection. | `Clear the Header row checkbox.` |
| **Choose** | When the customer picks based on preference or outcome. Also when the verb `Select` would create awkward repetition. | `On the Font tab, choose the effects that you want.` `Choose Select users.` |
| **Switch**, **turn on**, **turn off** | Toggle keys or toggle switches. | `Use the Caps lock key to switch from typing capital letters to typing lowercase letters.` `Turn on the toggle under Turn on high contrast.` |
| **Enter** | Instructing to type or insert a value, including typing or selecting in a combo box. | `In the search box, enter "settings."` `In the Name box, enter a name for this script.` |
| **Move**, **drag** | Moving anything by dragging, cut and paste, or another method. Use for tiles and any open window. | `Drag the file to the folder.` `Move the tile to the new section.` |
| **Move through** | Moving around on a page, through screens, or up/down/right/left in a UI. | `Move through the wizard pages to configure each option.` |
| **Zoom**, **zoom in**, **zoom out** | Changing the magnification of the screen or window. | `Zoom in to see more details on the map.` |
| **Press** | Keyboard keys outside of menu/UI-element contexts where `select` would be wrong. | `Press Enter to submit.` `Press Esc to cancel.` (`Select Enter` is also acceptable in step contexts.) |

### Don't talk about the UI — talk about what to do

For dialog boxes, menus, palettes, panes, tabs, toggles, and windows, **avoid mentioning the UI element type itself**. Describe what the customer needs to do, naming the element by its label in bold only when necessary to disambiguate.

```text
✓ Select Save and continue.
✗ Click the Save and continue button.

✓ In Properties, select Details.
✗ In the Properties dialog box, select the Details tab.

✓ Go to Tools, and select Change language.
✗ On the Tools menu, click the Change language menu item.
```

When you must refer to a specific UI element by name, use **bold** for the name. Use sentence-style capitalization unless the UI uses something different (in which case match the UI). Don't include the type (button, dialog, menu, pane, tab, toggle, window) unless it adds clarity.

### Elements and conventions — the comprehensive table

This is the canonical Microsoft reference for how to format every text element that appears in instructions. Match exactly.

| Element | Convention | Example |
|---|---|---|
| **Buttons, checkboxes, options** | Avoid talking about UI elements; describe what the customer needs to do. When you must name one, use **bold**. Sentence-style capitalization unless matching the UI. Drop trailing colons or ellipses from labels. Don't include the type (button, checkbox) unless clarity demands it. | `Select Save as` (not `Select the Save as button` or `Select Save as…`) `Select Allow row to break across pages.` `Clear the Match case checkbox.` |
| **Command-line commands** | Code style (backticks or code block). | `` `copy` `` |
| **Command-line options (switches/flags)** | Code style. Capitalize as the command must be typed. | `` `/a` `` `` `/Aw` `` |
| **Commands** | **Bold**. Sentence-style capitalization unless matching the UI. Drop trailing colons or ellipses. Don't include the word `command` unless clarity demands it. | `Go to Tools, and select Change language.` `On the Design menu, select Colors, and then select a color scheme.` |
| **Database names** | **Bold** in prose. Code style if part of a code syntax. Capitalization varies. | `WingtipToys database` `Enter the command USE WingtipToys;` |
| **Device and port names** | All uppercase. | `USB` `LPT1` `COM3` |
| **Dialog boxes** | Avoid talking about UI. When needed, refer to the dialog by name in **bold**. Don't use `pop-up window`, `dialog box`, or `dialogue box` — use `dialog`. Sentence-style capitalization unless matching the UI. Drop trailing colons or ellipses. | `Select Upload, and then select a file to upload.` `In Properties, select Details.` `In the Protect document dialog, clear the Shapes checkbox.` |
| **Error messages** | Sentence-style capitalization. Enclose in quotation marks when referring to them in body text. | `Looks like that's a broken link.` `If you see the error message "Check scanner status and try again," use Windows Update to check for the latest drivers.` |
| **File attributes** | All lowercase. | `hidden` `system` `read-only` |
| **File name extensions** | All lowercase. | `.docx` `.pdf` `.intunewin` `.json` |
| **File names (user examples)** | Title-style capitalization. Internal caps OK for readability. **Bold** in procedures if the customer is selecting, typing, or interacting with the name. Code style if part of code syntax. | `My Taxes for 2025` `MyTaxesFor2025` `` Enter `MyTaxesFor2025`. `` |
| **Folder and directory names (user examples)** | Sentence-style capitalization. Internal caps OK for readability. **Bold** in procedures if the customer is interacting with the name. Code style if part of code syntax. | `Vacation and sick pay` `MyFiles\Accounting\Payroll\VacPay` `Select Documents.` |
| **Key names, combinations, sequences** | Capitalize. **Bold** in instructions. No space around the `+` in shortcuts. | `Shift`, `F7` `Ctrl+Alt+Del` `Alt, F, O` `Spacebar` `Select the F1 key.` `To open the Preview tab, select Alt+3.` |
| **Macros** | Usually all uppercase. **Bold** if predefined. Code style if user-defined or in code-related content. | `LOWORD` `MASKROP` |
| **Markup language elements (tags)** | Code style. Capitalization varies. | `<img>` `<input type="text">` |
| **Mathematical constants and variables** | Italic. | `a² + b² = c²` |
| **Menus** | Avoid talking about menus. When needed, refer to the menu by name in **bold**. Sentence-style capitalization unless matching the UI. Don't include the word `menu` unless clarity demands. | `Go to Tools, and select Change language.` `On the Design menu, select Colors, and then select a color scheme.` |
| **New terms** | Italicize the first mention if you're going to define the term immediately in body text. | `Microsoft Exchange consists of both server and client components.` |
| **Palettes** | Avoid talking about palettes. When needed, name in **bold**. Sentence-style capitalization. Don't include `palette` unless clarity demands. | `In Colors, let Windows pull an accent color from your background, or choose your own color.` |
| **Panes** | Avoid talking about panes. When needed, name in **bold**. Don't include `pane` unless clarity demands. | `Select the arrow next to the Styles gallery, select Apply styles, and then select a style to modify.` |
| **Placeholders (in syntax and user input)** | Italic when the placeholder is UI text. Use angle brackets for code placeholders when angle brackets aren't part of the syntax. | `Enter password.` `/v: <version>` |
| **Products, services, apps, trademarks** | Usually title-style capitalization. Check the Microsoft trademark list for trademarked names. | `Microsoft Arc Touch Mouse` `Microsoft Word` `Surface Pro` `Notepad` |
| **Slashes** | When telling customers to enter a slash, spell out the term followed by the symbol in parentheses. | `Enter two backslashes (\\) ....` |
| **Strings** | When referring to strings in code, documents, websites, or UI: sentence-style capitalization unless the string is capitalized differently. Enclose in quotation marks, or use code style if it's a code string. | `Select "Now is the time."` `` Find `font-family:Segoe UI Semibold` in the code. `` |
| **Tabs** | Avoid talking about tabs. When needed, name in **bold**. Sentence-style capitalization unless matching the UI. Don't include `tab` unless clarity demands. | `Select the table, and then select Design > Header row.` `On the Design tab, select Header row.` |
| **Toggles** | Avoid talking about toggles. When needed, name in **bold**. Include `toggle` if it adds clarity. | `To make text and apps easier to see, turn on the toggle under Turn on high contrast.` `Turn on the Pass all filters toggle.` |
| **URLs** | All lowercase for complete URLs. Line-break long URLs before a slash if needed. Don't hyphenate URL line breaks. | `www.microsoft.com` `www.microsoft.com/download` |
| **User input** | Usually lowercase unless case-sensitive. **Bold** or italic depending on the element. Italicize placeholder text inside the input string. | `Enter hello world` `Enter password` |
| **Windows** | Avoid talking about windows. When needed, name in **bold**. Use `window` only as a generic term for an area of the screen — not for a specific dialog box, pane, or other UI element. | `To embed the new object, switch to the source document.` |
| **XML schema elements** | Code style. Often in angle brackets. Capitalization varies. | `ElementType element` `<xml:space>` |

### Multi-input-method procedures

When a procedure needs to support more than one input method (mouse, keyboard, touch, voice), Microsoft offers four patterns. Pick one and stick to it consistently.

1. **Use a table** with a separate column per input method.
2. **Document the primary method**, then add the alternative in parentheses or a follow-up sentence: `To pan, slide one finger in any direction (or drag the mouse pointer, or use the arrow keys).` `To copy the selection, click Copy on the toolbar. You can also press Ctrl+C.`
3. **Use a table comparing whole procedures** (one row per approach) if there are multiple ways to complete the same outcome.
4. **For a single step with an alternative**, separate the alternative into its own paragraph in the step, or use the word `or` between them.

For input-method-specific verbs:

- Touch-only content uses `tap`, `double-tap`, `tap and hold`, `pan`, `flick`, `swipe`. Don't use `tap on` or `double-tap on`. Don't use `touch and hold`.
- Mouse-only content can use `click`, `double-click`, `right-click`. But for general docs that work across input methods, use `select`.
- Keyboard procedures should always be documented for accessibility, even if shown in UI.

---

## 2. Word choice

Word choice is the second-most-common Microsoft-style violation. For words not on this list, check the full Microsoft A-Z list at <https://learn.microsoft.com/style-guide/a-z-word-list-term-collections/>.

### UI actions and verbs

| Replace | With | Notes |
|---|---|---|
| click | **select** | Microsoft uses "select" for all input methods (mouse, touch, keyboard, voice). |
| click on | select | Drop the "on." |
| tap | select | Use "select" even for touch — it covers all input methods. Use `tap` only in touch-specific content. |
| hit (a key, a button) | press / select | Press for keyboard keys; select for UI elements. |
| double-click | double-click | OK to use when literally a double-click is needed; otherwise prefer "select." |
| right-click | right-click | OK alongside `select and hold`. |
| key in | enter / type | "Key in" is dated. |
| login (verb) | **sign in** | "Login" is a noun only. |
| log in / log into | sign in / sign into | Two words for the verb. |
| logout (verb) | **sign out** | "Logout" is a noun only. |
| log out / log off | sign out | |
| logon (verb) | sign in | |
| login screen / page | sign-in screen / page | Hyphenated as an adjective. |

### Microsoft product terminology

| Replace | With | Notes |
|---|---|---|
| Azure AD / Azure Active Directory | **Microsoft Entra ID** | Renamed in 2023. |
| Azure AD Connect | Microsoft Entra Connect | |
| O365 / Office 365 | **Microsoft 365** | |
| AAD | Microsoft Entra ID | Don't abbreviate. |
| MEM / Microsoft Endpoint Manager | Microsoft Intune | |
| MECM | Configuration Manager | The "Microsoft Endpoint" prefix was dropped. |
| OS X / Mac OS | macOS | One word, lowercase m. |
| Powershell / power shell | PowerShell | Capital P, capital S, one word. |
| GitHub / Github | **GitHub** | Capital H. |
| email address (when redundant) | email | "Enter your email" is enough unless context demands disambiguation. |

### Security and access terminology

| Replace | With | Notes |
|---|---|---|
| whitelist / white list | **allowlist** | One word. |
| blacklist / black list | **blocklist** | One word. |
| master / slave | primary / replica, primary / secondary | |
| sanity check | quick check, verify | |
| dummy data | sample data, placeholder data | |
| 2FA | two-factor authentication | Spell out on first use. |

### Plain-language replacements

| Replace | With |
|---|---|
| in order to | to |
| due to the fact that | because |
| at this point in time | now |
| in the event that | if |
| with regard to | about |
| utilize | use |
| leverage (verb) | use |
| facilitate | help, make it easier |
| enable (in marketing sense) | let, allow |
| commence | start, begin |
| terminate | end, stop |
| modify | change |
| prior to | before |
| subsequent to | after |
| simply | (delete) |
| just (as in "just click") | (delete) |
| easily / quickly / smoothly | (delete — adverb without specific meaning) |
| please | (delete — implies optional in instructions) |
| basically | (delete) |
| actually | (delete) |
| obviously | (delete — if it's obvious, you don't need to say so) |

### Anthropomorphism — devices don't have feelings

| Replace | With |
|---|---|
| The app wants to... | The app needs..., requires... |
| The system thinks... | The system reports..., detects... |
| The app sees... | The app receives..., reads... |
| The app understands... | The app processes..., accepts... |
| Smart device | (describe what it actually does) |

### Direction and reference

| Replace | With | Notes |
|---|---|---|
| above (referring to earlier content) | preceding | `See the preceding table`. |
| below (referring to later content) | following | `See the following section`. |
| over / under (numeric ranges) | more than / less than | `More than 100 devices`. |

### Words with multiple meanings or that are dated

| Avoid | Use instead | Why |
|---|---|---|
| since (meaning "because") | because | "Since" should refer to time only. |
| as (meaning "because") | because | Same reason. |
| while (meaning "although") | although | "While" should refer to time only. |
| once (meaning "after") | after | "Once" can read as "one time only." |
| where (meaning "when") | when | "Where" is spatial; "when" is temporal. |

---

## 3. Capitalization

Microsoft uses **sentence-style capitalization** almost everywhere. Reference: <https://learn.microsoft.com/style-guide/capitalization>

### The default rule

In headings, titles, UI labels, standalone phrases, and the beginnings of sentences:

- **Capitalize only the first word** plus any proper nouns.
- **Lowercase everything else.**

```text
✓ Configure email notifications
✗ Configure Email Notifications

✓ Add the production redirect URI
✗ Add The Production Redirect URI

✓ Sign in and verify
✗ Sign In And Verify
```

### Proper nouns

Always capitalize:

- Product names: **Microsoft Intune**, **Microsoft Entra ID**, **PowerShell**, **App Store for Intune**, **BI for Intune**, **Power BI**
- Service names: **Azure SQL Database**, **Application Insights**, **Log Analytics**
- Brand names, place names, person names

### UI element names

Match the UI exactly. If the button label is sentence case in the product, use sentence case. If the label uses title case, use title case.

```text
✓ Select Save and continue.   (UI shows "Save and continue")
✗ Select save and continue.

✓ Navigate to Microsoft Entra ID > Security > Conditional Access.
```

### Title-style capitalization exceptions

Use title-style **only** for:

- Book titles, e-book titles, white papers, reports
- Game titles, event names, webinar titles
- Article titles in citations
- Names of blogs
- Titles of people: **Vice President**, **Director of Marketing**

Title-style rules:

- Capitalize the first and last words.
- Don't capitalize `a`, `an`, `the` unless first word.
- Don't capitalize prepositions of four or fewer letters (`on`, `to`, `in`, `up`, `down`, `of`, `for`) unless first or last.
- Capitalize all verbs, nouns, pronouns, adjectives, adverbs.

### Things to never capitalize

- ALL CAPS for emphasis — use italics sparingly instead.
- all lowercase as a design choice — start sentences with a capital.
- Internal capitalization (AutoScale, e-Book) unless part of an established brand name.
- The spelled-out form of an acronym unless it's a proper noun: `virtual private network (VPN)`, not `Virtual Private Network (VPN)`.

### Slash and hyphen compounds

- In a slash compound, capitalize the word after the slash if the word before is capitalized: `Country/Region`, `Turn on the On/Off toggle.`
- Hyphenated compounds follow standard rules.

---

## 4. Bold usage

Microsoft uses bold for specific structural purposes, not for emphasis. Reference: <https://learn.microsoft.com/style-guide/text-formatting/formatting-common-text-elements>

### Use bold for

- **UI elements that the reader interacts with**: button labels, menu items, tab names, checkbox labels, dialog names, form field labels.
- **Database names** (in prose).
- **Titles** in body content — bold is preferred over italics.
- **Key names and keyboard shortcuts** in instructions: **Shift**, **Ctrl+Alt+Del**.
- **The text the user types** in command examples or input fields (when called out as user input).

```text
✓ Select **Save** and then select **OK**.
✓ In the **Name** field, enter your tenant ID.
✓ On the **Settings** tab, select **Advanced**.
✓ Press **Alt+F4** to close the window.
```

### Don't use bold for

- **Emphasis** — use italics sparingly instead. Bold-for-emphasis dilutes the visual signal that bold = UI element.
- **Entire sentences or paragraphs** — if a whole paragraph is bold, it's not emphasis anymore, it's noise.
- **"Important" callouts** — use admonition blocks (Note, Tip, Warning) for that.
- **Person names**.
- **Product names** — capitalization handles those.

### Italics — sparingly

- Emphasis (rarely — usually you can rewrite to make the point).
- Mathematical constants and variables (`a² + b² = c²`).
- New terms on first mention if you're defining them immediately.

---

## 5. Formatting titles and headings

Reference: <https://learn.microsoft.com/style-guide/text-formatting/formatting-titles>

### Titles

- **Sentence-style casing** for almost all titles. First word capitalized, everything else lowercase except proper nouns.
- **Skip end punctuation** on titles, headings, subheadings, UI titles, and list items of three or fewer words. Save periods for body content.
- **Use bold, not italics**, for titles in body content.

```text
✓ Configure Microsoft Teams Bot
✗ Configure Microsoft Teams Bot.

✓ Sign in and verify
✗ Sign In and Verify.
```

### Headings

- Sentence case. First word capitalized.
- Front-load keywords for scannability.

```text
✓ Grant Microsoft Graph permissions to the App Service
✗ How to give Microsoft Graph permissions for the App Service
```

- Don't end headings with a colon unless the heading literally functions as a label for the content that immediately follows.

### Title-style exceptions

Allowed for book titles, white papers, reports, games, events, webinars, formal long-form names. See section 3 for the rules.

---

## 6. Voice and tone

### Use second person

Address the reader as **you**. Avoid third person (`the user`, `the administrator`) and first person plural (`we configure`).

```text
✓ You can change the admin group from the Settings tab.
✗ The administrator can change the admin group from the Settings tab.
```

### Use active voice

```text
✓ Microsoft Entra ID validates the token.
✗ The token is validated by Microsoft Entra ID.

✓ Select Save to apply your changes.
✗ Your changes will be applied when Save is selected.
```

### Use present tense

```text
✓ The portal validates the token and grants access.
✗ The portal will validate the token and then access will be granted.
```

### Contractions are encouraged

Microsoft embraces common contractions in technical content: **you'll**, **don't**, **can't**, **won't**, **it's**, **that's**, **here's**, **we're**.

```text
✓ You'll see the deploy form open in Azure Portal.
```

Avoid awkward contractions (`wouldn't've`, `mightn't`). Avoid contractions in legal/compliance text and anywhere misreading could mislead.

### Don't tell people what they don't need to do

Microsoft (and PowerStacks) docs prefer describing only what's required. Sentences like `You don't need to do X` or `Don't worry about Y` add noise. Just don't mention X or Y.

This rule is enforced more strictly by the companion `avoid-ai-writing` skill.

References:

- <https://learn.microsoft.com/style-guide/brand-voice-above-all-simple-human>
- <https://learn.microsoft.com/style-guide/grammar/person>

---

## 7. Search writing

For docs that need to surface in search results, structure content for scanners and search engines. Reference: <https://learn.microsoft.com/style-guide/search-writing>

### Title and heading rules

- **Front-load the most important keyword** in titles and headings.
- Use the specific product name, not a pronoun or generic term.
- Keep titles under ~60 characters where possible.

```text
✓ Configure Microsoft Teams Bot for App Store
✗ Setting up your bot

✓ Grant Microsoft Graph permissions to the App Service
✗ Permissions that need granting
```

### First paragraph

- The first paragraph of every page should contain the most important keyword and answer the page's question directly.
- Don't bury the lead with throat-clearing context.

```text
✓ "App Store for Intune is a full-lifecycle application management platform..."
✗ "Welcome to App Store for Intune! In this guide, you'll learn how to..."
```

### Use customer language, not internal terminology

If customers search for `single sign-on`, don't title the page `SSO configuration`. Use the term the customer types.

---

## 8. Formatting common text elements (non-procedure docs)

For content outside step-by-step procedures, the conventions for common text elements are simpler. Reference: <https://learn.microsoft.com/style-guide/text-formatting/formatting-common-text-elements>

| Element | Convention |
|---|---|
| Database names | Bold. Capitalization varies. |
| Error messages | Sentence-style. Quotation marks when referenced in body text. |
| File attributes | All lowercase. |
| File name extensions | All lowercase. |
| File names | Title-style. Internal caps OK. |
| Folder/directory names | Sentence-style. Internal caps OK. |
| Mathematical constants and variables | Italic. |
| New terms (first mention) | Italic when defining immediately. |
| Ports | All uppercase. |
| Products, services, apps, trademarks | Title-style. Match Microsoft trademark list. |
| UI text and strings | Sentence-style. Match the UI exactly. |
| URLs | All lowercase. Don't hyphenate; line-break before slashes. |
| Emphasis | Italic, sparingly. |

For instruction-specific element conventions, see section 1 (Step-by-step instructions).

---

## 9. Punctuation — high-frequency rules

### Em dashes ( — )

Use sparingly. Microsoft style allows them but prefers commas or sentence breaks where possible. The companion `avoid-ai-writing` skill flags em dashes as an AI-pattern signal and recommends replacement. **Defer to that rule** in PowerStacks docs.

When used: closed (no spaces around): `She said—and she meant it—the answer was no.`

### En dashes ( – )

Use only for number or date ranges: `pages 5–12`, `January–March 2026`.

### Hyphens ( - )

Use for compound adjectives before a noun: `multi-factor authentication`, `read-only file`. Microsoft is gradually de-hyphenating common words (`email`, not `e-mail`; `online`, not `on-line`).

### Oxford comma

Use it. `Red, white, and blue.`

### Colons in headings

Avoid unless the heading literally functions as a label.

Reference: <https://learn.microsoft.com/style-guide/punctuation/dashes-hyphens>

---

## 10. Acronyms

- Spell out the full term on first use, with the acronym in parentheses: `multi-factor authentication (MFA)`. Use the acronym afterward.
- Don't capitalize the spelled-out form unless it's a proper noun.
- Avoid acronyms in titles, headings, and the first line of body content unless the acronym is more recognizable than the spelled-out term (`URL`, `HTML`, `API`).
- Microsoft-preferred acronyms not needing spell-out: `URL`, `HTML`, `API`, `MFA`, `SSO`, `VPN`, `OS`.

Reference: <https://learn.microsoft.com/style-guide/acronyms>

---

## Workflow

When invoked:

1. **Read** the content the user provides (or the file they reference).
2. **Audit** against the rules above, in priority order: step-by-step instructions → word choice → capitalization → bold → titles → voice/tone → search → common text elements → punctuation → acronyms.
3. In `rewrite` mode: produce the fixed version plus a brief diff summary of what changed.
4. In `detect` mode: produce only the audit list with each violation cited and the rule it breaks.

If the content already passes all major rules, say so. Don't invent problems.

For anything not covered here, defer to the canonical Microsoft Writing Style Guide: <https://learn.microsoft.com/style-guide/>.

## Pairing with avoid-ai-writing

The `avoid-ai-writing` and `microsoft-style` skills are complementary. Recommended order:

1. Run `avoid-ai-writing` first to strip AI patterns (em dashes, `delve into`, hollow intensifiers, `It's not X — it's Y` constructions).
2. Run `microsoft-style` second to align terminology, capitalization, and formatting.

Some overlap exists (both dislike unnecessary words and indirect phrasing) but the rule sets focus on different problems. The combined pass produces tighter, more Microsoft-aligned docs.
