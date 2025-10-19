# 📊 MINTLIFY VISUAL REFERENCE GUIDE

## 1. Complete System Diagram

```
YOUR LOCAL MACHINE                  GITHUB REPOSITORY
├── .mdx files      ──git push──>   ├── .mdx files
├── mint.json                       ├── mint.json
├── /images                         └── /images
└── /logo

        ↓ mintlify dev                  ↓ GitHub App webhook
        
Dev Preview (localhost:3000)     Mintlify Build (Automated)

        └──────────────┬──────────────┘
                       ↓
                Next.js Build
                       ↓
            Static HTML + React Components
                       ↓
                CDN Distribution
                       ↓
        PUBLIC WEBSITE (docs.brainbox.com)
```

---

## 2. File Structure Flow

```
brainbox-docs/ (Project Root)
│
├── mint.json
│   └─ Controls: Site name, colors, nav, versions, features
│
├── README.md
│   └─ Project documentation
│
├── Root Pages (Accessible if in mint.json nav)
│   ├── introduction.mdx      → URL: /introduction
│   ├── quickstart.mdx        → URL: /quickstart
│   └── development.mdx       → URL: /development
│
├── en/ (English Version)
│   └── introduction.mdx      → URL: /en/introduction
│
├── es/ (Spanish Version)
│   └── introduction.mdx      → URL: /es/introduction
│
├── essentials/ (Guide Content)
│   ├── code.mdx              → URL: /essentials/code
│   ├── markdown.mdx          → URL: /essentials/markdown
│   ├── images.mdx            → URL: /essentials/images
│   ├── navigation.mdx        → URL: /essentials/navigation
│   ├── settings.mdx          → URL: /essentials/settings
│   └── reusable-snippets.mdx → URL: /essentials/reusable-snippets
│
├── snippets/ (NOT PUBLIC)
│   └── snippet-intro.mdx     → Import only, not accessible
│
├── logo/
│   ├── dark.svg
│   └── light.svg
│
└── images/
    ├── checks-passed.png
    ├── hero-dark.svg
    ├── hero-light.svg
    └── Introduccion.png
```

---

## 3. MDX Document Structure

```
example-page.mdx

FRONT MATTER (YAML)
---
title: "Page Title"         ← Page title in browser
description: "Page desc"    ← SEO & preview
icon: "pen-to-square"       ← Sidebar icon
---

MARKDOWN CONTENT

# Main Heading              ← Creates anchor + TOC
## Subheading               ← Creates anchor + TOC

**Bold text** here          ← Styling
_italic text_ here

[Link](/page)               ← Navigation
![Alt](/image.png)          ← Images

```javascript
const hello = "world";      ← Code blocks
```                              with syntax highlight

REACT COMPONENTS

<Card
  title="..."               ← Interactive elements
  href="..."
>
  Text
</Card>

<Tip>
  Important info            ← Callout boxes
</Tip>
```

---

## 4. mint.json Configuration Map

```
mint.json Structure

BRANDING
├── name
├── logo              → Website appearance
├── favicon
├── colors
└── font

NAVIGATION
├── topbarLinks
├── topbarCtaButton   → Header & menu
├── anchors
└── navigation

INTERNATIONALIZATION
└── versions (en, es, etc.)  → Language support

ENGAGEMENT
├── feedback
├── search            → User features
└── footerSocials

API DOCS
├── openapi
├── api.baseUrl       → API documentation
└── api.auth
```

---

## 5. Website Layout Map

```
TOP BAR
[LOGO] Documentation    [Support] [🌐 English ▼] [Get Started]

MAIN CONTENT AREA
├── SIDEBAR NAV (from mint.json)
│   ├── 📄 Get Started
│   │   ├─ Quickstart
│   │   └─ Setup
│   ├── 📚 Guides
│   │   ├─ Markdown
│   │   ├─ Code
│   │   └─ Images
│   ├── 🔗 Blog
│   └── [🔍 Search...]
│
├── MAIN CONTENT (from .mdx)
│   ├── ## Main Title
│   ├── Lorem ipsum...
│   ├── ### Subtitle
│   ├── Content here
│   ├── <Card/>
│   ├── <Tip/>
│   └── More content...
│
└── RIGHT TOC (auto generated)
    ├── On this page
    ├── • Main Title
    ├── • Subtitle
    ├── • Sub-sub
    ├── ✏️ Edit this
    └── 🐛 Report

FOOTER
© 2024 BrainBox    [🐦 Twitter] [💼 LinkedIn]
[Privacy] [Terms]
```

---

## 6. Navigation Configuration Visual

```
mint.json Navigation Array:

"navigation": [
  {
    "group": "Get Started",
    "version": "English",
    "pages": [
      "en/introduction",
      "en/quickstart",
      {
        "group": "Advanced",
        "pages": [
          "en/advanced/setup",
          "en/advanced/deploy"
        ]
      }
    ]
  }
]

↓ Renders as Sidebar ↓

┌─ Get Started
│  ├─ Introduction
│  ├─ Quickstart
│  └─ Advanced
│     ├─ Setup
│     └─ Deploy
```

---

## 7. Language Switching Flow

```
User visits docs.brainbox.com

    ↓ Default locale (English) ↓

Redirects to: /en/introduction

    ↓ User clicks language selector ↓

┌────────────────────────────────┐
│ Select Language:               │
│  ☑ English    (current)        │
│  ☐ Español                     │
└────────────────────────────────┘

    ↓ User selects Spanish ↓

Navigates to: /es/introduction

    ↓ Sidebar updates ↓

Shows Spanish navigation:
├─ Bienvenida (instead of Welcome)
├─ Inicio Rápido (instead of Quick Start)
└─ etc...
```

---

## 8. Development Workflow Timeline

```
Time    Action                          Result
────    ────────────────────────────    ─────────────────────────
T0      npm install -g mintlify        ✓ CLI installed
        
T1      cd brainbox-docs               ✓ In project directory
        mintlify dev                   ✓ Dev server starting
        
T2      Browser: localhost:3000        ✓ Local preview loads
        
T3      Edit en/introduction.mdx       ✓ File saved
        
T4      (automatic reload)             ✓ Browser updates (2-3s)
        
T5      Fix looks good                 
        
T6      git add .
        git commit -m "Update docs"
        git push                       ✓ Pushed to GitHub
        
T7      GitHub webhook triggers        ✓ Mintlify build starts
        
T8      Build & compile                ✓ Next.js compiling
        
T9      Deploy to CDN                  ✓ Live on production
        
T10     docs.brainbox.com updates      ✓ Users see changes

Total Time: ~1-3 minutes from push to production
```

---

## 9. Component Quick Reference

```
COMPONENT FAMILIES

🎨 CONTENT DISPLAY
├── <Card> / <CardGroup>       Info cards
├── <Accordion> / <AccordionGroup> Expandable sections
└── <Tabs> / <Tab>             Tabbed content

⚠️ CALLOUT BOXES
├── <Info>                     Gray info box
├── <Tip>                      Green tip box
├── <Note>                     Blue note box
└── <Warning>                  Red warning box

📋 STRUCTURED DATA
├── <Steps> / <Step>           Numbered procedures
├── <ResponseField>            API parameters
└── <CodeGroup>                Multi-language code

📦 CONTAINERS
├── <Frame>                    Image/content wrapper
├── <Expandable>               Expandable section
└── <Latex>                    Math formulas
```

---

## 10. Color System Application

```
mint.json Colors:

"colors": {
  "primary": "#2E2E2E",        ← Dark gray
  "light": "#454545",          ← Lighter gray
  "dark": "#2E2E2E",           ← Dark gray (buttons)
  "anchors": {
    "from": "#2E2E2E",
    "to": "#454545"
  }
}

Applied to Website Elements:

Links:           [#2E2E2E underline]
Active sidebar:  [#454545 background]
CTA button:      [#2E2E2E background]
Tip box border:  [#2E2E2E left edge]
Anchor links:    [#2E2E2E→#454545]
Code highlights: [#2E2E2E accents]
Hover states:    [#454545 highlight]
```

---

## 11. Page Accessibility vs Visibility

```
File: en/my-page.mdx

In mint.json navigation? NO  →  Hidden from sidebar

Still accessible via:
✅ Direct URL: /en/my-page
✅ Search bar: Search for content
✅ Internal links: [Link text](/en/my-page)
❌ NOT in sidebar menu

Use case: Drafts, utilities, API ref pages
```

---

## 12. Deployment Status Indicators

```
GitHub Commit:
"Update documentation"

Status Indicators:

✅ Green checkmark = Deployment successful
   Changes live on docs site (1-2 min)

❌ Red X = Deployment failed
   Check Mintlify dashboard for errors
   Common issues:
   ├─ Invalid JSON in mint.json
   ├─ Broken MDX syntax
   ├─ Missing image files
   └─ Page reference errors

⏳ Yellow circle = Building
   Mintlify is compiling your changes
```

---

## 13. Content Update Path

```
You want to update content

    ↓

Edit .mdx file in text editor

    ↓

Save file

    ↓

➜ IF using mintlify dev (local):
  ├─ Dev server detects change
  ├─ Hot-reloads in browser (2-3s)
  └─ You see changes immediately

    ↓

Verify changes look good

    ↓

git add .
git commit -m "Update content"
git push

    ↓

➜ IF GitHub App installed:
  ├─ Webhook triggered automatically
  ├─ Mintlify servers build docs
  ├─ Changes deployed to CDN
  └─ docs.brainbox.com updates

    ↓ DONE ↓

All users see updated docs
```

---

## 14. Quick Command Reference

```
ESSENTIAL MINTLIFY COMMANDS

Installation:
npm install -g mintlify
npm install -g mintlify@latest    (update)
npm remove -g mintlify            (uninstall)

Development:
mintlify dev                      (start local)
mintlify dev --port 3333          (custom port)
Ctrl+C                            (stop server)

Validation:
mintlify broken-links             (check links)
mintlify install                  (reinstall deps)

Build & Deploy:
(automatic via GitHub)
(manual via dashboard)
```

---

## 15. Troubleshooting Decision Tree

```
Problem?
  ↓
  ├─ Local dev not working?
  │  ├─ Port in use? → Use --port flag
  │  └─ Works
  │
  ├─ Build fails in production?
  │  ├─ Invalid JSON in mint.json? → Fix JSON syntax
  │  └─ Works
  │
  └─ Content issues?
     ├─ Broken links in navigation? → Check mint.json
     ├─ Page not showing? → Add to mint.json
     └─ Works

Commit and push
  ↓
Wait 1-2 minutes
  ↓
Check docs site
  ↓
DONE!
```

---

**Use this visual guide alongside the deep research document for complete understanding of Mintlify!**

