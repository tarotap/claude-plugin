---
name: tarot-reading
description: Give a tarot reading with real cards the user draws by hand. Use when the user asks for a tarot reading, a tarot spread such as a Celtic Cross or past-present-future, a card of the day, or wants cards drawn about a question or decision.
---

# Tarot reading with Tarotap

Tarotap is a connector with two tools. `list_spreads` returns the available
spreads. `draw_cards` shuffles a full 78-card Rider-Waite-Smith deck and opens
a card table in the conversation, where the user picks their own cards. Where
the card table cannot be shown, `draw_cards` draws the cards itself and
returns them in the result. Use these tools for every reading. Never name or
invent cards from memory.

If the Tarotap tools are not available, tell the user to open this plugin's
Connectors tab, connect Tarotap (it needs no sign-in), and ask again.

## 1. Settle the question

A reading needs a question to read against. If the user gave one, use it. If
they only asked for "a reading", ask once what it is about. A card of the day
needs no question.

## 2. Choose the draw

- The user named a spread: call `list_spreads`, find it, and use its `id`.
- The user asked what spreads exist: call `list_spreads` and present the
  options with their number of cards and positions.
- The user left it open: call `list_spreads` and choose the spread whose name
  and tagline fit the question. Several spreads are made for one kind of
  question, such as a lost item, a job search, whether someone will get in
  touch, or a yes-or-no decision. Say why you chose it in one sentence. If none
  fits, use `time-flow` (past, present, future) for a general question and
  `celtic-cross` when they ask for depth. For a card of the day or a quick
  answer, use a single card (`card_count: 1`).
- The user asked for a number of cards without a spread: pass `card_count`
  (1 to 10).

## 3. Draw

Call `draw_cards` with the `spread_id` or the `card_count`.

Pass `locale` as the language the user is writing in, so the card table, the
position names and the card names match the conversation. Supported values:
`en`, `zh-CN`, `zh-TW`, `ja`, `ko`, `es`, `de`, `pt`, `fr`, `it`, `nl`, `ru`,
`uk`, `he`, `th`, `tr`, `pl`, `da`, `no`, `vi`, `hu`, `fi`, `id`. Use `en` for
any other language.

Check the `status` in the result.

- `status: "face_down"`, or a result that says no cards have been drawn yet:
  the result does not contain the cards. The deck is face down and the user
  has not drawn yet. Reply with one short sentence inviting them to draw, and
  stop there. Do not describe, guess or interpret any card. Then follow
  section 4.
- `status: "drawn"`, or a result that lists the drawn cards: no card table is
  shown. The `cards` in the result are the draw, in position order. Each has a
  `name`, a `reversed` flag and, except in a free-form draw, a `position`. Do
  not ask the user to draw or to send anything. Go straight to section 5 and
  read these cards.

## 4. Wait for the cards

After a `face_down` result, the user draws in the card table. When the user
has turned over the last card, the card table puts a message in their reply
box that lists each position with its card, and marks reversed cards. The user
sends it.

The only source of truth for what was drawn is that message after a
`face_down` result, and the `cards` in the tool result after a `drawn` result.

If the user writes again before that message arrives, ask them to finish
drawing in the card table and send the message it prepares. In either case, do
not call `draw_cards` again for the same reading.

## 5. Read the spread

Read in the user's language, against their question.

1. Open with one or two sentences on the spread as a whole.
2. Go position by position. For each card: what the position asks, what this
   card says there, and how a reversal changes it. Tie it to the question
   instead of reciting a generic meaning.
3. Look across the cards: repeated suits or numbers, a run of Major Arcana,
   several reversals, cards that answer or contradict each other.
4. Close with what the reading suggests the user consider or do next.

Keep the tone warm and direct. Tarot is a way to reflect on a question, not a
forecast: describe tendencies and choices, not fixed outcomes. For health,
legal or money questions, read the cards as a prompt for reflection and say
that the decision itself belongs with a qualified professional.

## 6. Afterwards

Follow-up questions use the cards already drawn. Draw again only when the user
asks for a new reading or a new question.
