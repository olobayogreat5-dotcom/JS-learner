# JS Quiz Builder

An interactive, browser-based tool for turning HTML snippets into fill-in-the-blank JavaScript quizzes. Paste in HTML, write the JS that powers it, mark key tokens as blanks, and quiz yourself on the result — all client-side, no backend required.

## Features

- **HTML input panel** — paste any HTML markup as the basis for a quiz block
- **Multiple JS blocks per quiz** — split a page into 2–4 distinct interactive behaviors (clicks, form submissions, toggles, etc.)
- **Mark-as-blank editor** — select any token in your JS and convert it into a quiz blank
- **Quiz mode** — renders each block with input fields in place of blanks, scores answers, and shows pass/fail percentage
- **Save / load quizzes** — store multiple quizzes locally and reload them from a saved-quiz modal
- **Import / export JSON** — share quizzes as a single `quizzes.json` file
- **AI-assisted quiz generation** — use the included prompt template to have an AI generate new quiz entries from raw HTML at Easy, Medium, or Hard difficulty

## Getting Started

1. Open `html-js-quiz.html` in any modern browser — no build step or server needed.
2. Paste HTML into the left panel and click **+ Add Block** for each interactive section you want to quiz.
3. Write the JavaScript for each block in its editor tab.
4. Select tokens in the JS and mark them as blanks.
5. Click **Start Quiz ▶** to test yourself, or **Save Quiz** to store it for later.

## AI-Assisted Quiz Creation

`quiz-prompt.md` contains instructions for an AI assistant to generate new quiz entries automatically:

1. Set the desired difficulty (`Easy`, `Medium`, or `Hard`) at the top of `quiz-prompt.md`.
2. Send the prompt along with an HTML file to an AI assistant.
3. The AI identifies 2–4 interactive blocks, writes the corresponding JS, blanks out tokens based on difficulty, and appends a new quiz entry to `quizzes.json` without modifying existing entries.

| Difficulty | Blanked tokens |
|---|---|
| Easy | Core DOM basics — `getElementById`, `addEventListener`, `value`, `innerHTML`, `textContent`, common event names (2–3 blanks/block) |
| Medium | Easy + `createElement`, `appendChild`, `classList.toggle`, `preventDefault`, operators like `+=` (3–5 blanks/block) |
| Hard | Medium + `parentElement`, `querySelectorAll`, `dataset`, `eval`, string literal values, exact arguments (5–7 blanks/block) |

## quizzes.json Format

Each quiz is an object with an `id`, `name`, `createdAt` timestamp, the original `htmlSource`, and a list of `blocks`. Each block contains alternating `text` and `blank` segments that reconstruct the JS code, with `blank` segments holding the exact (case-sensitive) answer.

```json
{
  "version": 1,
  "quizzes": [
    {
      "id": "unique_snake_case_id",
      "name": "Human-readable quiz name",
      "createdAt": "ISO 8601 timestamp",
      "htmlSource": "...",
      "blocks": [
        {
          "id": 1,
          "color": "#6366f1",
          "htmlSnippet": "<button id=\"myBtn\">",
          "segments": [
            { "type": "text", "content": "document.getElementById(\"myBtn\")." },
            { "type": "blank", "content": "addEventListener" },
            { "type": "text", "content": "(\"click\", function() { ... });" }
          ]
        }
      ]
    }
  ]
}
```

## Included Sample Quizzes

- **DOM Manipulation Basics** — button clicks, form submission, show/hide toggle
- **To-Do List** — adding items, toggling done state, deleting items
- **Calculator** — display input, clear, and evaluate logic

## File Structure

```
.
├── html-js-quiz.html   # Main app — open this in your browser
├── quiz-prompt.md      # AI prompt template for generating new quizzes
└── quizzes.json        # Saved quiz data
```

## Roadmap

- **Multi-language support** — extend the quiz builder beyond JavaScript to support HTML, Java, Python, and other languages, allowing fill-in-the-blank quizzes for a wider range of programming concepts and courses.

## License

No license specified — add one if you plan to distribute this project.
