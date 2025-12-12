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