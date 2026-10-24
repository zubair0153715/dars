# Dars درس — free AI study companion

Paste a lecture, chapter, or notes → get structured study notes, flashcards,
an auto-built quiz, and a spaced-repetition review queue. **Free, unlimited,
no account.**

An original, clean-room build — not affiliated with Coconote, Quizlet, or any
other study-notes product.

## Why it exists

AI study-notes apps (Coconote: $6.7M ARR, acquired by Quizlet) have public,
well-documented gaps:

1. **Paywall shrinkflation** — tiny free tiers, manipulative multi-discount
   pricing screens, broken subscription activation (public Play Store /
   justuseapp reviews).
2. **No spaced repetition** — the core learning-science loop (SM-2 scheduling)
   is missing, unlike RemNote/Memrizz.
3. **Fragile recording pipelines** — reviews report mid-session recording
   failures and corrupt files.
4. **Weak export** — flashcards stuck in a silo, no LMS integration.

Dars fills those: free + unlimited, SM-2 spaced repetition built in, works on
pasted/uploaded text (no fragile recorder), exports to Markdown and Anki-ready
CSV, and Urdu/Roman-Urdu/English support for real classrooms.

## Honest by design

- Rule-based engine is **extractive**: every note line, card back, and quiz
  stem is verbatim from your source text. Nothing is invented.
- Optional Gemini AI pack is **grounded**: it must quote/rephrase only your
  text, and says plainly when no API key is set instead of faking it.
- Stateless server: your text is never stored; SM-2 schedules live in your
  own browser (localStorage).

## Run the tests

```bash
python3 dars/tests/verify.py   # 61 checks: SM-2 math, extractive outputs, quiz logic, routes
```

Needs `fastapi` + `pydantic` installed for the route-registration checks.

## Deploy (as part of the host FastAPI app)

The live demo runs at `/dars` inside the clinic-demo FastAPI Cloud app.
`dars/` mirrors `app/dars/` there; `routes.py` exposes the `router`
(`APIRouter(prefix="/dars")`), registered in the host `main.py`.

## Layout

```
dars/
  __init__.py
  spaced.py    # SM-2 scheduler (the loop Coconote lacks)
  notes.py     # extractive notes: headings, definitions, key terms, summary
  quiz.py      # flashcards + MCQ/true-false builder from notes
  gemini.py    # optional AI study pack + grounded chat (key at call time)
  pages.py     # single-page UI (notes/cards/quiz/review tabs, exports)
  routes.py    # FastAPI router: /dars page + JSON APIs + .md/.csv downloads
  tests/verify.py
```

## License

MIT — do what you want, just don't blame me when your GPA goes up.
