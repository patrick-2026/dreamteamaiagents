---
name: Website QA
description: A comprehensive instruction set for performing a thorough Quality Assurance (QA) audit on websites, spanning functionality, visual consistency, and common spelling/alignment issues.
---

# 🕵️ Website Quality Assurance Skill

This skill provides a systematic approach to verifying the health of a website's preview before production deployment.

## 📋 Audit Workflow

When utilizing this skill, perform investigations in the following order:

### Phase 1: Critical Functionality
- **Sync Contact Info**: Extract all `tel:` and `mailto:` links and compare them with their visible text labels.
- **Form Deep-Dive**: Locate all `<form>` elements and verify:
    - **Required Fields**: Do they trigger validation errors?
    - **Email Logic**: Does the input type enforce valid email syntax?
    - **Submission State**: Does the UI provide clear feedback (Success/Error) after clicking "Submit"?
- **Multi-Page Crawl**: For sites with many pages, extract the main navigation links and categorize them by **Template** (e.g., Services, Blog, Locations, Listings).
    - **Audit Strategy**: Perform a full audit on at least one page from *each* category to identify template-wide bugs (such as missing viewport tags or fixed-width containers).
    - **Link Health**: Scan for any placeholders (e.g., `#`, `http://`, `Coming Soon`) across the entire navigation menu.

### Phase 2: Content & Copywriting
- **Spelling Scan**: Systematic scan of all headings (`h1` - `h6`) and paragraph text for typos or grammatical errors.
- **Tone Check**: Ensure CTA buttons use consistent branding (e.g., choosing either "Schedule" or "Book" across the entire site).
- **Metadata**: Verify the `<title>` tag and `<meta description>` are configured and meaningful.

### Phase 3: Visual & Responsive Alignment
- **Viewport Comparison**: Take screenshots of the **Desktop (1200px)**, **Tablet (768px)**, and **Mobile (320px)** views.
- **Spacing Check**: Analyze the vertical padding between sections to ensure they scale proportionally (e.g., 60px on Desktop, 40px on Mobile).
- **Element Crowding**: Pay specific attention to the mobile header—ensure the logo and icons are not "sandwiched" too tightly.

### Phase 4: Technical Health
- **Console Monitoring**: Keep the browser console open and report any errors (`ReferenceError`, `TypeError`) that occur during page load.
- **Accessibility Check**: Verify that informative images have `alt` text and that the "Skip to Content" logic (or simple tab-navigation) functions.

## 🛠️ Recommended Tools & Commands
*   Use `mcp_playwright_browser_evaluate` to extract links and computed styles.
*   Use `mcp_playwright_browser_take_screenshot` (full page) for visual comparisons.

---
*Authored by Antigravity.*
