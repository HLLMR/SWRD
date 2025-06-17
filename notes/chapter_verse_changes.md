## 📜 Note: Chapter and Verse Numbering in SWRD

**Purpose:** This document outlines the reasoning behind SWRD’s modified chapter and verse structure, offering clarity for readers and contributors.

---

### 📆 Historical Background

- **Chapter divisions** were introduced in the 13th century by Stephen Langton, Archbishop of Canterbury.
    
- **Verse numbers** came later, finalized in the 16th century by Robert Estienne (aka Stephanus) for his Greek and Latin Bibles.
    
- These divisions were **not part of the original inspired texts**, but editorial tools added for navigation and teaching.
    

---

### 🧠 Why This Matters

While chapter and verse numbers are now **deeply embedded in Bible study and tradition**, they sometimes:

- Break narrative flow awkwardly
    
- Separate logically unified thoughts
    
- Introduce artificial divisions not found in the original Hebrew or Greek manuscripts
    

This has created **the illusion of coherence** where none was intended, and **concealed coherence** where context was split across headings.

---

### 🔁 Why We’re Renumbering

SWRD seeks to **restore narrative integrity** by:

- Aligning divisions to **natural literary structure** and **original scroll breaks** (where discernible).
    
- Respecting the **Masoretic Text (MT)** as our anchor point, rather than late Western editorial tradition.
    
- Clarifying where traditional chapter/verse structure **masks doctrinal or chronological significance**.
    

One clear example is **Genesis 2:1–3**, which belongs with the creation narrative of Genesis 1 — so we reassign it as **Genesis 1:32–34** in SWRD.

---

### 🧭 Staying Grounded

To prevent confusion and preserve cross-referencing:

- **Traditional chapter/verse numbers are preserved in metadata** and notes
    
- **Footnotes and commentary** will refer to both systems where relevant
    
- **Cross-reference tables** may be generated to map SWRD structure to traditional formats
    

This approach honors both **faithful preservation** of Scripture and **transparent restoration** of its true flow.

---

### 🛠️ Implementation Notes

- Each chapter file will include a frontmatter YAML block with:
    
    swrd_chapter: 1
	traditional_reference: "Genesis 2:1–3"
    
- Each verse is labeled using nested headers:
    
    - `# Scroll title`
		
    - `## Chapter 1`
		
	- `### Section title`
        
    - `#### Verse 1`
        
- Commentary or variant notes are separated from the main translation into dedicated `notes/` files.