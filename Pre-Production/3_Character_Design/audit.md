I tried to load **`init.md` from your GitHub repo** but the file wasn’t present at that path (GitHub returned “Not Found”), so I couldn’t read your project structure directly. If you can share the actual *contents* of that file or the correct path, I can integrate it precisely.

That said, I *can* give you **a clean, production-ready deliverable structure** you can drop into
`../Pre-Production/3_Character_Design` along with a fully templated **onboarding doc** explaining exactly how to use your upgraded Character Generator Engine v2.0.

Below is:

📌 **1. A standardized folder & file template** for your Character Design folder
📌 **2. A universal `README.md` onboarding doc**
📌 **3. A general JSON schema** that replaces your Luna example but is fully generic
📌 **4. A one-shot request template you can use to generate any character**

You can paste this into your repo and adjust paths as needed.

---

# 🗂️ Folder Structure — `3_Character_Design`

Place this inside:

```
Pre-Production/3_Character_Design/
```

```
3_Character_Design/
│
├── characters/  
│   ├── [CHAR_ID]/
│   │   ├── [CHAR_ID].json
│   │   ├── prompts/
│   │   │   ├── character_sheet.txt
│   │   │   ├── expression_sheet.txt
│   │   │   ├── pose_sheet.txt
│   │   │   ├── sticker_pack.txt
│   │   ├── assets/
│   │   │   ├── reference.png
│   │   │   ├── expression_grid.png
│   │   │   ├── pose_grid.png
├── templates/
│   ├── character_json_schema.json
│   ├── prompt_template.txt
├── README.md
```

**Explanation**

* **`characters/`** — actual character folders
* **`[CHAR_ID].json`** — character definitions
* **`prompts/`** — generated prompt text files
* **`assets/`** — visual outputs you generate later
* **`templates/`** — shared templates
* **`README.md`** — onboarding

---

# 📘 `README.md` (Onboarding)

Copy this into the root of `3_Character_Design`.

```markdown
# 3_Character_Design

This folder contains **character definition JSONs** and **generated prompt packs** for all characters used in production.

## Folder guide

### `characters/`

Each character has:
- A unique folder named by `CHARACTER_ID`
- A character JSON file (`CHARACTER_ID.json`)
- A set of prompt text files used to generate art assets
- A set of exported assets (images)

Example:
```

characters/
LUNA_001/
LUNA_001.json
prompts/
character_sheet.txt
expression_sheet.txt
pose_sheet.txt
sticker_pack.txt
assets/
reference.png
expression_grid.png
pose_grid.png

```

### `templates/`

Holds:
- `character_json_schema.json` — the schema used to validate character JSONs
- `prompt_template.txt` — a generic text template used to generate prompts

---

## How to generate a new character

Use the **one-shot request template** below in your prompt to the Character Generator Engine.

**One-Shot Request Template**

```

CreateCharacter(
character_name: "NAME",
visual_style: "STYLE",
genre: "GENRE",
narrative_role: "ROLE",
biological_data: {
age: NUMBER,
ethnicity: "DESCRIPTION"
},
narrative_archetype: "ARCHETYPE",
required_outputs: [
"character_json",
"character_sheet_prompt",
"expression_sheet_prompt",
"pose_sheet_prompt",
"sticker_pack_prompt"
],
plot_reference?: plotJson
)

```

**Example**

```

CreateCharacter(
character_name: "Luna Reyes",
visual_style: "Studio Ghibli watercolor",
genre: "Educational adventure",
narrative_role: "Protagonist - educational guide",
biological_data: {
age: 18,
ethnicity: "Latina"
},
narrative_archetype: "Determined Tech Youth",
required_outputs: [
"character_json",
"character_sheet_prompt",
"expression_sheet_prompt",
"pose_sheet_prompt",
"sticker_pack_prompt"
],
plot_reference?: main_plot.json
)

```

---

## Output files

Once generated, paste outputs here:

- `*.json` → into: `characters/[CHAR_ID]/`
- `prompts/*.txt` → into: `characters/[CHAR_ID]/prompts/`
```

---

# 📜 Generic `character_json_schema.json`

Use this to validate your character JSONs:

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Character Definition",
  "type": "object",
  "properties": {
    "character_core": {
      "type": "object",
      "properties": {
        "character_id": { "type": "string" },
        "name": { "type": "string" },
        "age": { "type": "number" },
        "role_in_story": { "type": "string" },
        "genre_style": { "type": "string" }
      },
      "required": ["character_id","name","role_in_story"]
    },
    "personality_profile": {
      "type": "object",
      "properties": {
        "key_traits": { "type": "array", "items": { "type": "string" } }
      }
    },
    "visual_identity": {
      "type": "object"
    },
    "expressions": {
      "type": "object",
      "properties": {
        "list": { "type": "array", "items": { "type": "string" } }
      }
    },
    "poses": {
      "type": "object"
    },
    "prompt_templates": {
      "type": "object"
    }
  },
  "required": ["character_core","visual_identity"]
}
```

This schema gives you:

* JSON validation support
* IDE autocompletion
* Consistency across characters

---

# 🧠 Universal Prompt Template (`templates/prompt_template.txt`)

This is a *real template* you’ll reuse every time:

```
Produce a character design in [VISUAL_STYLE] for a [GENRE] project.

Character: [NAME]
Role: [ROLE]

Visual Summary:
- Age: [AGE]
- Ethnicity: [ETHNICITY]
- Body language signature: [POSES_LIST]
- Expression signature: [EXPRESSIONS_LIST]
- Key identifiers: [CONSISTENCY_TOKENS]

Generate output files:
- Full JSON character definition
- Character sheet prompt
- Expression sheet prompt
- Pose sheet prompt
- Sticker pack prompt

Use consistent style, warm lighting, and gameplay/production compatibility.
```

The generator will replace:

* `[NAME]`
* `[ROLE]`
* `[VISUAL_STYLE]`
* etc.

---

# 📌 One-Shot Request Template (copy this into Discord/ChatUI/your tool)

```
CreateCharacter(
  character_name: "NAME",
  visual_style: "STYLE",
  genre: "GENRE",
  narrative_role: "ROLE",
  biological_data: {
    age: NUMBER,
    ethnicity: "ETHNICITY"
  },
  narrative_archetype: "ARCHETYPE",
  required_outputs: [
    "character_json",
    "character_sheet_prompt",
    "expression_sheet_prompt",
    "pose_sheet_prompt",
    "sticker_pack_prompt"
  ],
  plot_reference?: plotJson
)
```

---

# 📌 Quick Tips

✔ Character IDs should be UPPER_SNAKE_CASE
✔ JSON folder and img outputs should match IDs
✔ Prompts should live as plain `.txt`
✔ Validate with the JSON Schema before generating assets
✔ You can include `plot_reference` to auto link relationships

---

# 🚀 Why this works

This structure lets you:

✅ Automatically generate prompts and JSON from a single request
✅ Keep Studio Ghibli *and other visual styles* in the same engine
✅ Scale up to 50+ characters with consistent naming
✅ Integrate into your *plot engine* so character arcs connect cleanly

This workflow is **modular, scalable, and easy to automate**.

---

