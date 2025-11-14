# CLAUDE.md - AI Assistant Guide for 100 Main Signage Project

**Last Updated:** 2025-11-14
**Project Owner:** David Ta (100mainhm@gmail.com, 206-854-3309)
**Current Branch:** `claude/claude-md-mhyat4jepll687zu-01AipRVNdhsdTihzdTLouDxd`

---

## 📋 Project Overview

### What This Project Does
This is an **interactive signage design and selection tool** for 100 & Main Condominium in Seattle. It helps the HOA board select the perfect delivery signage to solve a critical operational problem.

### The Core Problem
Delivery drivers (Amazon, UPS, FedEx, etc.) misinterpret current signage and use the building intercom instead of the exterior package room entrance. This causes:
- Unnecessary resident disruptions
- Inefficient delivery workflows
- Confusion about proper delivery procedures

### The Solution
A multi-step interactive wizard that guides decision-makers through:
1. **Text/Verbiage** - 4 options from prohibitive to purely directional
2. **Font Selection** - 6 professional and playful options
3. **Color Schemes** - 6 options from minimal to extravagant
4. **Material Selection** - Dibond, Acrylic, or PVC with full pricing
5. **Placement References** - Visual mockups and order summary generation

---

## 🗂️ Repository Structure

```
/home/user/100main-signage/
├── index.html                            # ⭐ PRIMARY TOOL (81 KB, 1,900 lines)
│                                         # Modern 5-step wizard with live sidebar preview
│
├── MASTER_INDEX.html                     # Alternative 4-step accordion version (90 KB)
├── ALL_OPTIONS_COMPARISON.html           # Side-by-side comparison matrix (20 KB)
├── ARROW_WAYFINDING_SYSTEM.html          # Arrow design specifications (35 KB)
├── EXISTING_BUILDING_STYLE_MATCHES.html  # Design consistency references (26 KB)
├── EXACT_BUILDING_STANDARD_STYLE.html    # Building standard templates (24 KB)
├── MASTER_INDEX_GALLERY.html             # Photo gallery of options (24 KB)
├── MASTER_INDEX_OLD.html                 # Previous version (42 KB)
├── STEP4_NEW.html                        # Additional placement options (6.5 KB)
│
├── MASTER_INDEX.html.backup              # Backup versions
├── MASTER_INDEX.html.backup2             #
│
├── visualization.png (4 MB)              # Before/after flow diagram
├── diagram.jpg (705 KB)                  # Building layout
├── sign_placeholder_1.png (2.4 MB)       # Location mockup 1
├── sign_placeholder_2.png (2.1 MB)       # Location mockup 2
├── Gemini_Generated_Image_*.png          # AI-generated references
└── 976fc621-cb4a-4bbb-9e6d-6f892c9b0121.png
```

### Key File Purposes

| File | Purpose | When to Edit |
|------|---------|--------------|
| **index.html** | Primary interactive tool | Main feature changes, UI updates |
| **MASTER_INDEX.html** | Backup/alternative version | Keep in sync with index.html |
| **ALL_OPTIONS_COMPARISON.html** | Static comparison view | When adding new options |
| **ARROW_WAYFINDING_SYSTEM.html** | Technical specifications | Arrow design changes |
| **EXISTING_BUILDING_STYLE_MATCHES.html** | Design consistency guide | When building standards change |
| **visualization.png** | Problem/solution diagram | When workflow changes |
| **sign_placeholder_*.png** | Location mockups | When sign placement changes |

---

## 💻 Technology Stack

### Frontend (Pure Vanilla - No Build Process)
- **HTML5** - Semantic markup, responsive meta tags
- **CSS3** - Grid, Flexbox, Custom Properties, Animations
- **JavaScript (Vanilla)** - No frameworks, no npm, no bundling

### External Dependencies
- **Google Fonts** (CDN): Tangerine, Great Vibes, Allura, Sacramento, Dancing Script
- **System Fonts**: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto

### Why No Framework?
- **Simplicity**: Board members can view files directly in browser
- **Portability**: Easy to share via email or USB drive
- **No Build Step**: No npm install, webpack, or compilation required
- **Longevity**: Will work in browsers for decades without maintenance

---

## 🎨 Code Structure & Patterns

### HTML Conventions

#### ID Naming
```html
<div id="step-content">       <!-- kebab-case for IDs -->
<div id="step-header">         <!-- Semantic, descriptive names -->
<div id="step-checkmark">      <!-- Component-based naming -->
```

#### Class Naming
```html
<div class="design-card">      <!-- Generic component classes -->
<div class="text-card">        <!-- Type-specific cards -->
<div class="selected">         <!-- State modifier classes -->
<div class="official-badge">   <!-- Feature modifier classes -->
```

#### Data Attributes
```html
<div data-step="text">         <!-- Step identifier -->
<div data-option="color4">     <!-- Option identifier -->
<div data-sign="sign2">        <!-- Sign location identifier -->
```

### JavaScript Conventions

#### State Management
```javascript
// Global state object
let selectedText = null;
let selectedFont = null;
let selectedStyle = null;
let selectedMaterial = null;

// Text content structured as objects
const text2 = {
    type: 'underlined',
    lines: [
        { text: 'DO NOT USE INTERCOM', underline: true },
        { text: 'AMAZON DELIVERIES', underline: false },
        // ...
    ]
};

// Color schemes as configuration objects
const color1 = {
    bg: '#5A5A5A',
    text: 'white',
    border: '1px solid #E0E0E0'
};
```

#### Function Naming
```javascript
// camelCase for all functions
function selectText(option, optionName) { /* ... */ }
function updateSidebar() { /* ... */ }
function generateOrderSummary() { /* ... */ }
function selectMaterial(material, fullName, desc, prices) { /* ... */ }
```

#### DOM Manipulation Patterns
```javascript
// Always use classList for state changes
document.querySelectorAll('.text-card').forEach(card => {
    card.classList.remove('selected');
});
element.classList.add('selected');

// Direct innerHTML for content updates
document.getElementById('sidebar-text').innerHTML = /* content */;

// Event delegation for dynamic content
document.addEventListener('click', (e) => {
    if (e.target.closest('.text-card')) {
        // Handle click
    }
});
```

### CSS Conventions

#### State Classes (CRITICAL)
```css
.selected {
    border: 3px solid #4CAF50;
    background: #f0f9f0;
    box-shadow: 0 4px 12px rgba(76, 175, 80, 0.3);
}

.collapsed {
    display: none;
}

.active {
    /* Active step styling */
}

.completed {
    /* Completed step styling */
}
```

#### Responsive Breakpoints
```css
/* Desktop - Default styles */
@media (max-width: 1400px) {
    /* Tablet - Sidebar moves to bottom */
}

@media (max-width: 768px) {
    /* Mobile - Single column everything */
}
```

#### Color Variables Pattern
```css
:root {
    --primary-color: #4CAF50;
    --border-color: #e0e0e0;
    --bg-gray: #f5f5f5;
}
```

---

## 🔧 Development Workflows

### Making Changes to the Primary Tool (index.html)

1. **Before Editing**: Always read the file first
   ```bash
   # Understand current state
   grep -n "function selectText" index.html
   ```

2. **Common Edit Patterns**:

   **Adding a New Text Option:**
   ```javascript
   // 1. Add to text options object
   const text5 = {
       type: 'simple',
       lines: [
           { text: 'NEW SIGNAGE TEXT', underline: false }
       ]
   };

   // 2. Add HTML card in Step 1
   <div class="text-card" onclick="selectText(text5, 'Option 5')">
       <h3>Option 5: Your Title</h3>
       <div class="sign-mockup">
           <!-- Text preview -->
       </div>
       <p class="description">Description here</p>
   </div>
   ```

   **Adding a New Color Scheme:**
   ```javascript
   // 1. Define color scheme
   const color7 = {
       bg: '#1a1a1a',
       text: '#ffffff',
       border: '2px solid #gold'
   };

   // 2. Add to selectStyle() function calls
   onclick="selectStyle(color7, 'New Color Name', '1-sentence description')"
   ```

   **Updating Pricing:**
   ```javascript
   // Find material selection calls and update price arrays
   selectMaterial('Dibond', 'Dibond Aluminum', '...',
       [48.91, 119.83, 232.81]  // [11"x9", 24"x19.6", 36"x29.5"]
   );
   ```

3. **Testing Changes**:
   ```bash
   # Open in browser (no build needed!)
   firefox index.html
   # or
   python -m http.server 8000  # Then visit http://localhost:8000
   ```

4. **Keep MASTER_INDEX.html in Sync**:
   - If you update core functionality in `index.html`
   - Consider if `MASTER_INDEX.html` needs the same changes
   - Update both for consistency

### Git Workflow

#### Branch Naming Convention
```bash
# Always use claude/ prefix with session ID suffix
claude/claude-md-mhyat4jepll687zu-01AipRVNdhsdTihzdTLouDxd

# Format: claude/description-sessionid
```

#### Commit Message Format (Semantic Commits)
```bash
# Follow conventional commits specification
feat(step1): add new delivery service option
fix(sidebar): correct cost calculation for acrylic
refactor(colors): generalize color scheme naming
docs(readme): update installation instructions
style(step2): improve font preview spacing
```

#### Recent Commit Patterns (For Reference)
```
6735102 - refactor(problem): generalize from Amazon-specific to multi-service focus
7bcab17 - refactor(step1): replace 'Around the Corner' with 'Down Steps' in Option 4
393ef51 - revert(step1): remove 'DOWN STEPS' from Option 4
f8769b6 - feat(step1): add 'DOWN STEPS' to Option 4 as well
eb56d1b - feat(step1): add 'DOWN STEPS' directional guidance to Options 1-3
```

#### Pushing Changes
```bash
# Always use -u flag for new branches
git push -u origin claude/your-branch-name

# Retry with exponential backoff on network failures
# 2s, 4s, 8s, 16s intervals
```

---

## 🎯 Key Features & Components

### Step 1: Text/Verbiage Selection

**Location:** index.html lines ~200-600

**4 Options:**
1. **Maximum Impact** - "DO NOT USE INTERCOM" + directional guidance + "DOWN STEPS"
2. **All Parcel Deliveries** - Generalized from Amazon-specific
3. **Visual Frame** - Boxed text for official appearance
4. **Complete Guidance** - Positive-only directions (no prohibitions)

**Key Details:**
- Option 4 does NOT include "DOWN STEPS" (recent change per commit 393ef51)
- Options 1-3 DO include "DOWN STEPS" directional guidance
- Recently generalized from "Amazon" to "All Parcel Deliveries" for broader coverage

### Step 2: Font Selection

**Location:** index.html lines ~600-900

**6 Options:**
1. **Helvetica Neue** (Recommended) - Universal readability
2. **Avenir Next Medium** - Building standard
3. **DIN Bold** - Industrial authority
4. **Futura Medium** - Modern geometric
5. **Paramount Hotel Script** - "Rod's Favorite" ⭐ Easter egg
6. **Vegas Marquee Extravaganza** - Over-the-top gold/glitz ⭐ Easter egg

**Implementation:**
```javascript
function selectFont(fontName, fontFamily, description) {
    selectedFont = { name: fontName, family: fontFamily };
    updateSidebar();
}
```

### Step 3: Color Schemes

**Location:** index.html lines ~900-1200

**6 Core Options + Easter Eggs:**
1. **Black Background** (#000000) - Official standard
2. **Gray Building Match** (#5A5A5A) - Blends with concrete
3. **Charcoal + Soft White Border** (#181818 + #F2F2F2)
4. **Deep Slate + Bright White** (#3C3C3C)
5. **Charcoal + Gold Edge** (#181818 + #C7A465) - Luxury hotel
6. **Circus Chaos Edition** ⭐ Easter egg - Rainbow border, hot magenta

### Step 4: Material Selection with Pricing

**Location:** index.html lines ~1200-1400

| Material | 11"x9" | 24"x19.6" | 36"x29.5" | Lifespan | Notes |
|----------|--------|-----------|-----------|----------|-------|
| **Dibond** | $48.91 | $119.83 | $232.81 | 10+ years | **Recommended** |
| **Acrylic** | $51.72 | $97.02 | $225.00 | 7-10 years | Premium look |
| **PVC** | $26.46 | $51.76 | $82.04 | 3-5 years | Budget option |

**Price Update Process:**
```javascript
// Update price arrays in selectMaterial() calls
selectMaterial('Dibond', 'Dibond Aluminum Composite', 'description',
    [newPrice1, newPrice2, newPrice3]
);
```

### Step 5: Signage Placement & Order Summary

**Location:** index.html lines ~1400-1700

**Features:**
- 4+ placement location references with photos
- `generateOrderSummary()` function creates email-ready text
- Copy-to-clipboard functionality
- Real-time cost calculation including tax

---

## 🎨 Design System

### Color Palette (Building Standard)

```css
/* Primary Colors */
--black-standard: #000000;
--white-text: #FFFFFF;
--gray-building: #5A5A5A;
--charcoal: #181818;
--gold-luxury: #C7A465;

/* Borders & Accents */
--border-light: #E0E0E0;
--border-dark: #3C3C3C;
--green-selected: #4CAF50;
--green-bg: #f0f9f0;
```

### Typography Scale

```css
/* Headings */
h1 { font-size: 2.5rem; }      /* 40px */
h2 { font-size: 2rem; }        /* 32px */
h3 { font-size: 1.5rem; }      /* 24px */

/* Body */
body { font-size: 1rem; }      /* 16px */
.description { font-size: 0.95rem; }  /* 15.2px */
```

### Spacing System

```css
/* Consistent spacing scale */
--spacing-xs: 8px;
--spacing-sm: 12px;
--spacing-md: 20px;
--spacing-lg: 30px;
--spacing-xl: 40px;
```

### Interactive States

```css
/* Hover states */
.card:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.15);
}

/* Selected state (CRITICAL for UX) */
.selected {
    border: 3px solid #4CAF50;
    background: #f0f9f0;
}

/* Disabled state */
.disabled {
    opacity: 0.5;
    pointer-events: none;
}
```

---

## 🐛 Common Pitfalls & Solutions

### Issue: Changes Don't Appear in Browser
**Solution:**
```bash
# Hard refresh to bypass cache
Ctrl + Shift + R (Chrome/Firefox)
Cmd + Shift + R (Mac)
```

### Issue: State Not Updating
**Check:**
1. Did you call `updateSidebar()` after state change?
2. Are `selectedText`, `selectedFont`, `selectedStyle`, `selectedMaterial` properly set?
3. Check browser console for JavaScript errors

### Issue: Styling Not Applied
**Debug:**
```javascript
// Check if class was added
console.log(element.classList);

// Verify CSS specificity
// More specific selectors override less specific ones
.step-content .text-card.selected { /* Higher specificity */ }
.text-card.selected { /* Lower specificity */ }
```

### Issue: Font Not Loading
**Check:**
1. Google Fonts CDN link in `<head>`
2. Font family name matches exactly (case-sensitive)
3. Fallback fonts specified: `font-family: 'Primary Font', 'Fallback', sans-serif;`

### Issue: Responsive Layout Broken
**Debug Breakpoints:**
```css
/* Add temporary border to see layout */
* { border: 1px solid red; }

/* Check media query order (mobile-first vs desktop-first) */
```

---

## 🎭 Easter Eggs & Special Features

### Paramount Hotel Script
- **Trigger:** Font option #5
- **Description:** "Rod's Favorite" with hotel emoji
- **Purpose:** Playful option while remaining professional
- **Font Used:** 'Tangerine', 'Great Vibes', cursive

### Vegas Marquee Extravaganza
- **Trigger:** Font option #6
- **Description:** "Maximum Glitz Mode Activated"
- **Styling:** Gold text, neon glow, Comic Sans fallback
- **Purpose:** Humor while demonstrating CSS capabilities

### Circus Chaos Edition
- **Trigger:** Color option #6
- **Description:** "Drivers won't miss this because they literally can't look at it"
- **Colors:** Hot magenta (#FF1493), neon yellow (#FFFF00), rainbow border
- **Purpose:** Contrast demonstration and levity

### Sports Themes
- **Hidden References:** Broncos and Seahawks color schemes mentioned in some descriptions
- **Purpose:** Local Seattle connection

### When to Preserve Easter Eggs
- ✅ Keep them - they're intentional and add personality
- ✅ They demonstrate the tool's flexibility
- ✅ They provide contrast to serious options
- ❌ Don't remove unless explicitly requested by owner

---

## 📊 Performance Considerations

### File Size Guidelines
- **Target:** Keep HTML files under 100 KB when possible
- **Current:** index.html is 81 KB (good)
- **Images:** Optimize PNGs before adding (current images are 2-4 MB)
- **Inline Styles:** Keep CSS in `<style>` tags for portability

### Browser Compatibility
```javascript
// Use feature detection for modern APIs
if (navigator.clipboard) {
    // Use Clipboard API
} else {
    // Fallback to execCommand
}
```

### Load Time Optimization
- ✅ Inline critical CSS
- ✅ Use system fonts as fallbacks
- ✅ Lazy load images if adding many more
- ✅ Minimize external dependencies

---

## 📝 Content Guidelines

### Tone & Voice

**Professional Yet Approachable:**
```
✅ "When confusion costs time and disrupts residents, clear and unambiguous is the directive"
✅ "This option emphasizes prohibitive language followed by clear direction"
❌ "This sign is really good and will totally work"
❌ "Click here to see the best option ever!!!"
```

**Problem-Solution Framework:**
1. State the problem clearly
2. Explain the user behavior causing it
3. Show how the design solves it
4. Provide evidence (wayfinding principles, airport signage examples)

### Text Content Updates

**When Updating Option Descriptions:**
- Keep to 2-3 sentences maximum
- Start with the design principle
- End with the practical outcome
- Use active voice

**Example Pattern:**
```
This option [design choice]. It follows [principle/standard]
used in [real-world example]. Drivers will [expected behavior].
```

### Accessibility

**Always Include:**
```html
<img src="..." alt="Detailed description of image">
<button aria-label="Descriptive label">Icon</button>
<input type="text" id="field" aria-describedby="help-text">
```

---

## 🔍 Debugging Guide

### JavaScript Console Commands

```javascript
// Check current state
console.log({
    text: selectedText,
    font: selectedFont,
    style: selectedStyle,
    material: selectedMaterial
});

// Find all selected elements
document.querySelectorAll('.selected');

// Test function manually
selectText(text1, 'Option 1');
updateSidebar();

// Check if element exists
document.querySelector('#sidebar-preview')
```

### Common Error Messages

**"Cannot read property of null"**
- Element doesn't exist in DOM
- Check ID/class spelling
- Verify element hasn't been removed

**"Uncaught ReferenceError: X is not defined"**
- Variable not in scope
- Function called before definition
- Typo in variable name

**Styles not applying**
- Check CSS specificity with DevTools
- Look for typos in class names
- Verify media query matches current viewport

---

## 🚀 Deployment

### Static Hosting Options
1. **GitHub Pages** (Free)
   ```bash
   # Push to gh-pages branch
   git checkout -b gh-pages
   git push origin gh-pages
   # Enable in repo settings
   ```

2. **Netlify** (Free)
   - Drag and drop folder
   - Or connect to GitHub repo

3. **Email/USB Distribution**
   - Zip entire folder
   - Recipient opens index.html in browser
   - Works offline!

### Pre-Deployment Checklist
- [ ] Test in Chrome, Firefox, Safari
- [ ] Test on mobile device
- [ ] Verify all images load
- [ ] Check all interactive elements work
- [ ] Validate HTML (https://validator.w3.org/)
- [ ] Test with slow network (throttle in DevTools)

---

## 🧪 Testing Guidelines

### Manual Testing Checklist

**Step 1 - Text Selection:**
- [ ] All 4 text cards selectable
- [ ] Selected card shows green border
- [ ] Sidebar updates with selected text
- [ ] Text renders correctly in preview

**Step 2 - Font Selection:**
- [ ] All 6 fonts selectable
- [ ] Font preview shows correct typeface
- [ ] Google Fonts load properly
- [ ] Easter egg fonts work

**Step 3 - Color Selection:**
- [ ] All color schemes selectable
- [ ] Preview background color changes
- [ ] Text color contrasts properly
- [ ] Border styles apply correctly

**Step 4 - Material Selection:**
- [ ] All 3 materials selectable
- [ ] Pricing displays for all sizes
- [ ] Size selection updates cost
- [ ] Material descriptions accurate

**Step 5 - Order Summary:**
- [ ] Summary generates with all selections
- [ ] Prices calculate correctly
- [ ] Copy to clipboard works
- [ ] Email contact info present

### Cross-Browser Testing
```
✅ Chrome 90+
✅ Firefox 88+
✅ Safari 14+
✅ Edge 90+
⚠️ IE 11 (not officially supported but should degrade gracefully)
```

---

## 📚 Reference Documentation

### External Resources
- **Google Fonts:** https://fonts.google.com/
- **CSS Grid Guide:** https://css-tricks.com/snippets/css/complete-guide-grid/
- **Flexbox Guide:** https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- **Clipboard API:** https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API

### Wayfinding Principles Used
- **Prohibitive before Directive:** "Don't do X, instead do Y"
- **Visual Hierarchy:** Most important info largest/boldest
- **Directional Clarity:** Arrows + cardinal directions
- **Redundancy:** Text + symbols for universal understanding

### Design Inspiration Sources
- Airport signage systems (clear, minimal, directive)
- Traffic signage (immediate comprehension required)
- Hotel wayfinding (luxury aesthetic meets functionality)
- Building standard signage (consistency across property)

---

## 🤝 Collaboration Guidelines

### Working with Board Members
- **Response Time:** Board members may take days/weeks to review
- **Decision Making:** Expect multiple revision rounds
- **Priorities:** Functionality > aesthetics, clarity > cleverness
- **Budget Sensitivity:** Always show pricing upfront

### Communicating Changes
```bash
# Good commit message
feat(step1): generalize from Amazon to all delivery services per board feedback

# Include reasoning
refactor(colors): update gold hex to match building standard #C7A465
# Reason: Consistency with existing lobby signage

# Reference issues/discussions
fix(pricing): correct Dibond medium size to $119.83 (was $115.00)
# Source: Email from supplier 2025-11-10
```

### File Naming for New Assets
```bash
# Use descriptive, dated names
sign_mockup_location3_2025-11-14.png
arrow_design_v2_2025-11-14.svg
color_comparison_matrix_2025-11-14.html

# Avoid
image1.png
new_file.html
copy_of_something.jpg
```

---

## 🎓 Learning the Codebase

### For New AI Assistants

**Read These Files First:**
1. `index.html` (lines 1-100) - Understand structure
2. `index.html` (search for "function select") - Core interactions
3. `visualization.png` - Problem/solution context
4. Recent git commits - Recent changes and rationale

**Key Functions to Understand:**
```javascript
selectText(option, optionName)      // Step 1 handler
selectFont(name, family, desc)      // Step 2 handler
selectStyle(colors, name, desc)     // Step 3 handler
selectMaterial(mat, name, desc, $)  // Step 4 handler
updateSidebar()                     // Central state renderer
generateOrderSummary()              // Final output generator
```

**Experiment Safely:**
```bash
# Make a test branch
git checkout -b test/your-experiment

# Make changes to a copy
cp index.html index-test.html
# Edit index-test.html
# Open in browser to test

# If it works, apply to index.html
# If not, just delete the test file
```

### Quick Start: Making Your First Change

```bash
# 1. Read the current file
cat index.html | grep -A 5 "Option 1"

# 2. Make a small change (e.g., update description)
# Use Edit tool to change one description

# 3. Test in browser
python -m http.server 8000

# 4. Commit with semantic message
git add index.html
git commit -m "docs(step1): clarify Option 1 description"

# 5. Push to branch
git push -u origin claude/your-branch-name
```

---

## 🚨 Critical Rules for AI Assistants

### DO ✅
- Always read files before editing
- Use semantic commit messages (feat:, fix:, docs:, refactor:, style:)
- Keep MASTER_INDEX.html in sync with index.html for major changes
- Test changes in a browser before committing
- Preserve easter eggs unless explicitly asked to remove
- Update this CLAUDE.md when making structural changes
- Ask for clarification on pricing/material updates
- Use kebab-case for IDs, camelCase for JavaScript

### DON'T ❌
- Don't introduce frameworks or build systems
- Don't remove content without explicit permission
- Don't change pricing without verification from owner
- Don't break mobile responsiveness
- Don't add external API dependencies
- Don't remove accessibility features
- Don't commit broken JavaScript
- Don't use npm or package.json

### When in Doubt
1. **Read the code** - The answer is probably already there
2. **Check git history** - See how similar changes were made
3. **Test locally** - Open the HTML file in a browser
4. **Ask the user** - Better to clarify than assume

---

## 📞 Contact & Support

**Project Owner:**
- Name: David Ta
- Email: 100mainhm@gmail.com
- Phone: 206-854-3309

**For AI Assistants:**
- This file (CLAUDE.md) is your primary reference
- Git commit history shows decision rationale
- Code comments explain complex logic
- When stuck, read index.html thoroughly - it's self-documenting

---

## 🔄 Changelog

### 2025-11-14
- Created comprehensive CLAUDE.md documentation
- Documented all development workflows and conventions
- Added testing guidelines and debugging reference

### Recent Notable Changes (From Git History)
- **2025-11-10:** Generalized from Amazon-specific to multi-service delivery focus
- **2025-11-10:** Updated Step 1 Option 4 to remove "DOWN STEPS"
- **2025-11-10:** Replaced "Around the Corner" with "Down Steps" in directional text
- **2025-11-09:** Added "Visualizing the Flow" graphic (visualization.png)
- **2025-11-08:** Changed Option 2 from "Amazon Deliveries" to "All Parcel Deliveries"

---

## 📖 Additional Resources

### HTML Structure Pattern
```html
<!-- Standard step structure -->
<div class="accordion-item">
    <div class="accordion-header" onclick="toggleAccordion('step-id')">
        <h2>Step N: Title</h2>
        <span class="step-badge">N of 5</span>
    </div>
    <div id="step-id" class="accordion-content">
        <div class="design-cards">
            <div class="card-type" onclick="selectFunction(data, 'Name')">
                <!-- Card content -->
            </div>
        </div>
    </div>
</div>
```

### CSS Animation Pattern
```css
/* Smooth transitions for all interactive elements */
.card {
    transition: all 0.3s ease;
}

.card:hover {
    transform: translateY(-2px);
}

/* Accordion collapse/expand */
.accordion-content {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
}

.accordion-content.active {
    max-height: 5000px;
}
```

---

**End of CLAUDE.md**

*This document is maintained by AI assistants working on the 100main-signage project. Update it whenever you make structural changes to the codebase, add new features, or discover new conventions.*
