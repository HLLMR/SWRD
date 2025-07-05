## 🎨 SWRD STYLE STRATEGY

You’re building a tool of truth. Your UI/UX should say:

- “This is **serious**.” (not gimmicky)
    
- “This is **sacred**, but not sterile.”
    
- “This is **accessible**.” (modern, legible, mobile)
    
- “This is **restored**.” (not Catholic, not Protestant, but something higher)
    

---

## 🧱 1. FOUNDATIONAL AESTHETIC

|Layer|Style|Notes|
|---|---|---|
|**Base Style**|Minimalist, monastic, manuscript-inspired|Like a digital Dead Sea Scroll|
|**Primary Vibe**|Flat + serifed + slightly textured|Modern with sacred weight|
|**UI Metaphor**|Scroll meets console|Serious, readable, editorial|
|**Dark Mode**|Default|With high-contrast light mode toggle|

---

## 🎨 2. COLOR PALETTE

### 🔹 Primary Palette

|Role|Color|Description|
|---|---|---|
|Background|`#111111`|True dark (dark mode default)|
|Text|`#eaeaea`|Soft paper white|
|Accent|`#d6a756`|Gold parchment / priestly tone|
|Hover/Active|`#577d7a`|Sea green / antique ink feel|
|Link|`#88c0d0`|Gentle cyan, readable|
|Error|`#e27878`|Soft crimson|

### 🔸 Light Mode Variant

|Role|Color|
|---|---|
|Background|`#fdfaf6`|
|Text|`#1e1e1e`|
|Accent|`#b88900`|

> Optional: allow users to choose from themes like `Scroll`, `Stone`, `Iron`, `Parchment`

---

## 🔤 3. TYPOGRAPHY

### 🔠 Reading Font (scripture)

|Option|Type|Notes|
|---|---|---|
|**Cormorant Garamond**|Serif|Beautiful, spiritual, designed for literary text|
|**EB Garamond**|Serif|Classical, high legibility|
|**Cardo**|Serif|Unicode Bible-ready font with Hebrew + Greek support|
|**Tienne**|Serif|Monastic manuscript vibe with modern edges|

### 🧱 UI / Nav Font

|Option|Type|
|---|---|
|**Inter**|Sans-serif, modern, readable|
|**Source Sans Pro**|Sleek, balanced|
|**IBM Plex Sans**|Serious but flexible|
|**Lexend**|Accessibility-forward choice|

> Best combo: **Cardo (scripture) + Inter (UI)**

---

## 🧩 4. LAYOUT + FEEL

|Layer|Style|
|---|---|
|Headings|Stylized small caps or gold-trimmed serif (e.g., `"GENESIS 1:1"`)|
|Scroll Nav|Fixed sidebar with `Scroll of Moses`, `Scroll of Adam`, etc|
|Verse|Floating `¶` link + expandable footnotes|
|Timeline|Gold-tinted vertical scrollbar|
|Calendar|Feasts in gold, Sabbaths in dark blue|
|Commentary|Toggle drawer / colored tabs (`doctrinal`, `linguistic`, etc)|

---

## 🔘 5. INTERACTION DETAILS

|Item|Style|
|---|---|
|Button hover|Gold ring or glow|
|Verse hover|Highlight with soft vertical rule|
|Verse reference links|Underline on hover, not default|
|Keyboard nav|Arrow keys for next/prev chapter|
|Reader focus mode|Strip UI chrome, expand font, fullscreen text|

---

## ⚙️ IMPLEMENTATION HINTS

|Tool|Use|
|---|---|
|**TailwindCSS**|Absolute best for maintaining style consistency|
|**ShadCN UI**|Clean, prebuilt components with good dark mode support|
|**Fontsource**|For easy Google font integration without performance issues|
|**Custom Theme Toggle**|Store user preference in localStorage or DB|

---

## 🧪 OPTIONAL: Brand Visuals

|Element|Idea|
|---|---|
|Logo|Stylized aleph-tav ligature, or flaming sword|
|Favicon|Tablet + scroll hybrid|
|Hero Image|Cracked stone + golden lettering|
|Scroll Transitions|Framer Motion or similar for immersive chapter loads|

## Mockup

![](<../ChatGPT Image Jul 5, 2025, 05_32_41 PM.png>)


---

## 🧭 SWRD SITE LAYOUT

---

### 🔝 MASTHEAD / HEADER

|Element|Content|Notes|
|---|---|---|
|**Logo / Title**|`SWRD` or `Restored Word` (stylized)|Upper left, small-caps or serif|
|**Main Nav**|`Read`, `Timeline`, `Calendar`, `Search`, `About`|Horizontal, top-right|
|**Theme Toggle**|Light/Dark mode icon|Right-aligned|
|**Language Selector**|ISO dropdown (EN, ES, FR, etc)|Optional, multilingual-ready|
|**Account Menu**|`Sign In` / `Your Profile` dropdown|Shows when logged in|
|**Search Bar**|Global verse/word search|Inline or expanding on focus|

> 🔒 If user is `admin` or `editor`, show `Admin Panel` button  
> 🔧 Dev mode: consider toggles for “show verse IDs”, “show raw source codes”