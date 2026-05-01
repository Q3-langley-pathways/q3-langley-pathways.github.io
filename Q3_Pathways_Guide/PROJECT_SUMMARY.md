# KS4 Pathways Guide - Complete Project Summary

## What This Is
A **Key Stage 4 (Year 10-11) Pathways selection guide website** for Q3 Academy Langley. It helps students and parents understand:
- What GCSEs are
- The different subject choices available
- Career pathways
- Teacher contact information
- Timeline and deadlines
- FAQ section

**Single File:** `index.html`  
This is a **self-contained HTML file** with all CSS, JavaScript, and content embedded. No external files needed.

---

## Key Problem Solved
**Teacher contact emails were being flagged by antivirus software** as potential phishing/malware because plain email addresses in HTML look like security threats.

**Solution:** Email obfuscation - emails are stored as JavaScript-concatenated strings that only assemble in the browser at runtime, bypassing antivirus detection at the source level.

---

## Main Features & Customizations

### 1. **Email Obfuscation System**
- **Location:** Lines 2833-2851 in the HTML (JavaScript email database)
- **How it works:**
  - Emails stored as concatenated strings: `'r' + 'singh' + '@lan.merciantrust.org.uk'`
  - Assembled at runtime in the browser (never appears as full string in source)
  - 17 teachers have email entries
  - Each teacher has a `data-teacher` attribute connecting them to their email

**Current Teachers with Emails:**
- Mr. Singh (English)
- Mrs. Markwick (Spanish)
- Mr. Khan (Creative iMedia)
- Mrs. Morrall (Music Technology)
- Miss Bloor (Hospitality & Catering)
- And 12 others...

### 2. **Email Display Markup**
- **Location:** Throughout the HTML document where teachers are mentioned
- **Format:** `<span data-teacher="singh">Contact through Teams</span>`
- **Why:** JavaScript finds these spans and replaces "Contact through Teams" with clickable mailto links
- **Applied to:** ~23 teacher contact mentions across all pages

### 3. **Scroll Position Preservation**
- **Problem:** Users clicking "Back to Home" would jump to the top of the page instead of returning to where they were
- **Solution:** Global variable `homeScrollPosition` stores the scroll position
  - `goToPage()` saves position before leaving home page
  - `goHome()` restores position when returning
- **Location:** Lines 3054-3072

### 4. **Custom Content Placeholders**
- **Applied to:** All 25 course/info pages (every page except home)
- **Two sections on each page:**
  1. `[Prefect Text (Custom)]` - For course introduction or promotional text (gray italic)
  2. `[Videos/Images]` - For media content like videos or subject images (blue dashed box)

**Styling:**
- Background: `rgba(94, 179, 246, 0.05)` (subtle blue tint)
- Left border: `4px solid rgba(94, 179, 246, 0.3)` (blue accent)
- Easy to identify and replace with actual content

### 5. **Teacher Email Link Styling**
- **Location:** Lines 688-701 in CSS
- **Color:** #f0f0f0 (off-white) with subtle blue underline
- **Hover effect:** Brightens to white with solid blue underline
- **Purpose:** Links blend naturally with site design while remaining visible

---

## All Pages in the File (27 total)

### Info Pages (5)
1. Home Page (no placeholders needed)
2. Grading System
3. Pathways Overview
4. FAQs
5. Timeline

### Core Subjects (5) - Required for all students
6. English Language & Literature
7. Mathematics
8. Science
9. History-Geography (choose one)
10. French OR Spanish (choose one, if selected by MFL team)

### Optional GCSE Subjects (10)
11. Art & Design
12. Music
13. Computer Science (selective entry, Grade 7+ Maths required)
14. Religious Studies
15. Further Maths (Grade 8+ predicted Maths, early morning sessions)
16. Business Studies
17. Retail Business
18. Child Development
19. Health & Social Care
20. Sports Studies

### Vocational Subjects (7) - Level 1/2, more practical
21. Music Technology
22. Performing Arts
23. Creative iMedia
24. Hospitality & Catering
25. Travel & Tourism
26. (Plus other vocational options)

---

## How to Edit the File

### Adding New Content to a Page
Each page follows this structure:
```html
<div class="page" id="pageNamePage">
    <div class="course-page-header [type]">
        <span class="subject-icon-large">emoji</span>
        <h1>Page Title</h1>
        <span class="course-badge">Badge text</span>
    </div>
    
    <div class="course-section [type]" style="background: rgba(94, 179, 246, 0.05); border-left: 4px solid rgba(94, 179, 246, 0.3);">
        <div style="color: #a0a0a0; font-style: italic; margin-bottom: 15px;">[Prefect Text (Custom)] - Space for additional course introduction or promotional text</div>
        <div style="background: #252540; border: 2px dashed rgba(94, 179, 246, 0.3); padding: 30px; text-align: center; color: #5eb3f6; margin: 15px 0;">
            [Videos/Images] - Space for course preview videos or subject images
        </div>
    </div>
    
    <!-- Replace placeholder sections above with actual content -->
</div>
```

### Replacing Placeholders
1. Find `[Prefect Text (Custom)]` - replace entire `<div>` with your introduction text
2. Find `[Videos/Images]` - replace entire `<div>` with `<img>`, `<video>`, or other media

### Adding a Teacher Email
1. Add entry to email database (lines 2833-2851):
   ```javascript
   'newteacher': 'newteacher' + '@lan.merciantrust.org.uk',
   ```
2. Add `<span data-teacher="newteacher">Contact through Teams</span>` where teacher info appears
3. Save file

---

## Technical Details

### Why This Approach?
- **Self-contained:** Single HTML file, no server needed, easy to share
- **Antivirus safe:** Emails never appear as complete strings in source code
- **No external dependencies:** All CSS and JavaScript embedded
- **Easy to edit:** Open in any text editor

### JavaScript Event Used
- **`window.addEventListener('load', ...)`** - Not `DOMContentLoaded`
  - Reason: `load` event fires AFTER all resources (images, stylesheets) are loaded
  - More reliable for DOM manipulation timing
  - Ensures all page elements exist before email linking

### CSS Color Scheme
- **Primary dark:** #252540 (dark blue-gray background)
- **Primary light:** #1a1a2e (darker backgrounds)
- **Accent blue:** #5eb3f6 (links, borders, highlights)
- **Text:** #e8e8e8 (off-white on dark backgrounds)

### File Size
- ~200KB+ (single HTML file with embedded CSS and JavaScript)
- Takes 1-2 seconds to load in browser (normal)

---

## Navigation Flow

**Home Page:**
- Shows all course/subject categories
- "Back to Home" button visible when on any other page
- Scroll position preserved when returning

**Course Pages:**
- Each has back button
- Teacher contact information at bottom
- Consistent layout across all pages

---

## If Something Breaks

### Common Issues & Fixes

**Emails not showing:**
- Check that `<span data-teacher="key">` matches email database keys
- Ensure browser has JavaScript enabled
- Check browser console for errors (F12)

**Page won't display:**
- Check that page `id="..."Page"` is unique
- Ensure all opening tags have closing tags
- Look for syntax errors in CSS (unclosed brackets)

**Styling looks wrong:**
- Check for CSS conflicts between page classes (`.core`, `.optional`, `.vocational`)
- Verify color hex codes are correct (#RRGGBB format)
- Clear browser cache (Ctrl+Shift+Delete)

---

## Important Notes

- **Do NOT share plain email addresses** - always use obfuscation
- **Backup this file** - it contains all content and configuration
- **Test in browser** after making changes - save HTML file, refresh browser (F5)
- **No database needed** - everything is in this one file
- **Mobile responsive** - file works on phones and tablets

---

## Contact Information

This guide was created for Q3 Academy Langley's KS4 Pathways program.  
Last updated: 2026-04-30Copilot: Select Model

For technical questions about the file structure, contact the developer.
sign