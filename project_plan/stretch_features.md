### 🧩 POTENTIALLY MISSING OR OPTIONAL

#### 1. **Offline Mode / PWA Support**

- Installable on mobile/desktop
    
- Store scrolls locally with service workers
    
- Great for missionaries, prison ministries, travel
    

#### 2. **Fuzzy Search + NLP Querying**

- Ask: “Show me all times God speaks from the sky”
    
- Autocomplete + Hebrew root suggestions
    
- “Did you mean…” engine
    

#### 3. **Bible Builder Toolkit (Dev/Power Users)**

- Custom export: “Give me all verses tagged [Eschatology] with Hebrew + Greek interlinear, in PDF”
    
- Modular study plan generator
    
- Plugin system down the road?
    

#### 4. **Verse Influence/Weight Graph**

- Track how often a verse is quoted, referenced, or commented on
    
- Useful for study emphasis or theological density
    

#### 5. **Parallel Manuscript Viewer**

- Scroll side-by-side MT vs. DSS fragment vs. LXX Greek scan
    
- Useful for Enoch, Jubilees, Dead Sea Scrolls reconstruction
    

#### 6. **REST vs. GraphQL API**

- Offer external apps access to RAW
    
- Rate-limited, token-authenticated
    
- Could drive a native app or AI Bible bot
    

---

### 🔐 Defensive Design Features

To preserve purity and control over SWRD's mission:

- **Immutable mode**: freeze “approved” verses from future AI overwrite
    
- **Human confirmation queue**: only marked “blessed” texts appear in public RAW
    
- **Audit trail**: who translated, who edited, who approved
    

---

### 📦 Future-SWRD Vision Ideas

|Concept|Description|
|---|---|
|**SWARD**|A “Study With Annotated Restored Doctrine” print/devotional Bible|
|**SWRD Companion**|Podcast/video channel walking through RAW line-by-line|
|**Verse API**|Public SWRD index used by 3rd party pastors, tools, even AI|
|**RAW-Only Bible App**|Minimalist Android/iOS app with audio/text-only RAW edition|

---

## 🚀 STUDIES INTEGRATION POINTS

|Feature|How to Integrate|
|---|---|
|**Navigation**|`/studies` route, with `/studies/:slug` for detail view|
|**Searchable**|Integrate with global search by keyword, tag, verse|
|**Topic Index**|Auto-generate by tag (e.g. `cosmology`, `rebellion`, `judgment`)|
|**Backlog tracking**|Unpublished studies can act as backlog/todo|
|**Contributor access**|Allow editors or supporters to write and submit content|
|**AI use**|Let the “Scribe” agent draft or outline studies from verse groups, backlog items, or timelines|
