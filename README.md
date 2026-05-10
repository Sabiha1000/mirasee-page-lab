# Mirasee Page Lab

A copy-to-code agent for the Mirasee design team. Paste your page copy → pick a template → get paste-ready code blocks for Ontraport Pages, plus a live preview and a step-by-step build checklist.

**Built for:** Mirasee page designers who build landing pages in Ontraport's drag-drop editor.

**Built with:** Single-file React app · Anthropic Claude API · No build step · Deploys to GitHub Pages.

---

## What it does

You paste raw copy like this:

```
You're a Little Early!
The AI for Business Growth training hasn't started just yet...

I'm glad you're here! If you're seeing this page, you're a bit early.
The training starts on Tuesday, April 7, at 11am Pacific / 2pm Eastern.
...
```

You pick a template — **Text Landing**, **Video Landing**, or **Text Landing with Form** — set a few options (Wistia ID, Ontraport form ID, countdown timer on/off), and click Generate.

You get:

1. **Live preview** — what the page will look like in Mirasee's blue gradient style
2. **Code snippets** — labeled, copy-pasteable blocks for each Ontraport element (CSS, hero headline, body, video embed, form embed, CTA button, signature row)
3. **Standalone HTML** — a complete `.html` file you can open in a browser to preview or share
4. **Build checklist** — numbered step-by-step instructions for assembling the page in Ontraport

The structuring is done by Claude Sonnet 4.6 — it figures out which line is the headline, which is the subheadline, where the bold/italic emphasis should go, etc. — without changing any wording.

---

## Quick start

### Option 1: Use the live version

If your manager already deployed it, just visit the GitHub Pages URL.

### Option 2: Run it locally

```bash
git clone https://github.com/YOUR_USERNAME/mirasee-page-builder.git
cd mirasee-page-builder
# Open index.html in any modern browser. That's it.
```

No `npm install`, no build step, no server. Just open the file.

### Option 3: Deploy to GitHub Pages

1. Push this repo to GitHub
2. Settings → Pages → Source: Deploy from branch → Branch: `main`, Folder: `/ (root)` → Save
3. Wait ~1 minute. Your URL will be `https://YOUR_USERNAME.github.io/mirasee-page-builder/`

---

## How to use it

1. **Get an Anthropic API key** from [console.anthropic.com](https://console.anthropic.com) → API Keys. Paste it into the bar at the top. The key is stored only in your browser's localStorage — it never goes anywhere else.

2. **Pick a template:**
   - 📄 **Text Landing** — hero + body copy + signature footer (e.g. the "You're a Little Early!" page)
   - 🎬 **Video Landing** — hero + Wistia video + body + CTA + signature
   - 📝 **Text Landing with Form** — text landing with an Ontraport form embedded where you choose

3. **Paste your copy.** Don't worry about formatting — just paste it however you have it. The AI figures out structure.

4. **Set options:**
   - **Countdown timer** (on/off)
   - **Wistia ID** (for video landing) — just the ID, not the full URL
   - **Form ID** + **position** (before / middle / after body) — for the form template

5. **Click Generate.** Output appears on the right with four tabs.

6. **Use the Snippets tab** to copy each block into the matching Ontraport element. The Build Steps tab tells you the order.

---

## Output tabs explained

| Tab | What it's for |
|---|---|
| 👁 Preview | Visual approximation of the final page. Use to sanity-check structure & emphasis. |
| ✂️ Snippets | Labeled code blocks (A, B, C…) to paste into Ontraport elements one-by-one. **This is your main workflow.** |
| 📄 Standalone HTML | A complete HTML file. Open in a new tab, download, or copy. **Not for pasting into Ontraport** — share with stakeholders or use as a backup reference. |
| ✅ Build Steps | Numbered step-by-step instructions for building this specific page in Ontraport. |

---

## Why it works this way (and not as full-page HTML)

Ontraport Pages is a drag-drop visual builder, not a raw-HTML editor. You can't usually paste a full page HTML and have it render correctly — Ontraport wraps everything in its own structure.

So instead of generating one massive paste-ready HTML, this tool generates the actual things you'll paste into Ontraport:
- The CSS goes into the Custom CSS panel
- The body copy goes into a Text element (Source/HTML mode)
- The video embed goes into an HTML element
- The form goes into the native Form element (or HTML element with the script embed)
- The CTA goes into a Button element

This matches the real Ontraport workflow and produces output you can actually use.

---

## Privacy & cost

- **Privacy:** Your API key and copy stay in your browser. They're sent directly to Anthropic's API (not through any intermediate server). The repo has no backend.
- **Cost:** Each generation costs roughly $0.01–$0.03 in API usage (Claude Sonnet 4.6, ~2k token responses). One designer making 20 pages a month → under $1/month.

---

## Customizing for your team

The CSS in the tool is hardcoded from the Mirasee styles you provided. To update it:

1. Open `index.html`
2. Find the `MIRASEE_CSS` constant near the top of the `<script type="module">` block
3. Replace the CSS string with the updated styles
4. Commit and push — GitHub Pages redeploys automatically

The system prompt that tells Claude how to structure copy is in the `buildSystemPrompt()` function in the same file. You can tweak the rules (e.g., add Mirasee-specific terminology, add new emphasis rules, change voice guidelines) by editing that prompt.

---

## Adding new templates later

To add a new template (say, "Sales Page" or "Thank You Page"):

1. In `index.html`, find the `TEMPLATES` constant.
2. Add a new entry with `name`, `description`, `icon`, `hasVideo`, `hasForm`, and any other flags you need.
3. Update `buildSystemPrompt()` to handle the new fields the AI should output.
4. Update the rendering logic in `PreviewTab`, `SnippetsTab`, and `ChecklistTab` for any new sections.

---

## Stack

- **React 18** loaded via ESM from esm.sh — no build step
- **Tailwind CSS** loaded via CDN
- **Google Fonts** (Fraunces for display, Inter for body, JetBrains Mono for code)
- **Anthropic Messages API** with `anthropic-dangerous-direct-browser-access: true` (browser-direct; key stays client-side)
- **Model:** `claude-sonnet-4-6`

No package.json, no node_modules, no build pipeline. Just one HTML file.

---

## Built by

The Mirasee page design team, with help from Claude.
