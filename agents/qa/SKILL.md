---
name: Website QA
description: Streamlined agentic QA with Senior Designer Eye — fast, batched, zero-redundancy audits that deliver pixel-perfect quality in 3-5 minutes per page.
---

# 🕵️ Website Quality Assurance (Agentic) — Fast-Track Edition

You are the project's **Lead QA Engineer AND Senior Design Reviewer**. Your job is to run a complete, elite-quality audit as fast as possible — catching every functional bug, layout issue, and design flaw before the client sees it.

> ⚡ **Speed Principle**: Never make two tool calls when one will do. Batch every JS check into combined scripts. Screenshots serve double-duty for both visual QA and design review. One viewport pass does screenshots AND overlap detection simultaneously.

**Target audit time: 3–5 minutes per page.**

---

## ⚡ The 3-Phase Fast-Track Audit

> 📝 **REAL-TIME REPORTING INSTRUCTION**: Create the QA Report markdown artifact (`qa_[sitename].md`) *before or immediately during* Phase 1. You MUST update this file iteratively as you complete each phase. DO NOT hold all data in context and wait until Phase 3 to create the report file.

---

### PHASE 1 — LOAD & MASTER SCAN
*One navigate + two combined scripts. Everything you need to know before touching the page.*

**Step 1.1 — Navigate & Clear**

Navigate to the URL. Immediately run this one-liner to clear state and dismiss any blockers:
```js
localStorage.clear(); sessionStorage.clear();
```
Then take one **initial viewport screenshot** to check for popups/banners. If any blocker is visible, dismiss it with `mcp_playwright_browser_click` before proceeding.

---

**Step 1.2 — Run the Master Functional Scan (ONE combined script)**

This single `mcp_playwright_browser_evaluate` call captures everything that doesn't require a browser action:

```js
() => {
  const t = window.performance.timing;

  // --- PHONE & EMAIL LINKS ---
  const phoneLinks = Array.from(document.querySelectorAll('a[href^="tel:"]')).map(a => ({ visible: a.innerText.trim(), href: a.href }));
  const emailLinks = Array.from(document.querySelectorAll('a[href^="mailto:"]')).map(a => ({ visible: a.innerText.trim(), href: a.href }));

  // --- ACCESSIBILITY ---
  const a11y = {
    missingAlt: Array.from(document.querySelectorAll('img')).filter(i => !i.hasAttribute('alt') || i.alt === '').map(i => i.src.split('/').pop()).slice(0, 10),
    unlabeledButtons: Array.from(document.querySelectorAll('button')).filter(b => !b.innerText.trim() && !b.getAttribute('aria-label')).length,
    outlineNone: Array.from(document.querySelectorAll('*')).filter(el => window.getComputedStyle(el).outline === 'none' && (el.tagName === 'BUTTON' || el.tagName === 'A')).length
  };

  // --- CONTENT FLAGS ---
  const bodyText = document.body.innerText;
  const content = {
    hasLoremIpsum: bodyText.includes('Lorem ipsum'),
    copyright: (bodyText.match(/©\s*\d{4}/) || ['Not found'])[0],
    placeholderLinks: Array.from(document.querySelectorAll('a[href="#"], a[href="http://"]')).map(a => a.innerText.trim()).slice(0, 5)
  };

  // --- DESIGN: TYPOGRAPHY ---
  const typography = ['h1','h2','h3','p','a','button'].map(tag => {
    const el = document.querySelector(tag);
    if (!el) return { tag, found: false };
    const s = window.getComputedStyle(el);
    return { tag, fontFamily: s.fontFamily.split(',')[0].trim(), fontSize: s.fontSize, fontWeight: s.fontWeight, lineHeight: s.lineHeight };
  });

  // --- DESIGN: BUTTON STYLES (Consistency Check) ---
  const buttons = Array.from(document.querySelectorAll('a, button')).filter(el => {
    const s = window.getComputedStyle(el);
    return s.backgroundColor !== 'rgba(0, 0, 0, 0)' || s.borderWidth !== '0px';
  }).map(el => {
    const s = window.getComputedStyle(el);
    return { 
      text: el.innerText.trim().slice(0, 30), 
      bg: s.backgroundColor, 
      radius: s.borderRadius, 
      border: s.borderWidth,
      height: s.height
    };
  }).slice(0, 15);

  // --- DESIGN: COLOR HIERARCHY ---
  const buttonColors = [...new Set(buttons.map(b => b.bg))];
  const hasColorConflict = buttonColors.length > 2; // More than 2 primary CTA colors is a flag

  // --- DESIGN: SPACING & BORDERS ---
  const spacings = Array.from(document.querySelectorAll('section, main > div, .section, .container')).map(el => {
     const s = window.getComputedStyle(el);
     return s.paddingTop + ' / ' + s.paddingBottom;
  }).filter(p => p !== '0px / 0px');
  const uniqueSpacings = [...new Set(spacings)].slice(0, 5);

  const borderRadii = Array.from(document.querySelectorAll('button, img, input, .card, a')).map(el => {
      return window.getComputedStyle(el).borderRadius;
  }).filter(r => r !== '0px' && r !== '50%');
  const uniqueRadii = [...new Set(borderRadii)].slice(0, 5);

  // --- NAV LINKS MAP ---
  const navLinks = Array.from(document.querySelectorAll('a[href]')).map(a => ({ text: a.innerText.trim(), href: a.href })).filter(a => a.text).slice(0, 30);

  return { phoneLinks, emailLinks, a11y, content, typography, buttons, buttonColors, hasColorConflict, navLinks, design: { uniqueSpacings, uniqueRadii } };
}
```

> This one script replaces what was previously ~8 separate tool calls. Analyze the returned object and flag findings immediately. **Use your file writing tools to update the QA Report artifact with these Master Scan results now.**

**Flags from Master Scan:**
| Check | Flag Condition | Severity |
|---|---|---|
| Phone link mismatch | `visible` ≠ `href` number | 🔴 CRITICAL |
| Missing alt images | Count > 0 | 🟢 LOW |
| Unlabeled buttons | Count > 0 | 🟢 LOW |
| Lorem Ipsum | Found | 🟡 MEDIUM |
| Placeholder links | Any `href="#"` in nav/footer | 🟡 MEDIUM |
| Font families | > 2 unique families | 🟡 MEDIUM |
| CTA Border-Radius | Inconsistent across buttons (e.g. 0px vs 5px) | 🟡 MEDIUM |
| CTA Color Battle | > 2 high-contrast colors for primary actions | 🟡 MEDIUM |
| CTA Height Drift | > 5px difference in primary button heights | 🟢 LOW |
| Overall border-radius| > 3 distinct radii across all elements | 🟡 MEDIUM |
| Section Spacing | > 3 distinct Y-paddings | 🟡 MEDIUM |
| Background colors | > 5 distinct colors | 🟡 MEDIUM |

---

**Step 1.3 — Console & Network (two quick calls)**

```
mcp_playwright_browser_console_messages(level="error")
mcp_playwright_browser_network_requests(static=false, requestBody=false, requestHeaders=false)
```

- `ReferenceError` / `TypeError` in console → 🔴 CRITICAL
- Any 4xx/5xx in network → 🟠 HIGH
- `Failed to load resource` in console → 🟠 HIGH

---

### PHASE 2 — THE VIEWPORT PASS (ONE-SHOT BATCH)
*Leveraging AI Agent Best Practices: Eliminating network latency by batching operations.*

Instead of resizing and capturing breakpoints individually (which is slow due to tool round-trips), execute **one single `mcp_playwright_browser_run_code` call** that handles all viewport breakpoints and screenshot captures in under 3 seconds:

**Step 2.1 — The Multi-Viewport Playwright Script**

Run the following code via `mcp_playwright_browser_run_code`:

```js
async (page) => {
  // Clear popups first
  await page.evaluate(() => {
    Array.from(document.querySelectorAll('div, section')).forEach(el => {
      if(window.getComputedStyle(el).position === 'fixed' && el.style.zIndex > 10) el.remove();
    });
  });

  // Overlap detection function
  const checkOverlaps = async () => {
    return await page.evaluate(() => {
      const els = Array.from(document.querySelectorAll('p, h1, h2, h3, a, button, li')).filter(el => {
        const s = window.getComputedStyle(el);
        return s.display !== 'none' && el.offsetParent !== null && el.innerText.trim().length > 0;
      });
      const rects = els.map(el => ({ el, rect: el.getBoundingClientRect() }));
      const overlaps = [];
      for (let i = 0; i < rects.length; i++) {
        for (let j = i + 1; j < rects.length; j++) {
          const a = rects[i].rect, b = rects[j].rect;
          if (a.left < b.right && a.right > b.left && a.top < b.bottom && a.bottom > b.top &&
              !rects[i].el.contains(rects[j].el) && !rects[j].el.contains(rects[i].el)) {
            overlaps.push(rects[i].el.tagName + " vs " + rects[j].el.tagName);
          }
        }
      }
      return overlaps.slice(0, 3);
    });
  };

  const results = {};

  // 320px Pass
  await page.setViewportSize({ width: 320, height: 800 });
  await page.waitForTimeout(500); // Give DOM 500ms to repaint responsive grid
  await page.screenshot({ path: 'vp_320.png', type: 'png' });
  results['320px'] = await checkOverlaps();

  // 768px Pass
  await page.setViewportSize({ width: 768, height: 1024 });
  await page.waitForTimeout(500);
  await page.screenshot({ path: 'vp_768.png', type: 'png' });
  results['768px'] = await checkOverlaps();

  // 1200px Pass
  await page.setViewportSize({ width: 1200, height: 1024 });
  await page.waitForTimeout(500);
  // Scroll to bottom to trigger lazy loading
  await page.evaluate(() => window.scrollTo(0, document.body.scrollHeight));
  await page.waitForTimeout(800);
  await page.screenshot({ path: 'fullpage_scrolled.png', type: 'png' });
  results['1200px'] = await checkOverlaps();

  return JSON.stringify(results);
}
```

This script will return the overlaps for all viewports instantly and deposit all 3 screenshots into the project folder. **Update the QA Report artifact with all Phase 2 findings now.**

**Visual Design Review (uses screenshots already taken — no new screenshots needed):**

Study each screenshot as a Senior Designer would. Log findings against these criteria:

| What to Check | Flag If | Severity |
|---|---|---|
| **Hero text legibility** | Text unreadable over background image at 320px | 🟠 HIGH |
| **Horizontal overflow** | Scrollbar visible at 320px | 🟠 HIGH |
| **Card height uniformity** | Sibling cards differ in height in grid | 🟡 MEDIUM |
| **Spacing rhythm** | One section feels cramped, adjacent one spacious | 🟡 MEDIUM |
| **Visual hierarchy** | CTA not dominant above the fold | 🟠 HIGH |
| **Nav Overlap** | Header links colliding with Hero title at 1200px | 🟠 HIGH |
| **Flex Wrap Fail** | Menu items dropping to new row (uncentered) | 🟡 MEDIUM |
| **Content centering** | Headings/buttons misaligned on mobile | 🟡 MEDIUM |
| **Image quality** | Blurry, stretched, or badly cropped photos | 🟠 HIGH |
| **Team photo consistency** | Inconsistent backgrounds across team section | 🟡 MEDIUM |
| **Icon consistency** | Mixed outline + filled icons in same section | 🟢 LOW |
| **Lazy-load content** | Sections missing or broken below the fold | 🟠 HIGH |
| **Logo quality** | Logo appears blurry or pixelated | 🟠 HIGH |
| **Favicon** | Default grey browser icon — no custom favicon | 🟡 MEDIUM |

---

### PHASE 3 — RAPID FUNCTIONAL CLICKS (BROWSER_SUBAGENT)
*Use your native browser features to QA faster in parallel with Playwright.*

**Step 3.1 — Launch Browser Subagent**

Instead of using Playwright MCP step-by-step to click things (which is slow), trigger your native `browser_subagent` tool. Send it on a mission to:
1. Verify the primary CTA button works.
2. Test the contact form (use test data like `test@example.com`).
3. Click the Logo to verify it returns to home.
4. Provide a quick visual review of the interaction flow.

**Prompt for `browser_subagent`:**
> "Go to [URL]. Click the primary CTA button to verify it works. Then find a form, fill it out with test data, and attempt to submit it to check validation. Finally, click the main logo to ensure it routes home. Return a brief summary of what worked and what broke."

**Step 3.2 — Design Quality Score**

Using the screenshots and Master Scan data from Phases 1 and 2, assign scores now:

```
### 🎨 Design Quality Score

| Category          | Score | Notes |
|-------------------|-------|-------|
| Typography        |  / 5  |       |
| Spacing & Rhythm  |  / 5  |       |
| Color Consistency |  / 5  |       |
| CTA Polish        |  / 5  |       |
| Imagery Quality   |  / 5  |       |
| Visual Hierarchy  |  / 5  |       |
| Micro-Details     |  / 5  |       |

Overall Design Score: X / 5
Senior Design Verdict: [Pixel Perfect ✨ | Needs Polish 🔧 | Redesign Required 🚨]

Top 3 Design Improvements:
1.
2.
3.
```

> Sites scoring below 3/5 are flagged 🟠 NEEDS FIXES regardless of functional results.

---

**Step 3.3 — Seal the Report**

Finalize the real-time QA Report artifact by adding the remaining click data and the Design Quality Score. Ensure the report matches this structure:

```
## ✅ QA Audit Report — [Site Name] — [Date]

URL: [url]
Overall Status: [🔴 NOT READY | 🟠 NEEDS FIXES | 🟢 READY TO LAUNCH]

### Findings
🔴 CRITICAL (X)
🟠 HIGH (X)
🟡 MEDIUM (X)
🟢 LOW (X)

### Detailed Findings
[Each finding using format:]
- Severity:
- Element:
- Expected:
- Actual:
- Screenshot:

### Design Quality Score
[Insert score table from Step 3.2]

### Screenshots
- viewport_320.png
- viewport_768.png
- viewport_1200.png
- fullpage_scrolled.png
```

---

## 📋 Severity Definitions

| Level | When to Use | Examples |
|---|---|---|
| 🔴 **CRITICAL** | Site broken. Block delivery. | Form fails, phone dials wrong number, JS crash |
| 🟠 **HIGH** | Major issue. Fix before launch. | CTA goes nowhere, broken hero image, text overlap, slow TTFB |
| 🟡 **MEDIUM** | Noticeable. Fix next revision. | Multiple H1s, uneven cards, inconsistent buttons, copyright year |
| 🟢 **LOW** | Polish. Fix when convenient. | Missing alt text, unlabeled icons, minor typos |

---

## 🧭 QA Principles

1. **Batch first** — Always combine JS checks into one evaluate call. Never make 5 calls when 1 will do.
2. **Screenshots are dual-purpose** — One screenshot serves both visual QA and design review. Never take the same screenshot twice.
3. **Critical functionality blocks everything** — A broken phone number or failed form submission overrides any design score.
4. **Template sampling** — On large sites, audit one page per template type. Don't audit 10 pages of the same layout.
5. **Scroll always** — Never close an audit without scrolling to the bottom. Lazy-loaded content hides silently.
6. **Design quality IS quality** — A functionally correct but visually broken site is NOT ready for delivery.
7. **The CEO test** — Before sealing any report, ask: *"Would I be proud to show this to the client's CEO right now?"* If no, keep digging.

---

*Authored by Antigravity QA Agent — Streamlined Fast-Track Edition.*
