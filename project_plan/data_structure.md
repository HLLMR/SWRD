### 🧱 DATA STRUCTURE

#### 📘 `sources`

_Stores all text sources, including ancient manuscripts and modern translations._

| Field            | Type         | Description                                    |
| ---------------- | ------------ | ---------------------------------------------- |
| `id`             | INTEGER (PK) | Unique ID                                      |
| `name`           | TEXT         | Full name (e.g., "Masoretic Text")             |
| `abbreviation`   | TEXT         | Short tag (e.g., `MT`, `LXX`)                  |
| `language`       | TEXT         | Source language (e.g., Hebrew, Greek)          |
| `type`           | TEXT         | `manuscript`, `translation`, `apocrypha`, etc. |
| `text_direction` | TEXT         | ltr or rtl; controls reading direction         |

---
#### 📜 `scrolls`

_One entry per scroll/book in the SWRD canon._

| Field                      | Type         | Description                                                     |
| -------------------------- | ------------ | --------------------------------------------------------------- |
| `id`                       | INTEGER (PK) | Unique ID                                                       |
| `name`                     | TEXT         | Common name (e.g., “Genesis”)                                   |
| `formal_title`             | TEXT         | Long/formal title (e.g., “Bereshit”)                            |
| `traditional_abbreviation` | TEXT         | Short code (e.g., `GEN`)                                        |
| `restored_order`           | INTEGER      | Order for sorting/printing (by canon/timeline)                  |
| `scroll_group`             | TEXT         | e.g., `Torah`, `Writings`, `Prophets`, `Apostolic`, `Apocrypha` |

---
#### 📂 `chapters`

_Logical divisions of scrolls — aligned to SWRD structure, not necessarily traditional chapters._

| Field                     | Type          | Description                                                                 |
| ------------------------- | ------------- | --------------------------------------------------------------------------- |
| `id`                      | INTEGER (PK)  | Unique ID                                                                   |
| `scroll_id`               | FK → scrolls  | Which scroll this belongs to                                                |
| `restored_chapter_number` | INTEGER       | Internal chapter number                                                     |
| `traditional_reference`   | TEXT          | e.g., “Genesis 2:1–3”                                                       |
| `title`                   | TEXT          | Optional section name                                                       |
| `section`                 | TEXT          | e.g., “Scroll of Adam”                                                      |
| `restored_section_id`     | FK → sections | Anchors to a new table organizing chapters into restored literary divisions |

---
### 🧬 `toledoths`

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`scroll_id`|FK → scrolls|Book/scroll the toledoth appears in|
|`start_verse_id`|FK → verses|Where the toledoth begins|
|`title`|TEXT|e.g., “Scroll of the Generations of Adam”|
|`hebrew_text`|TEXT|Full MT text of the toledoth|
|`summary`|TEXT|Optional explanation or commentary|
|`restored_label`|TEXT|Internal name or label for structuring (e.g., `adam_scroll`)|

> These help structure the **restored scroll format**, build the sidebar nav, and guide AI segmentation.

---

### 📐 `parashots`

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`scroll_id`|FK → scrolls|Source book|
|`verse_id`|FK → verses|Where break occurs|
|`type`|TEXT|`open` or `closed`|
|`note`|TEXT|Optional explanation or footnote|
|`mt_alignment`|BOOLEAN|Whether this matches the MT tradition|

> These give a way to **visually cue scribal rhythm**, help readers pause and reflect, and preserve original formatting.

---

#### 📘 `sections`

| Field       | Type         | Description                            |
| ----------- | ------------ | -------------------------------------- |
| `id`        | INTEGER (PK) | Unique ID                              |
| `scroll_id` | FK → scrolls | Parent scroll                          |
| `label`     | TEXT         | Display title (e.g., “Scroll of Adam”) |

---

#### 📄 `verses`

_Atomic units of text. These are the spine of the database — every translation hooks into these._

| Field                   | Type          | Description                         |
| ----------------------- | ------------- | ----------------------------------- |
| `id`                    | INTEGER (PK)  | Unique ID                           |
| `chapter_id`            | FK → chapters | Which chapter this verse belongs to |
| `restored_verse_number` | INTEGER       | SWRD’s corrected verse number       |
| `traditional_reference` | TEXT          | e.g., “Gen 2:1”                     |
| `note_id`               | Optional FK   | Links to variant/footnote           |
| `order_index`           | INTEGER       | Rendering order inside the chapter  |

---
#### 📖 `texts`

_Stores the actual content of each verse from a given source._

| Field           | Type         | Description                                       |
| --------------- | ------------ | ------------------------------------------------- |
| `id`            | INTEGER (PK) | Unique ID                                         |
| `verse_id`      | FK → verses  | Which verse this content is tied to               |
| `source_id`     | FK → sources | What source produced this content                 |
| `language`      | TEXT         | Language of the content                           |
| `content`       | TEXT         | The actual verse or passage                       |
| `variant_notes` | TEXT         | Optional notes (e.g., DSS variant, missing lines) |

---
#### 🧠 `commentary`

_Used for storing all types of commentary: linguistic, doctrinal, critical, timeline-related._

| Field        | Type         | Description                                                         |
| ------------ | ------------ | ------------------------------------------------------------------- |
| `id`         | INTEGER (PK) | Unique ID                                                           |
| `verse_id`   | FK → verses  | Which verse this commentary belongs to                              |
| `type`       | TEXT         | `literal`, `doctrinal`, `critical`, `timeline`, etc.                |
| `content`    | TEXT         | Commentary body text                                                |
| `source_id`  | FK → sources | Origin of the note if sourced externally (e.g. Masorah, DSS margin) |
| `visibility` | TEXT         | `public`, `editor`, `archived`, `ai_suggested`                      |

---
#### 📚 `lexemes` _(future module)_

_Word root definitions, enabling a full internal dictionary and semantic analysis._

| Field             | Type         | Description                   |
| ----------------- | ------------ | ----------------------------- |
| `id`              | INTEGER (PK) | Unique ID                     |
| `root`            | TEXT         | Original root (e.g., “רוח”)   |
| `language`        | TEXT         | Hebrew, Greek, Latin          |
| `definition`      | TEXT         | Gloss definition              |
| `semantic_domain` | TEXT         | Grouping/category for meaning |
This structure:
- Decouples verse content from reference (handles LXX/MT mismatch + SWRD renumbering)
    
- Supports infinite sources/translations without schema changes
    
- Enables AI/LLM analysis and future print-ready exports

---
### ⚔️ `text_variants`

Captures differences between sources for a single verse.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Target verse|
|`source_id`|FK → sources|Source causing the conflict|
|`variant_text`|TEXT|The alternative wording|
|`type`|TEXT|`addition`, `omission`, `mistranslation`, etc.|
|`note`|TEXT|Commentary about the conflict|

> Needed for: side-by-side comparison, institutional obfuscation flags, doctrinal variant mapping

---
### 📜 `transliterations`

Maps source-language text to Latin-character equivalents.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`lexeme_id`|FK → lexemes|Word root being transliterated|
|`method`|TEXT|System used (e.g. SBL, academic, phonetic)|
|`value`|TEXT|Transliterated string|
|`note`|TEXT|Notes on pronunciation, variations|

> Needed for: pronunciation guides, teaching tools, multilingual glossaries

---
### 🔗 `concordance_links`

Connects lexemes and verse instances for usage indexing.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Where the word appears|
|`lexeme_id`|FK → lexemes|Which root it maps to|
|`surface_form`|TEXT|Actual written word|
|`morphology`|TEXT|Optional morphological tag|

> Needed for: Strong’s-like word searches, cross-verse studies, word density stats

---
### 🔍 `name_references`

Maps people and place names to variants, meanings, and spelling versions.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name_type`|TEXT|`person`, `place`, `tribe`, `angel`, etc.|
|`primary_name`|TEXT|Canonical name (e.g., “Mosheh”)|
|`aliases`|TEXT[]|List of alternate names (e.g., “Moses”, “Μωϋσῆς”)|
|`meaning`|TEXT|Translated etymology|
|`verse_id`|FK → verses|Optional anchor to first appearance|
|`notes`|TEXT|Historical/theological metadata|

> Needed for: search harmonization, name glossaries, reverse lookup, cross-language linking

---
### 🧑‍🤝‍🧑 USERS & PERMISSIONS

#### 🧾 `users`

Stores user accounts, whether readers, contributors, or staff.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`username`|TEXT|Display name|
|`email`|TEXT|Email address (optional for read-only users)|
|`password_hash`|TEXT|Encrypted password|
|`role_id`|FK → roles|Role reference|
|`created_at`|TIMESTAMP|When the account was created|
|`status`|TEXT|`active`, `banned`, `pending`|

#### 🛡 `roles`

Defines user capabilities for moderation and access.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name`|TEXT|`reader`, `contributor`, `reviewer`, `admin`|
|`permissions`|TEXT[]|Array of permission flags|

#### 📈 `contributions`

Tracks verse-level activity for user audit and versioning.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Contributor|
|`verse_id`|FK → verses|Target verse|
|`action`|TEXT|`edit`, `submit`, `approve`, `revert`|
|`timestamp`|TIMESTAMP|Date/time of action|
|`notes`|TEXT|Optional change explanation|

---

### 🧾 VERSE APPARATUS

#### 💬 `footnotes`

Stores explanatory notes, citations, or clarifications.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Anchored verse|
|`label`|TEXT|Footnote key (e.g., `a`, `b`)|
|`content`|TEXT|Note content|
|`source`|TEXT|Optional attribution or origin|

#### 🔗 `crossrefs`

Links one verse to another logically or theologically.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`from_verse_id`|FK → verses|Source verse|
|`to_verse_id`|FK → verses|Target verse|
|`type`|TEXT|`quote`, `fulfillment`, `parallel`, etc.|

#### 🧬 `interleaves`

Maps relationships across non-standard scrolls (e.g., Jubilees, DSS, Apocrypha).

| Field               | Type         | Description                       |
| ------------------- | ------------ | --------------------------------- |
| `id`                | INTEGER (PK) | Unique ID                         |
| `verse_id`          | FK → verses  | Canonical anchor                  |
| `related_source_id` | FK → sources | Source of the interleaved content |
| `related_text`      | TEXT         | Related wording or passage        |

---
### 📊 ANALYTICS & TRACKING

#### 🔢 `word_counts`

Precomputed data for performance and statistical display.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Target|
|`word_count`|INTEGER|Total words|
|`char_count`|INTEGER|Total characters|

#### ✅ `translation_status`

Tracks whether each verse in each translation is complete.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Target verse|
|`source_id`|FK → sources|Translation version|
|`status`|TEXT|`pending`, `complete`, `reviewed`|
|`last_updated`|TIMESTAMP|Date of last status change|

#### 🕘 `change_log`

Stores a log of manual or AI-generated edits.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Affected verse|
|`user_id`|FK → users|Who made the change|
|`timestamp`|TIMESTAMP|When it occurred|
|`diff`|TEXT|Diff or description of change|

---

### 🌍 MULTILINGUAL SUPPORT

#### 🌐 `translations_ui`

Stores user interface translation strings.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`key`|TEXT|Translation key (e.g., `menu.home`)|
|`language`|TEXT|ISO code (e.g., `en`, `es`, `fr`)|
|`text`|TEXT|Translated string|

#### 📖 `verse_translations`

Parallel translations in non-English languages.

| Field             | Type         | Description                            |
| ----------------- | ------------ | -------------------------------------- |
| `id`              | INTEGER (PK) | Unique ID                              |
| `verse_id`        | FK → verses  | Target verse                           |
| `language`        | TEXT         | Language                               |
| `content`         | TEXT         | Translated text                        |
| `translator_name` | TEXT         | Optional attribution                   |
| `text_direction`  | TEXT         | ltr or rtl; controls reading direction |

#### ⚙️ `locale_settings`

Stores user-specific display preferences.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Owner|
|`language`|TEXT|Preferred display language|
|`timezone`|TEXT|Optional TZ|
|`font_size`|TEXT|Small, medium, large, etc.|

---
### 🗺️ MEDIA & VISUAL AIDS

#### 🗾 `maps`

Geographic mapping tied to verses or names.

| Field             | Type         | Description                             |
| ----------------- | ------------ | --------------------------------------- |
| `id`              | INTEGER (PK) | Unique ID                               |
| `title`           | TEXT         | Map name                                |
| `image_url`       | TEXT         | Path to image                           |
| `description`     | TEXT         | Context or source                       |
| `linked_verse_id` | FK → verses  | Optional anchor verse                   |
| `source_url`      | TEXT         | Link to original map/image/chart asset  |
| `origin_note`     | TEXT         | Source archive, license, or attribution |

#### 🖼 `images`

Inline illustrations, diagrams, or scanned artifacts.

| Field         | Type         | Description                             |
| ------------- | ------------ | --------------------------------------- |
| `id`          | INTEGER (PK) | Unique ID                               |
| `caption`     | TEXT         | Display caption                         |
| `image_url`   | TEXT         | Path or embed string                    |
| `attribution` | TEXT         | Photographer, archive, etc.             |
| `source_url`  | TEXT         | Link to original map/image/chart asset  |
| `origin_note` | TEXT         | Source archive, license, or attribution |

#### 📈 `charts`

Timelines, calendars, genealogies, etc.

| Field         | Type         | Description                               |
| ------------- | ------------ | ----------------------------------------- |
| `id`          | INTEGER (PK) | Unique ID                                 |
| `type`        | TEXT         | `genealogy`, `calendar`, `prophecy`, etc. |
| `title`       | TEXT         | Display title                             |
| `content_url` | TEXT         | Render or embed path                      |
| `source_url`  | TEXT         | Link to original map/image/chart asset    |
| `origin_note` | TEXT         | Source archive, license, or attribution   |

---

### 🧵 TAGGING, TOPICS, INDEXING

#### 🏷 `topics`

Topical index (e.g., “atonement”, “messianic”, “judgment”).

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`slug`|TEXT|Unique tag (e.g., `atonement`)|
|`title`|TEXT|Display title|
|`description`|TEXT|Optional explanation|

#### 🔖 `verse_tags`

Many-to-many map between verses and topics.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Anchored verse|
|`topic_id`|FK → topics|Related tag|

#### 📚 `collections`

Curated static groups of verses (e.g., “Laws of Torah”, “Messianic Prophecies”).

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`title`|TEXT|Collection title|
|`description`|TEXT|Explanation or rationale|
|`slug`|TEXT|URL/ID-friendly key|

#### 📎 `collection_items`

Mapping verses into collections.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`collection_id`|FK → collections|Group|
|`verse_id`|FK → verses|Verse|
|`order_index`|INTEGER|Display order|

---

### 🔀 CANON & BOOK STRUCTURE

#### 📏 `canon_mappings`

Allows export to traditional Bibles or alignment to tools like Logos.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`restored_verse_id`|FK → verses|Internal|
|`traditional_reference`|TEXT|e.g., “Genesis 2:3”|
|`book_id`|FK → scrolls|Book code (e.g., `GEN`)|

#### 📘 `book_aliases`

Supports multilingual and alternate naming conventions.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`scroll_id`|FK → scrolls|Related book|
|`language`|TEXT|Language name|

---

## 🔮 HIGH-END OPTIONAL FEATURES

These aren’t necessary for MVP, but could **differentiate SWRD** long-term:

---

### 🧩 1. **Interlinear Layers** (`interlinear_tokens`)

Break down each verse into word-level mappings across Hebrew/Greek and English.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Source verse|
|`token_index`|INTEGER|Word position|
|`surface`|TEXT|Original word (e.g., בָּרָא)|
|`translit`|TEXT|e.g., _bara_|
|`gloss`|TEXT|e.g., “create”|
|`morph`|TEXT|Morphological code|
|`lexeme_id`|FK → lexemes|Root word|

> 🔍 Enables: true interlinear display, academic alignment, lexicon search

---

### 🎙️ 2. **Audio & Narration Support** (`audio_clips`)

Store or reference narration files for each verse or scroll.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`verse_id`|FK → verses|Target verse|
|`language`|TEXT|e.g., English, Hebrew|
|`voice_actor`|TEXT|Optional attribution|
|`file_url`|TEXT|MP3/OGG or streaming link|

> 🎧 Supports: narration, podcast-style reading, accessibility

---

### 🧠 3. **Semantic Graph / Knowledge Mapping** (`verse_links`)

Think “Bible meets Neo4j.” Store rich, user-definable relationships.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`source_id`|FK → verses|Origin verse|
|`target_id`|FK → verses|Destination verse|
|`relation`|TEXT|e.g., “answers”, “contrasts”, “expands”|
|`confidence`|DECIMAL|AI or human rating of relevance|

> 🧠 Enables: AI learning, semantic search, teaching aid generation

---

### 📬 4. **Notifications / Watchlist** (`alerts`)

Let users subscribe to changes, topics, or personal studies.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Subscriber|
|`type`|TEXT|`verse_change`, `new_commentary`, `timeline_event`|
|`target_id`|INTEGER|Target object (e.g., verse_id or topic_id)|
|`sent_at`|TIMESTAMP|When it was last triggered|

> 📩 Supports: newsletters, change tracking, study plans

---

### 📋 5. **Structured Forms / Surveys** (`forms`, `responses`)

Capture feedback, prayer notes, or user submissions.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`title`|TEXT|Form title|
|`fields`|JSON|Dynamic form layout|

|Field|Type|Description|
|---|---|---|
|`response_id`|INTEGER (PK)|Unique ID|
|`form_id`|FK → forms|Which form|
|`user_id`|FK → users|Optional|
|`data`|JSON|Field-value pairs|
|`submitted_at`|TIMESTAMP|Timestamp|

> ✍️ Supports: feedback, prayer cards, crowd-input ideas

---

### ⛪ 6. **Ministry Mode / Reading Plans** (`plans`, `plan_items`)

Serve churches or study groups with pre-built or user-created plans.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name`|TEXT|Plan title|
|`description`|TEXT|What it covers|
|`owner_id`|FK → users|Creator|

|Field|Type|Description|
|---|---|---|
|`plan_id`|FK → plans|Parent|
|`day_number`|INTEGER|Sequence|
|`verse_id`|FK → verses|Reading for that day|

> 🗓 Enables: community-driven reading challenges or devotionals

---

### 🧩 7. **Taggable Annotations / Highlights** (`notes`)

Personal or public annotations with optional visibility.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Owner|
|`verse_id`|FK → verses|Anchored content|
|`content`|TEXT|User note|
|`visibility`|TEXT|`private`, `shared`, `public`|
|`tags`|TEXT[]|Optional topic tags|

> 🧠 Useful for: power users, pastors, discipleship tools

---

### 📅 BIBLICAL CALENDAR STRUCTURE

#### 📘 `calendar_months`

Defines month names, order, and special rules.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name`|TEXT|English name (e.g., “Nisan”)|
|`hebrew_name`|TEXT|Original name (e.g., “נִיסָן”)|
|`month_number`|INTEGER|1–12 (or 13 for intercalary)|
|`days_standard`|INTEGER|Usually 29 or 30|
|`season`|TEXT|`Spring`, `Summer`, etc.|
|`intercalary`|BOOLEAN|If it’s an intercalary month|
|`calendar_type`|TEXT|`Lunar`, `Jubilees`, `Prophetic`|

---

#### 🧱 `calendar_days`

Captures the date structure for rendering or time math.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`calendar_year`|INTEGER|AM year|
|`month_id`|FK → calendar_months|Associated month|
|`day_number`|INTEGER|Day in month (1–30)|
|`is_intercalary`|BOOLEAN|Seasonal marker (Jubilees)|
|`gregorian_date`|DATE|Corresponding modern date|
|`weekday`|TEXT|`Sun`, `Mon`, etc.|
|`feast`|TEXT|Optional: Passover, Shavuot, etc.|

---

#### 🕊️ `jubilee_cycles`

Defines Jubilee year mapping for larger prophetic alignment.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`cycle_number`|INTEGER|1–120 (up to AM 6000)|
|`start_year`|INTEGER|First AM year in this cycle|
|`end_year`|INTEGER|Last AM year (49 or 50 later)|
|`notes`|TEXT|E.g., “Exile”, “Return”, “Yeshua born”|
|`sabbatical_years`|TEXT[]|Years in cycle that are Sabbaths|

---
### 🎉 FEAST DAYS & PROPHETIC ALIGNMENT

#### 🍞 `feast_days`

Defines the annual moedim (appointed times) and their positions in the calendar.

| Field               | Type         | Description                                       |
| ------------------- | ------------ | ------------------------------------------------- |
| `id`                | INTEGER (PK) | Unique ID                                         |
| `name`              | TEXT         | Feast name (e.g., “Passover”)                     |
| `hebrew_name`       | TEXT         | e.g., “פֶּסַח”                                    |
| `month_number`      | INTEGER      | Month it occurs in                                |
| `day_number`        | INTEGER      | Day it occurs on                                  |
| `calendar_type`     | TEXT         | `Lunar`, `Jubilees`, `Prophetic`                  |
| `length_days`       | INTEGER      | Duration (e.g., 1 for Passover, 7 for Unleavened) |
| `sabbath_commanded` | BOOLEAN      | True if it carries sabbath rest                   |
| `offering_required` | BOOLEAN      | True if offerings were required historically      |
| `notes`             | TEXT         | Optional descriptions or instructions             |
| `verse_id`          | FK → verses  | Scriptural anchor of feast reference              |
| `scroll_id`         | FK → scrolls | Optional scroll link for general context          |

---

#### 📜 `prophetic_spans`

Models symbolic or prophetic time periods across Scripture.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`label`|TEXT|e.g., “1260 days”, “70 weeks”|
|`days_total`|INTEGER|Number of days represented|
|`description`|TEXT|What it symbolizes (e.g., exile, tribulation)|
|`source_verse_id`|FK → verses|Where it is stated or initiated|
|`calendar_type`|TEXT|`Prophetic`, `Lunar`, `Jubilees`|
|`associated_event_id`|FK → events|Optional event linkage|

---

#### 🕎 `sabbath_weeks`

Used to anchor 7-day sabbath cycles and count to feast days like Shavuot.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`am_year`|INTEGER|Year in AM|
|`week_number`|INTEGER|1–52 (or 53 for leap)|
|`start_day_id`|FK → calendar_days|First day of the week|
|`is_sabbath_week`|BOOLEAN|True if it includes a feast sabbath|
|`associated_feast`|TEXT|If it's part of Passover, Weeks, etc.|

---

### 📜 TIMELINE STRUCTURE (ERAS, CENTURIES, EVENTS)

#### 🧭 `timeline_eras`

Defines broad spans of theological or historical significance.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`label`|TEXT|Display name (e.g., “Edenic Age”)|
|`start_am`|INTEGER|Beginning year in Anno Mundi|
|`end_am`|INTEGER|Ending year in AM|
|`description`|TEXT|Optional summary of the era|
|`color`|TEXT|UI color for grouping (e.g., hex)|

---

#### 📅 `timeline_centuries`

Organizes the timeline vertically by 100-year buckets (or 50 for Jubilee mode).

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`era_id`|FK → timeline_eras|Parent grouping|
|`start_am`|INTEGER|First AM year in block|
|`end_am`|INTEGER|Last AM year|
|`label`|TEXT|e.g., “AM 2000–2100”|
|`collapsed_by_default`|BOOLEAN|For UI rendering|

---

#### 📌 `timeline_events`

The actual moments in time that matter.


|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`am_year`|INTEGER|Year in Anno Mundi|
|`gregorian_year`|INTEGER|Optional real-world link|
|`title`|TEXT|Short label|
|`description`|TEXT|Explanation or narrative|
|`verse_id`|FK → verses|Optional anchor verse|
|`scroll_id`|FK → scrolls|Optional anchor scroll|
|`era_id`|FK → timeline_eras|For faster query/indexing|
|`tags`|TEXT[]|e.g., “judgment”, “prophecy”, “restoration”|
|`feast_day_id`|FK → feast_days|Optional connection to moedim|
|`event_type`|TEXT|`biblical`, `historical`, `prophetic`, `apostasy`, etc.|

---

#### ➕ `user_feedback`

_New table to passively collect verse or commentary upvotes, flags, reactions._

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Who left the feedback|
|`target_type`|TEXT|`verse`, `commentary`, `note`, etc.|
|`target_id`|INTEGER|ID of the content|
|`reaction`|TEXT|`like`, `dislike`, `flag`, `helpful`, etc.|
|`timestamp`|TIMESTAMP|When feedback was recorded|

---

### 🧠📬 SWRD SCRIBE: Weekly Study & Newsletter Schema

#### 📬 `newsletters`

Stores full newsletter issues for delivery or archive.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`title`|TEXT|Display title (e.g., “Verse of the Week #17”)|
|`am_year`|INTEGER|AM year at time of creation|
|`calendar_day_id`|FK → calendar_days|Optional date anchor|
|`verse_id`|FK → verses|Main verse featured|
|`tone`|TEXT|`devotional`, `academic`, `pastoral`, etc.|
|`content_html`|TEXT|Full email or web HTML|
|`summary_text`|TEXT|Preview/intro|
|`created_at`|TIMESTAMP|When composed|
|`sent_at`|TIMESTAMP|Null until published/sent|

---

#### ✍️ `newsletter_tags`

Tags or topics used to categorize issues.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`newsletter_id`|FK → newsletters|Parent issue|
|`tag`|TEXT|e.g., “atonement”, “messianic”, “repentance”|

---

#### 📩 `subscribers`

Email-based or account-tied newsletter readers.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Optional (null if anonymous)|
|`email`|TEXT|Subscriber address|
|`verified`|BOOLEAN|Opt-in confirmed|
|`language`|TEXT|ISO code (e.g. `en`, `es`)|
|`frequency`|TEXT|`weekly`, `monthly`, `sabbath`, `feast-only`|
|`status`|TEXT|`active`, `paused`, `unsubscribed`|
|`subscribed_at`|TIMESTAMP|Opt-in timestamp|

---

#### ✅ `newsletter_queue`

Holds pending issues for processing or delivery.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`newsletter_id`|FK → newsletters|Issue to send|
|`subscriber_id`|FK → subscribers|Recipient|
|`scheduled_at`|TIMESTAMP|Scheduled delivery time|

---

### 🧠 `ai_agents`

Defines each agent's name, purpose, and configuration.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name`|TEXT|Agent name (e.g., “Scribe”, “Chronologer”)|
|`purpose`|TEXT|Short description|
|`role_prompt`|TEXT|High-level instructions / system prompt|
|`model`|TEXT|`gpt-4`, `claude-3-opus`, `mistral`, etc.|
|`active`|BOOLEAN|Enabled/disabled toggle|
|`last_updated`|TIMESTAMP|Last config change|

---

### 📝 `ai_prompts`

Tracks prompt templates used by agents (version-controlled).

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`agent_id`|FK → ai_agents|Owning agent|
|`label`|TEXT|Descriptive name (e.g., “RAW Genesis 1 Translator”)|
|`input_type`|TEXT|`verse`, `chapter`, `scroll`, `commentary`, etc.|
|`prompt_text`|TEXT|Full prompt with placeholders|
|`version`|TEXT|Manual or semantic (e.g. `v1.2`)|
|`is_active`|BOOLEAN|Can be used by scheduler|
|`created_at`|TIMESTAMP|Timestamp|

---

### 📥 `ai_tasks`

Scheduled or completed AI jobs for specific verse/content.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`prompt_id`|FK → ai_prompts|Prompt used|
|`target_type`|TEXT|`verse`, `commentary`, `timeline_event`, etc.|
|`target_id`|INTEGER|FK to target table|
|`status`|TEXT|`queued`, `running`, `complete`, `error`|
|`result_id`|FK → ai_outputs|Linked result|
|`started_at`|TIMESTAMP|When it began|
|`completed_at`|TIMESTAMP|Null if incomplete|
|`error_log`|TEXT|Optional error message|

---

### 📤 `ai_outputs`

Stores actual generated content + metadata.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`task_id`|FK → ai_tasks|What task created this|
|`content`|TEXT|Full result (markdown or HTML)|
|`token_count`|INTEGER|Input + output token usage|
|`model_used`|TEXT|e.g., `gpt-4-1106-preview`|
|`created_at`|TIMESTAMP|Generation time|
|`approved_by`|FK → users|Optional human approver|
|`approved_at`|TIMESTAMP|Optional|

---

### 🌐 `ai_providers`

Optional if you plan to support multiple API keys/models/providers.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`name`|TEXT|e.g., “OpenAI”, “Anthropic”|
|`base_url`|TEXT|API endpoint|
|`auth_type`|TEXT|`bearer`, `basic`, `api_key`|
|`key_masked`|TEXT|Last 4 chars only, for display|


---

#### 🧪 `ai_usage_policies`

Limits per agent + role (rate limiting or access gating).

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`agent_id`|FK → ai_agents|What agent the rule applies to|
|`role_id`|FK → roles|Role affected|
|`limit_type`|TEXT|`daily`, `monthly`, `burst`, `scope`|
|`value`|INTEGER|Threshold|
|`unit`|TEXT|e.g., `tokens`, `tasks`|
|`notes`|TEXT|Optional rationale or tier requirement|

---

#### 🔐 `ai_permissions`

Fine-grained feature control for interactivity by user.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`user_id`|FK → users|Who has access|
|`agent_id`|FK → ai_agents|Optional (null = all)|
|`feature`|TEXT|e.g., `chat`, `verse_review`, `timeline_populate`|
|`enabled`|BOOLEAN|Access toggle|
|`granted_by`|FK → users|Admin/mod who granted access|
|`granted_at`|TIMESTAMP|Timestamp of permission set|

---

### 📘 `studies`

Long-form essays, explorations, research, and manifestos.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`title`|TEXT|Display title|
|`slug`|TEXT|URL-safe title|
|`summary`|TEXT|Short preview or TL;DR|
|`content_md`|TEXT|Full Markdown or HTML body|
|`status`|TEXT|`draft`, `published`, `archived`|
|`author_id`|FK → users|Writer|
|`created_at`|TIMESTAMP|Initial creation|
|`updated_at`|TIMESTAMP|Most recent edit|

---

### 🔖 `study_tags`

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`study_id`|FK → studies|Which article|
|`tag`|TEXT|Thematic label: `nephilim`, `pre-flood`, `judas`, etc.|

---

### 🔗 `study_links`

Cross-references to site content.

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`study_id`|FK → studies|Parent article|
|`target_type`|TEXT|`verse`, `topic`, `timeline_event`, `scroll`, etc.|
|`target_id`|INTEGER|Reference ID|

---

### 🧑‍🤝‍🧑 `study_collaborators` _(optional)_

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`study_id`|FK → studies|Document|
|`user_id`|FK → users|Contributor|
|`role`|TEXT|`author`, `reviewer`, `editor`|

---

### 🧠 `study_votes` _(optional community feedback system)_

|Field|Type|Description|
|---|---|---|
|`id`|INTEGER (PK)|Unique ID|
|`study_id`|FK → studies|Target|
|`user_id`|FK → users|Who voted|
|`vote`|TEXT|`up`, `down`, `flag`, `truthbomb`|
|`comment`|TEXT|Optional explanation|
|`timestamp`|TIMESTAMP|When it happened|