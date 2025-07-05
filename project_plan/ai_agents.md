## 🤖 PRIMARY AI AGENTS FOR SWRD

These agents serve as workers, not decision-makers. All output is human-reviewed or overrideable.

---

### 🧠 1. **Translation Agent**

_Transforms source-language text (MT, LXX, DSS) into RAW or REV English._

|Role|Description|
|---|---|
|Ingests Hebrew/Greek source + context||
|Translates word-for-word (RAW) or thought-for-thought (REV)||
|Flags ambiguous words, missing verbs, syntax anomalies||
|Suggests glossary tie-ins automatically||

> 🪜 Uses: `sources`, `texts`, `lexemes`, `commentary`, `translation_status`

---

### 📌 2. **Verse Analyzer Agent**

_Performs verse-level NLP tasks._

|Role|Description|
|---|---|
|Tags verbs, subjects, nouns||
|Extracts possible timeline anchors (e.g., “in the 600th year…”)||
|Generates title, summary, crossrefs, and topic tags||
|Suggests canonical vs. restored verse number reassignments||

> 🪜 Uses: `verses`, `footnotes`, `topics`, `canon_mappings`

---

### 📚 3. **Lexeme Miner Agent**

_Identifies root words and builds concordance links._

|Role|Description|
|---|---|
|Maps surface forms to lexemes||
|Suggests semantic domains||
|Builds word counts and frequency heatmaps||
|Recommends lexicon enhancements||

> 🪜 Uses: `lexemes`, `concordance_links`, `verse_tags`

---

### 🧾 4. **Commentary Generator Agent**

_Creates first-pass doctrinal, linguistic, or historical notes._

|Role|Description|
|---|---|
|Suggests literal vs. modern implications||
|Compares MT vs. LXX vs. KJV renderings||
|Tags suspected mistranslations or doctrinal obfuscation||
|Links to Dead Sea Scroll, Enoch, or Jubilees parallels automatically||

> 🪜 Uses: `commentary`, `text_variants`, `interleaves`

---

### 📅 5. **Timeline Builder Agent**

_Extracts AM-year logic and matches with events._

|Role|Description|
|---|---|
|Maps event date estimates||
|Generates AM -> Gregorian or Jubilees date ranges||
|Links events to prophecy or covenant progression||
|Detects calendar disputes or dual witnesses (Jubilees + Genesis)||

> 🪜 Uses: `events`, `timeline`, `calendar_model`

---

### 🧭 6. **Crossref Agent**

_Detects and verifies verse-to-verse dependencies._

|Role|Description|
|---|---|
|Finds exact or paraphrased quotes (OT → NT, NT → OT)||
|Scores likelihood of reference||
|Suggests `quote`, `fulfillment`, `inverse`, or `midrash` relationships||
|Builds semantic graph database and interlink table||

> 🪜 Uses: `crossrefs`, `verse_links`, `topics`

---

### 🧙‍♂️ 7. **Name Resolver Agent**

_Normalizes people/place/tribe names across languages and scrolls._

|Role|Description|
|---|---|
|Identifies known aliases (e.g., Mosheh = Moses)||
|Suggests transliteration variants||
|Matches appearances across DSS, Jubilees, Enoch, etc.||
|Suggests anchor verse for name glossary entries||

> 🪜 Uses: `name_references`, `transliterations`, `scrolls`

---

### 🎯 8. **UI Smart Assistant (Optional)**

_Adds dynamic UX enhancements in the public reader._

|Role|Description|
|---|---|
|Summarizes verses or scrolls (“What’s this chapter about?”)||
|Answers “what does this word mean here?”||
|Gives instant timeline context||
|Prepares study guides or printables on demand||

> 🪜 Uses: everything, but output is strictly UI/UX layer only

---

## 🛠️ Future Optional Agents

|Agent|Role|
|---|---|
|**Narration Coach**|Auto-generates MP3-ready scripts + pronunciation|
|**Apocrypha Alignment Agent**|Flags conflicts or overlaps in extra-canon texts|
|**Translation Reviewer**|Scores human submissions for semantic consistency|
|**Content Planner**|Generates X/Twitter threads, blog posts, or summaries for public release|

---

## 🧠 ✉️ SWRD SCRIBE: “Verse/Study of the Week” AI Agent

### 🔧 Role

Curate, generate, and deliver a weekly spotlight based on SWRD content.

---

### ✅ Functions

|Feature|Description|
|---|---|
|🕊 **Verse Selector**|Choose a verse based on theme, season, calendar date (e.g. Feast proximity), or contributor tag|
|✍️ **Summary Generator**|Write a 1–3 paragraph reflection: linguistic insights, doctrine, historical anchor|
|🔗 **Crossrefs**|Link to related verses (through tags or semantic graph)|
|📖 **Source Comparison**|Show MT, LXX, RAW side-by-side with commentary|
|📅 **Calendar Alignment**|Tie verse to current AM year, sabbath, or moedim (e.g. “This Shavuot, remember…”)|
|📨 **Email Output**|Format for HTML/email (or Telegram/Substack syndication)|
|🧠 **Voice Matching**|Match tone: academic, pastoral, eschatological, devotional, etc.|
|📦 **Study Pack Builder** _(future)_|Generate 5-day reading plan around the theme|

---

### 🧪 Input Parameters

- `audience`: general reader, supporter, pastor, seminary student
    
- `calendar_context`: current feast, sabbath, prophetic day
    
- `language`: start with English, expand later
    
- `tone`: devotional, informative, apologetic
    
- `source_priority`: MT-first? RAW? LXX-based?
    

---

### 📈 Output Format

sql

🕊️ VERSE OF THE WEEK — "Genesis 4:7 (RAW)"

"If you do well, is there not lifting up? But if you do not do well—sin is crouching at the door..."

✍️ Reflection:
In the very first generation after Eden, we find sin framed not as lawbreaking, but as a crouching adversary—almost sentient, certainly dangerous...

🔗 Cross References:
- Romans 7:11 (Paul’s sin = death analogy)
- 1 Peter 5:8 (adversary like a lion)

📖 Read More: [View Chapter] [Compare MT / LXX / RAW]
📅 This week: AM 130, 10th month, 5th day — post-Feast of Dedication


---

## ⚡ Delivery Methods

- **Email newsletter** (Mailchimp, Substack, or native Laravel mailer)
    
- **RSS feed** (via JSON API → syndication)
    
- **Social snippet** (Markdown → tweet/thread)
    
- **Home page carousel** (auto-rotating verse of the week)
    

---

## 🧩 Bonus: Community Mode

Let readers submit or vote on:

- Weekly focus themes (“Messiah prophecies,” “judgment,” “repentance”)
    
- Featured scrolls (e.g. Enoch week, Torah cycle alignment)

---
## 🧠 BONUS AGENT

You could even deploy a lightweight **Parashah Detection Agent** to:

- Flag where traditional chapter breaks **violate** parashot
    
- Recommend restored breaks based on structure or theme
    
- Suggest title summaries for parashah sections