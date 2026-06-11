# JS Quiz Builder — AI Instructions

You are helping build a JavaScript fill-in-the-blank quiz. When the user sends you an HTML file, generate a quiz entry and add it to `quizzes.json`.

---

## Difficulty Setting

**Set the difficulty here before sending to an AI:**

```
DIFFICULTY: Easy
```

> Change `Easy` to `Medium` or `Hard` as needed.

| Level  | What gets blanked |
|--------|-------------------|
| Easy   | Only the most common, essential JS tokens — `getElementById`, `addEventListener`, `value`, `innerHTML`, `textContent`, common event names (`click`, `submit`). 2–3 blanks per block. |
| Medium | Everything in Easy, plus methods like `createElement`, `appendChild`, `classList.toggle`, `preventDefault`, operators like `+=`. 3–5 blanks per block. |
| Hard   | Everything in Medium, plus less obvious tokens — `parentElement`, `querySelectorAll`, `dataset`, `eval`, property values like `""` or `"none"`, and exact string arguments. 5–7 blanks per block. |

---

## Your Task

1. Read the HTML file the user provides.
2. Identify **2–4 distinct interactive blocks** (e.g. a button click, a form submission, an input event, a toggle).
3. For each block, write the complete JavaScript that makes it work.
4. Apply blanks based on the difficulty level above.
5. Add the new quiz to the `quizzes` array in `quizzes.json` — **do not remove or modify existing quizzes**.
6. Return the **full updated `quizzes.json`** file content.

---

## quizzes.json Schema

```json
{
  "version": 1,
  "quizzes": [
    {
      "id": "unique_snake_case_id",
      "name": "Human-readable quiz name",
      "createdAt": "ISO 8601 timestamp",
      "htmlSource": "the full HTML string (escape quotes)",
      "blocks": [
        {
          "id": 1,
          "color": "#hexcolor",
          "htmlSnippet": "short label showing which HTML element this JS is for",
          "segments": [
            { "type": "text",  "content": "code before the blank" },
            { "type": "blank", "content": "exact answer that goes here" },
            { "type": "text",  "content": "code after the blank" }
          ]
        }
      ]
    }
  ]
}
```

### Segment rules
- Alternate `text` and `blank` — never two `blank` entries in a row.
- A `text` segment can contain `\n` for line breaks.
- A `blank` content is the **exact string** the user must type to pass — case-sensitive.
- Keep each block focused on one function or behavior.
- Use these colors in order for blocks: `#6366f1`, `#f59e0b`, `#22c55e`, `#ec4899`, `#14b8a6`.

### ID rules
- Use a short descriptive snake_case string, e.g. `calculator_quiz`, `todo_list_quiz`.
- Never reuse an ID already present in the file.

---

## Example

HTML sent by user:
```html
<button id="myBtn">Click</button>
<p id="out"></p>
```

Correct quiz entry (Medium difficulty):
```json
{
  "id": "button_click_quiz",
  "name": "Button Click",
  "createdAt": "2026-06-11T00:00:00.000Z",
  "htmlSource": "<button id=\"myBtn\">Click</button>\n<p id=\"out\"></p>",
  "blocks": [
    {
      "id": 1,
      "color": "#6366f1",
      "htmlSnippet": "<button id=\"myBtn\">",
      "segments": [
        { "type": "text",  "content": "document.getElementById(\"myBtn\")." },
        { "type": "blank", "content": "addEventListener" },
        { "type": "text",  "content": "(\"click\", function() {\n  document.getElementById(\"out\")." },
        { "type": "blank", "content": "innerHTML" },
        { "type": "text",  "content": " = \"Clicked!\";\n});" }
      ]
    }
  ]
}
```

---

## Checklist before returning

- [ ] Difficulty level applied correctly
- [ ] No two `blank` segments are adjacent
- [ ] Every blank answer is the exact token the user must type
- [ ] Existing quizzes in the file are untouched
- [ ] Output is valid JSON
