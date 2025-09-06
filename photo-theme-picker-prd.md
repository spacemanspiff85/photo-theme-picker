# **PRD for Photo Theme Picker**

## **01. Overview**

**Product Name:** Monthly Photo Theme Picker

**Purpose:** A simple HTML page that randomly selects 3 photo themes from a database of 130+ options for our monthly photo challenge group, with smart weighting to reduce recent repeats and a tradition of "Americana" every July.

---

## **02. User Research & Problem Definition**

### **Problem Statement**

* **What specific problem am I trying to solve?** Our photo group needs fresh monthly themes but we've only tracked 9 themes out of 31 months, and we're not systematically avoiding repetition
* **Why does this problem matter to me?** It slows down our monthly kickoffs and we might be missing great theme opportunities
* **What's my current workaround?** Ad-hoc selection with incomplete tracking (22 months have no recorded theme)

### **User Story**

* As the monthly theme selector (rotating role)
* I want to quickly generate 3 theme options plus ability to add a custom 4th
* So that our group can vote and start shooting without decision paralysis

### **Success Scenario**

Visit page → See recent history → Click "Generate Themes" → Get 3 weighted-random themes → Optionally add 4th custom theme → Group votes → Mark winner as used → Done.

---

## **03. Goals & Objectives**

* **Primary Goal:** Generate 3 random themes with probabilistic weighting against recent selections
* **Secondary Goal:** Maintain complete history and allow custom theme entry
* **Nice-to-Have:** Photo gallery, AI-powered theme generation

---

## **04. Scope**

* **Phase 1 (MVP):** 
  * HTML page with 133+ theme database (organized by category)
  * Probabilistic selection (recent themes less likely, not impossible)
  * Custom 4th theme option input
  * History display and management
  * July = Americana tradition
  * Mark selected theme as used

* **Phase 2 (Future):** 
  * Photo upload and gallery
  * AI theme generation from keywords
  * Voting mechanism built-in

---

## **05. Detailed Requirements**

### **5.1 Functional Requirements**

* **Core Functionality:**
  * Database of 133 themes across 7 categories (human environment, nature, emotions, etc.)
  * Weighted random selection - themes used in last 6 months get 20% selection weight
  * Manual theme entry as 4th option
  * July special: "Americana" always appears as one option
  * History tracking with ability to backfill missing months
  * Display last 12 months of history for reference

* **Selection Algorithm:**
  * Calculate months since last use for each theme
  * Weight = 1.0 for never used or >6 months ago
  * Weight = 0.2 for used within 6 months  
  * Weight = 0.1 for used within 3 months
  * If July: Force "Americana" as all three selections

* **Interface Elements:**
  * "Generate 3 Themes" button (prominent)
  * Display area for 3 generated + 1 custom theme
  * "Shuffle Again" button (appears after first generation)
  * Input field for custom 4th theme
  * "Mark as Used" button for winning theme
  * History table showing last 12 months
  * "Add to History" option for backfilling

* **Re-roll Behavior:**
  * Clicking "Shuffle Again" generates 3 new themes
  * Previously shown themes in this session get slightly reduced weight (0.8x) to encourage variety
  * Tracks all themes shown in session to avoid excessive repeats
  * No limit on shuffles - keep going until you find themes you like

### **5.2 Input/Output Examples**

**Example 1: Regular Month (October)**
* Input: Click "Generate Themes"
* Expected Output: 
  - "circles" (from form & techniques)
  - "water in motion" (from nature)
  - "local streetscape" (from human environment)
  - [Custom theme input field]

**Example 2: July Selection**
* Input: Click "Generate Themes" in July
* Expected Output:
  - "Americana" (guaranteed)
  - "Americana" (guaranteed)
  - "Americana" (guaranteed)
  - [Custom theme input field]

**Example 3: Recent Theme Appears (Probabilistic)**
* Input: "Shadows" was used in May 2024, generate in November 2024
* Expected Output: "Shadows" could still appear but only 20% as likely as unused themes

**Example 4: Multiple Shuffles**
* Input: Click "Shuffle Again" after not liking first set
* Expected Output: 3 new themes, with themes from previous shuffle slightly less likely to repeat
* Behavior: Can keep shuffling indefinitely until you find themes you like

---

## **06. Success Metrics**

### **Quick Validation**

* **It's working if:** 
  - Generates themes from all 7 categories over time
  - Recently-used themes appear less frequently (but can still appear)
  - July always includes Americana
  - Can backfill the 22 missing months in history
  - Custom 4th theme can be added easily

* **It's failing if:** 
  - Same themes keep appearing repeatedly
  - Categories are ignored (only picking from one category)
  - Can't track history properly

* **Time saved:** 10-15 minutes per month + better theme variety

---

## **07. Assumptions & Dependencies**

* **Technical Assumptions:**
  * Users have modern browsers with localStorage support
  * Single-page application is sufficient (no backend needed)

---

## **10. Implementation Notes**

### **Theme Database Structure**
```javascript
const themeDatabase = {
  "the human environment": [
    "local streetscape", "famous places", "urban landscape", 
    "industrial landscape", "small towns", "markets", 
    // ... 41 total
  ],
  "seasonal": [
    "Christmas", "Easter", "Halloween", 
    // ... 11 total
  ],
  "nature": [
    "sky and cloud", "water in motion", "trees", 
    // ... 19 total
  ],
  "time of day": [
    "sunset", "sunrise", "blue hour", 
    // ... 6 total
  ],
  "emotions": [
    "peace & tranquility", "strife & war", "joy", 
    // ... 11 total
  ],
  "form & techniques": [
    "circles", "movement", "patterns", "texture",
    // ... 35 total
  ],
  "colors": [
    "red", "orange", "yellow", "green", "blue",
    // ... 10 total
  ]
};

// Special theme not in categories
const specialThemes = ["Americana"];
```

### **History Data to Import**
```javascript
const existingHistory = {
  "2023-07": "Americana",
  "2024-03": "Spring has sprung",
  "2024-05": "Shadows",
  "2024-06": "Summer is here",
  "2024-07": "Americana",
  "2025-05": "The extraordinary in the ordinary",
  "2025-06": "Americana?", // Note: Clarify if this was used
  "2025-07": "Simple Joy",
  "2025-08": "Weather"
};
```

### **Weighting Algorithm Pseudocode**
```javascript
function getThemeWeight(theme, history) {
  const lastUsed = findLastUsedMonth(theme, history);
  if (!lastUsed) return 1.0;
  
  const monthsSince = calculateMonthsDifference(lastUsed, currentMonth);
  if (monthsSince > 6) return 1.0;
  if (monthsSince > 3) return 0.2;
  return 0.1;
}
```

### **Error Handling**
* **Not enough unused themes:** That's OK with probabilistic approach
* **localStorage fails:** Use session storage with warning
* **Missing "Americana" for July:** Add it dynamically

---

## **Quick Start Checklist**

Before building:
* [x] Clear problem definition with actual usage data
* [x] Example inputs/outputs defined
* [x] Success criteria established  
* [x] 133 themes database ready to import
* [x] 9 months of history to import
* [x] Probabilistic algorithm defined
* [x] Custom theme entry specified

---

## **Implementation Priority**

1. **Core Functionality First**
   - Import theme database
   - Basic random selection
   - Display 3 themes

2. **Add Intelligence**
   - Implement weighting algorithm
   - Add July → Americana rule
   - History tracking

3. **Polish**
   - Custom 4th theme input
   - History display table
   - Backfill capability
   - Mobile-friendly design

## **Notes for Claude Code**

- Start simple: working button that shows 3 random themes
- Add the weighting system (probabilistic, not hard cutoff)
- Make the custom theme input prominent but optional
- History section should show gaps clearly (for backfilling)
- Consider adding category labels to selected themes for variety visibility
- Keep it fun and lightweight - this is for a photo club, not NASA!