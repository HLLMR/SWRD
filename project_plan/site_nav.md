## 🗂️ GOAL: Define the Pages & Functional Views

You want to break this down into:

### 1. **Public-Facing Navigation**

> What the general visitor experiences

### 2. **Authenticated User Portal**

> What contributors, editors, and donors see

### 3. **Admin Backend**

> Your private CMS to control everything

---

## 🔍 1. PUBLIC SITE STRUCTURE (Visitor)

|Page / Route|Description|
|---|---|
|`/`|Landing page with mission, intro, featured content|
|`/read`|Primary scripture reading interface|
|`/compare`|Verse comparison tool (RAW, MT, LXX, KJV, etc.)|
|`/search`|Keyword search with lexicon & full-text|
|`/timeline`|Interactive AM timeline viewer|
|`/dictionary`|Hebrew/Greek/Latin lexicon browser|
|`/names`|Name concordance: people, places, angels|
|`/topics`|Topical library: Nephilim, Prophecies, etc.|
|`/maps`|Interactive map browser|
|`/about`|Mission, licensing, contributors, contact|
|`/donate`|Support page with tiers & access benefits|
|`/downloads`|Free/public assets (PDFs, MP3s, maps)|

---

## 🧑‍💻 2. AUTHENTICATED USER PORTAL (Contributor/Supporter)

|Page / Route|Description|
|---|---|
|`/dashboard`|Personalized entry point (devotionals, updates, stats)|
|`/profile`|Edit account details, preferences|
|`/bookmarks`|Saved verses, studies, tags|
|`/notes`|Private & public verse notes|
|`/plans`|Reading plans or self-paced courses|
|`/submissions`|View or track translation/commentary work|
|`/community`|Comment threads, upvoting, discussion|
|`/alerts`|Personalized notifications or watchlist|
|`/downloads`|Premium resources unlocked by tier|

---

## 🛠 3. ADMIN BACKEND (Private CMS Interface)

|Module|Description|
|---|---|
|Verse Manager|Full CRUD on text entries per source/verse|
|Commentary Manager|Approve, edit, or reject submissions|
|User Manager|Roles, access, bans, activity|
|Timeline Builder|Add/edit events, AM calculations|
|Lexicon Builder|Add new lexemes or corrections|
|Name Map|Reconcile name references and aliases|
|File Manager|Upload charts, images, maps|
|Plans & Collections|Create structured reading guides|
|Moderation|Flagged content review, comment control|
|Analytics|Usage, verse coverage, translation progress|
|Monetization|Manage tiers, donors, product releases|

---

## 🧩 Optional Future Features (Modular Routes)

|Page / Tool|Purpose|
|---|---|
|`/graph`|Verse-to-verse semantic linking graph|
|`/voice`|Listen to RAW narration|
|`/compare/word`|Root-by-root comparative lexicon study|
|`/editor-ai`|Human-in-the-loop translation interface|
|`/apocrypha`|Special scroll archive & analysis|

---

### 🧭 MAIN NAVIGATION HIERARCHY

#### Primary Pages:

|Route|Purpose|
|---|---|
|`/read`|Main scripture viewer|
|`/timeline`|Scrollable, AM-based historical layout|
|`/calendar`|Feast + sabbath visual calendar|
|`/compare`|Side-by-side source view (MT vs LXX etc.)|
|`/search`|Full-text + Strong's + tag explorer|
|`/lexicon`|Dictionary browser|
|`/names`|Concordance for names, places, tribes|
|`/topics`|Thematic index (judgment, messiah, etc.)|
|`/contribute`|Volunteer, review, translate|
|`/about`|Mission, contact, tech, devlog|
|`/donate`|Donation tiers, Bibles to nations, etc.|

> 🔁 Optional nav modes: **reader-first**, **study-first**, or **contributor-first**

---

### 🧭 SECONDARY NAV OPTIONS (SIDEBAR / DRAWERS)

|Location|Content|
|---|---|
|**Left Sidebar**|Scroll Navigator: Genesis, Jubilees, Matthew, etc.|
|**Right Drawer**|Commentary / Notes / Tags for selected verse|
|**Bottom Sheet** (mobile)|Calendar wheel, next/prev chapter, audio bar|

---

### 📥 FOOTER

|Section|Content|
|---|---|
|**SWRD Info**|Mission link, GitHub repo, License|
|**Legal**|Terms of Use, Data Privacy, License|
|**Language**|Language selector|
|**Newsletter**|Input for verse of the week / study digest|
|**Social (optional)**|GitHub, YouTube, RSS|

---

### 🧠 READER PAGE SPECIFICS (`/read`)

|Zone|Element|Notes|
|---|---|---|
|Top|Chapter selector + breadcrumb (`Scroll of Adam › Chapter 1`)||
|Main|Scripture text (`RAW`, `REV`, or comparison mode)||
|Sidebar|Scroll nav OR commentary pane||
|Footer|Previous / Next buttons, Verse progress, Reading mode toggle||

---

## 🧰 TECH STACK HOOKS

|Stack|Suggestion|
|---|---|
|**Blade + Tailwind**|Layouts and dark mode theming|
|**Vue 3 + ShadCN**|Sidebar, drawer, dynamic menus|
|**Alpine.js (optional)**|Lightweight interactivity|
|**Framer Motion / GSAP**|Animate scrolls, verse reveals|