# 🔧 MINTLIFY PRACTICAL EXAMPLES & USE CASES

## Table of Contents
1. [Creating a New Page](#creating-a-new-page)
2. [MDX Content Examples](#mdx-content-examples)
3. [Navigation Patterns](#navigation-patterns)
4. [Component Usage Examples](#component-usage-examples)
5. [Real-World Scenarios](#real-world-scenarios)
6. [Common Issues & Solutions](#common-issues--solutions)

---

## Creating a New Page

### Scenario 1: Add a Simple English Page

**Step 1: Create the file**
```bash
# Create a new page in the en folder
touch en/installation.mdx
```

**Step 2: Add content**
```mdx
---
title: 'Installation'
description: 'How to install and set up BrainBox'
icon: 'download'
---

# Installation Guide

## System Requirements

- Windows 10+ or macOS 10.15+
- 2GB RAM minimum
- 100MB disk space

## Download

Visit [brainbox.com.co](https://brainbox.com.co) and click "Download".

## Setup Wizard

After downloading:

<Steps>
  <Step title="Open the installer">
    Double-click the downloaded file
  </Step>
  <Step title="Accept terms">
    Read and accept the license agreement
  </Step>
  <Step title="Choose location">
    Select where to install (default is fine)
  </Step>
  <Step title="Complete setup">
    Click "Finish" and wait 2-3 minutes
  </Step>
</Steps>

## Verify Installation

```bash
brainbox --version
```

<Tip>
  If you see a version number, installation was successful!
</Tip>
```

**Step 3: Add to navigation in mint.json**
```json
{
  "navigation": [
    {
      "group": "Get Started",
      "version": "English",
      "pages": [
        "en/introduction",
        "en/installation"    // ← Add this line
      ]
    }
  ]
}
```

**Step 4: Test locally**
```bash
cd brainbox-docs
mintlify dev
# Visit http://localhost:3000/en/installation
```

**Step 5: Deploy**
```bash
git add en/installation.mdx mint.json
git commit -m "Add installation guide"
git push
# Deployed in 1-2 minutes!
```

---

### Scenario 2: Create Parallel Spanish Translation

**Same file structure, different language**

```bash
# Create Spanish equivalent
touch es/instalacion.mdx
```

**Content (translated):**
```mdx
---
title: 'Instalación'
description: 'Cómo instalar y configurar BrainBox'
icon: 'download'
---

# Guía de Instalación

## Requisitos del Sistema

- Windows 10+ o macOS 10.15+
- 2GB de RAM mínimo
- 100MB espacio en disco

# ... rest of translation ...
```

**Update mint.json:**
```json
{
  "navigation": [
    {
      "group": "Get Started",
      "version": "English",
      "pages": [
        "en/introduction",
        "en/installation"
      ]
    },
    {
      "group": "Empezar",
      "version": "Español",
      "pages": [
        "es/introduction",
        "es/instalacion"        // ← Add Spanish equivalent
      ]
    }
  ]
}
```

---

## MDX Content Examples

### Example 1: Complete Feature Documentation Page

```mdx
---
title: 'Document Analysis'
description: 'Understand how BrainBox analyzes your documents'
icon: 'magnifying-glass'
---

# How Document Analysis Works

BrainBox uses advanced AI to extract meaning from your documents.

## The Process

<Steps>
  <Step title="Document Upload">
    You upload a PDF or document file (up to 200MB)
  </Step>
  <Step title="Text Extraction">
    Our system extracts all text and preserves formatting
  </Step>
  <Step title="AI Analysis">
    Machine learning models understand content and context
  </Step>
  <Step title="Index Creation">
    A searchable index is created for fast queries
  </Step>
</Steps>

## Supported Formats

| Format | Status | Notes |
|--------|--------|-------|
| PDF | ✅ Supported | Best performance |
| DOCX | ✅ Supported | Full text extraction |
| TXT | ✅ Supported | Plain text files |
| PPT | ⏳ Coming | Q2 2024 |
| XLS | ⏳ Coming | Q2 2024 |

## Performance

<CardGroup cols={2}>
  <Card title="Speed" icon="zap">
    Analyzes 200MB files in under 30 seconds
  </Card>
  <Card title="Accuracy" icon="bullseye">
    98.5% content extraction accuracy
  </Card>
  <Card title="Scale" icon="server">
    Processes 1000+ documents simultaneously
  </Card>
  <Card title="Cost" icon="money-bill">
    Pay per document analyzed
  </Card>
</CardGroup>

## Advanced Features

<Accordion title="Custom Extraction Rules">
You can define custom extraction patterns:

```json
{
  "patterns": [
    {
      "name": "invoice_number",
      "regex": "INV-\\d{6}",
      "type": "string"
    }
  ]
}
```
</Accordion>

<Accordion title="Metadata Preservation">
BrainBox preserves:
- Author information
- Creation date
- Document properties
- Embedded images and graphics
</Accordion>

## Tips for Best Results

<Tip>
  Upload high-quality scans (300 DPI) for OCR documents
</Tip>

<Warning>
  Encrypted PDFs require password entry before upload
</Warning>

<Note>
  All documents are encrypted and stored securely
</Note>

---

## See Also

- [Upload Documents](/en/upload)
- [Search Your Documents](/en/search)
- [API Reference](/api/analyze)
```

### Example 2: Troubleshooting Guide

```mdx
---
title: 'Troubleshooting'
description: 'Solutions to common BrainBox issues'
icon: 'wrench'
---

# Troubleshooting Guide

## Common Issues

### Issue: Upload Fails

**Problem**: File upload returns error "File too large"

**Solution**:
<AccordionGroup>
  <Accordion title="Check file size">
    BrainBox supports files up to 200MB each. If your file is larger:

    1. Split the document into smaller parts
    2. Or upgrade to Enterprise plan (1GB limit)
  </Accordion>
  
  <Accordion title="Verify file format">
    Supported formats: PDF, DOCX, TXT

    If different format:
    ```bash
    # Convert using free tools:
    # PDF → DOCX: Use ilovepdf.com
    # DOC → DOCX: Microsoft Word
    ```
  </Accordion>

  <Accordion title="Check internet connection">
    Slow/unstable connection may timeout. Try:
    - Refresh page
    - Use wired internet instead of WiFi
    - Close other bandwidth-heavy apps
  </Accordion>
</AccordionGroup>

### Issue: Can't Find Information in Search

**Problem**: Search doesn't return expected results

**Solution**:
- **Try different keywords**: "Invoice" vs "Bill" 
- **Search with quotes**: `"exact phrase"` for exact matches
- **Check document processing**: Wait 2-3 minutes after upload
- **Verify in source**: Manually check PDF to confirm info exists

### Issue: Slow Performance

**Problem**: Document analysis takes longer than expected

**Root Causes**:
| Issue | Fix | Time |
|-------|-----|------|
| Large file (>100MB) | Split into smaller files | Immediate |
| Complex formatting | Convert to plain text | Immediate |
| System overload | Try again in 1 hour | N/A |
| Server maintenance | Check status page | Varies |

---

## Performance Tips

<Tip>
  **Pro Tip**: Process documents during off-peak hours (2-5 AM UTC) for faster analysis
</Tip>

## Still Having Issues?

<Card 
  title="Contact Support"
  icon="headset"
  href="mailto:support@brainbox.com.co"
>
  Email us at support@brainbox.com.co for 24/7 help
</Card>
```

### Example 3: API Documentation Page

```mdx
---
title: 'API Reference'
description: 'BrainBox API endpoints'
icon: 'code'
---

# API Reference

## Authentication

All API requests require a Bearer token:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://api.brainbox.com/v1/documents
```

## List Documents

Retrieve all documents in a box.

**Endpoint**
```
GET /api/v1/boxes/{boxId}/documents
```

**Parameters**

<ResponseField name="boxId" type="string" required>
  The unique identifier of the box
</ResponseField>

<ResponseField name="limit" type="number" default={10}>
  Number of documents to return (1-100)
</ResponseField>

<ResponseField name="offset" type="number" default={0}>
  Pagination offset
</ResponseField>

**Response**

```json
{
  "documents": [
    {
      "id": "doc_123",
      "name": "Q4 Report.pdf",
      "uploadedAt": "2024-01-15T10:30:00Z",
      "size": 2048576,
      "status": "processed"
    }
  ],
  "total": 42,
  "hasMore": true
}
```

**Example Request**

<CodeGroup>
```bash cURL
curl -X GET "https://api.brainbox.com/v1/boxes/box_456/documents?limit=5" \
  -H "Authorization: Bearer sk_live_abc123"
```

```python Python
import requests

headers = {
    "Authorization": "Bearer sk_live_abc123"
}

response = requests.get(
    "https://api.brainbox.com/v1/boxes/box_456/documents",
    headers=headers,
    params={"limit": 5}
)

print(response.json())
```

```javascript JavaScript
const response = await fetch(
  'https://api.brainbox.com/v1/boxes/box_456/documents?limit=5',
  {
    headers: {
      'Authorization': 'Bearer sk_live_abc123'
    }
  }
);

const data = await response.json();
console.log(data);
```
</CodeGroup>
```

---

## Navigation Patterns

### Pattern 1: Linear Documentation

**Use Case**: Simple product with straightforward flow

```json
{
  "navigation": [
    {
      "group": "Getting Started",
      "pages": ["introduction", "quickstart"]
    },
    {
      "group": "Guides",
      "pages": ["guides/setup", "guides/usage"]
    },
    {
      "group": "Reference",
      "pages": ["reference/api", "reference/faq"]
    }
  ]
}
```

**Results in:**
```
Getting Started
├── Introduction
└── Quickstart

Guides
├── Setup
└── Usage

Reference
├── API
└── FAQ
```

### Pattern 2: Nested/Hierarchical

**Use Case**: Complex product with many topics

```json
{
  "navigation": [
    {
      "group": "Core Concepts",
      "pages": [
        "concepts/overview",
        {
          "group": "Advanced",
          "pages": [
            "concepts/advanced/ai-models",
            "concepts/advanced/security",
            "concepts/advanced/scaling"
          ]
        }
      ]
    },
    {
      "group": "How To",
      "pages": [
        {
          "group": "Documents",
          "pages": [
            "guides/upload-documents",
            "guides/organize-documents",
            "guides/share-documents"
          ]
        },
        {
          "group": "Analysis",
          "pages": [
            "guides/analyze",
            "guides/extract-data",
            "guides/generate-reports"
          ]
        }
      ]
    }
  ]
}
```

**Results in:**
```
Core Concepts
├── Overview
└── Advanced
   ├── AI Models
   ├── Security
   └── Scaling

How To
├── Documents
│  ├── Upload
│  ├── Organize
│  └── Share
└── Analysis
   ├── Analyze
   ├── Extract Data
   └── Generate Reports
```

### Pattern 3: Version-Specific with Shared Content

**Use Case**: Multi-language or versioned docs

```json
{
  "navigation": [
    {
      "group": "Get Started",
      "version": "English",
      "pages": [
        "en/introduction",
        "en/quickstart"
      ]
    },
    {
      "group": "Empezar",
      "version": "Español",
      "pages": [
        "es/introduction",
        "es/quickstart"
      ]
    }
  ]
}
```

---

## Component Usage Examples

### Example 1: Multi-Step Onboarding

```mdx
# Get Started in 3 Steps

<Steps>
  <Step title="Create Your Box" icon="folder">
    A Box is your workspace. Click "Create Box" and give it a name.
  </Step>
  
  <Step title="Upload Documents" icon="upload">
    Drag and drop PDFs or click to browse. Up to 200MB per file.
  </Step>
  
  <Step title="Start Asking Questions" icon="message">
    Type your question and get instant answers with source references.
  </Step>
</Steps>
```

### Example 2: Feature Comparison Card Grid

```mdx
# Our Plans

<CardGroup cols={3}>
  <Card title="Free" icon="star" href="/pricing/free">
    Perfect for testing
    
    ✅ 5 Boxes
    ✅ 100MB total storage
    ✅ Basic support
    ❌ No API access
  </Card>
  
  <Card title="Pro" icon="rocket" href="/pricing/pro">
    For active users
    
    ✅ 50 Boxes
    ✅ 50GB storage
    ✅ Priority support
    ✅ API access
  </Card>
  
  <Card title="Enterprise" icon="crown" href="/pricing/enterprise">
    For organizations
    
    ✅ Unlimited Boxes
    ✅ Unlimited storage
    ✅ 24/7 support
    ✅ SSO & advanced admin
  </Card>
</CardGroup>
```

### Example 3: Tips & Warnings

```mdx
## Best Practices

<Tip>
  Upload documents in a logical order. This helps with search relevance.
</Tip>

<Warning>
  Do not upload documents containing personal information without consent.
  All documents are encrypted but privacy is important.
</Warning>

<Note>
  Document processing typically takes 30 seconds to 2 minutes depending on size and complexity.
</Note>

<Info>
  You can manage permissions for shared Boxes from the settings page.
</Info>
```

### Example 4: Tabbed Code Examples

```mdx
## API Authentication

<CodeGroup>
  ```bash cURL
  curl -H "Authorization: Bearer YOUR_KEY" \
    https://api.brainbox.com/v1/documents
  ```

  ```python Python
  import requests
  
  headers = {"Authorization": "Bearer YOUR_KEY"}
  requests.get("https://api.brainbox.com/v1/documents", 
               headers=headers)
  ```

  ```javascript JavaScript
  const response = await fetch(
    'https://api.brainbox.com/v1/documents',
    { headers: { Authorization: 'Bearer YOUR_KEY' } }
  );
  ```

  ```go Go
  req, _ := http.NewRequest("GET", 
    "https://api.brainbox.com/v1/documents", nil)
  req.Header.Add("Authorization", "Bearer YOUR_KEY")
  client.Do(req)
  ```
</CodeGroup>
```

---

## Real-World Scenarios

### Scenario 1: Your Product Gets a Major Update

**Situation**: You release BrainBox 2.0 with major changes

**Solution**: Create version 2.0 docs

```bash
# Create new version folder
mkdir docs-v2.0
cp -r en/ docs-v2.0/en
cp -r es/ docs-v2.0/es

# Create migration guide
touch en/migrating-from-v1.mdx
```

**Update mint.json:**
```json
{
  "versions": [
    {
      "name": "v2.0 (Latest)",
      "locale": "v2.0",
      "default": true
    },
    {
      "name": "v1.9 (Legacy)",
      "locale": "v1.9"
    }
  ],
  "navigation": [
    {
      "group": "Getting Started",
      "version": "v2.0 (Latest)",
      "pages": [
        "docs-v2.0/en/introduction",
        "en/migrating-from-v1"
      ]
    },
    {
      "group": "Getting Started",
      "version": "v1.9 (Legacy)",
      "pages": ["v1.9/en/introduction"]
    }
  ]
}
```

### Scenario 2: Add Product Blog Link

**Situation**: You want to link to your blog from docs

**Solution**: Add anchor in mint.json

```json
{
  "anchors": [
    {
      "name": "Blog",
      "icon": "newspaper",
      "url": "https://blog.brainbox.com.co",
      "color": "#2E2E2E"
    },
    {
      "name": "Community",
      "icon": "slack",
      "url": "https://slack.brainbox.com.co",
      "color": "#E91E63"
    }
  ]
}
```

**Results in**: Two clickable icons in left sidebar

### Scenario 3: Redirect Old Documentation Links

**Situation**: You moved a page from `/guides/upload` to `/uploading-documents`

**Solution**: Create redirect page

```mdx
---
title: 'Upload Guide (Moved)'
description: 'This page has been moved'
---

<Info>
This page has been moved. You are being redirected...
</Info>

<script>
  window.location.href = '/uploading-documents';
</script>

If you are not redirected automatically, [click here](/uploading-documents).
```

---

## Common Issues & Solutions

### Issue 1: Sidebar Menu Not Updating

**Problem**: Added new page but doesn't appear in sidebar

**Diagnosis Checklist**:
1. ✅ File created? (`en/new-page.mdx` exists)
2. ✅ Has front matter? (YAML section at top)
3. ✅ Added to mint.json? (In navigation array)
4. ✅ Dev server restarted? (Kill and restart `mintlify dev`)

**Solution**:
```json
{
  "navigation": [
    {
      "group": "Category",
      "pages": [
        "en/existing-page",
        "en/new-page"
      ]
    }
  ]
}
```

### Issue 2: Broken Internal Links

**Problem**: Links work locally but fail on production

**Solution**: Use root-relative paths

```mdx
❌ BAD (relative path - slow):
[Link to guide](../guides/setup)

✅ GOOD (root-relative - fast):
[Link to guide](/en/guides/setup)

❌ BAD (external reference):
[Link to guide](https://docs.brainbox.com/en/guides/setup)

✅ GOOD (reference):
[Link to guide](/en/guides/setup)
```

### Issue 3: Images Not Loading

**Problem**: Images work locally but 404 on production

**Solution**: Check file size and path

```mdx
❌ BAD - File too large (>5MB):
![Image](/images/large-screenshot.png)  

✅ GOOD - File under 5MB:
![Image](/images/screenshot.png)

✅ GOOD - Large files on CDN:
![Image](https://cdn.brainbox.com/screenshot.png)
```

### Issue 4: MDX Component Rendering Error

**Problem**: Component shows as code instead of rendering

**Symptoms**:
```
<Card ... appears as plain text on page
```

**Solution**:
```mdx
❌ WRONG - Extra space before component:
<CardGroup cols={2}>

❌ WRONG - Component not imported (should auto-import)
<CustomComponent />

✅ CORRECT:
<CardGroup cols={2}>
  <Card title="...">
    Content
  </Card>
</CardGroup>
```

### Issue 5: Deployment Stuck

**Problem**: Changes committed 10+ minutes ago but not live

**Debugging Steps**:
```bash
# 1. Check GitHub status
git log -1  # Verify commit pushed

# 2. Check Mintlify dashboard
# → Login to https://dashboard.mintlify.com
# → Check "Recent Deployments"
# → Look for error messages

# 3. Validate mint.json
# → Use https://mintlify.com/schema.json validator
# → Check for JSON syntax errors

# 4. Check file references
mintlify broken-links

# 5. Manual fix:
# → Remove mint.json locally
# → Run `mintlify install`
# → Check dashboard again
```

---

## Maintenance Checklist

### Monthly

- [ ] Check for broken links: `mintlify broken-links`
- [ ] Review analytics: How many users? Which pages popular?
- [ ] Update outdated screenshots
- [ ] Check 404 errors in production

### Quarterly

- [ ] Update product version in docs
- [ ] Review and update feature lists
- [ ] Add new tutorial pages
- [ ] Check for outdated API examples

### Annually

- [ ] Review color scheme/branding
- [ ] Audit all links
- [ ] Update copyright year
- [ ] Plan major documentation restructuring

---

**This practical guide should help you handle real-world documentation scenarios with confidence!**

