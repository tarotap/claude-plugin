# Tarotap

Tarot readings in Claude with real cards. Tarotap shuffles a full 78-card
Rider-Waite-Smith deck, lays it face down in the conversation, and lets you
draw your own cards. Claude then reads the spread against your question.

## What's in the plugin

- **The Tarotap connector.** It deals the cards and shows the card table. It
  needs no account and no sign-in.
- **The `tarot-reading` skill.** It teaches Claude how to run a reading: settle
  the question, choose a spread, wait for your draw, and interpret the cards
  position by position.

## Use it

After you add the plugin, open its Connectors tab and connect Tarotap. Then ask
for a reading, for example:

```
Do a Time Flow tarot reading about my career this year.
```

```
Draw my tarot card of the day.
```

```
Use the Celtic Cross to look at my relationship.
```

The deck appears face down. Drag to browse it and tap the cards you want. When
the last card is turned over, a message listing your cards appears in the
reply box. Send it, and Claude reads the spread.

There are 14 spreads, from a three-card past, present and future to the
ten-card Celtic Cross, and you can ask for any number of cards from one to
ten. Write in your own language and the card table follows.

The full guide is at https://tarotap.com/en/blog/claude-tarot-reading-guide

## Data

The connector at tarotap.com receives the spread, the number of cards and the
language. It never receives your question or your conversation, it has no user
accounts, and it stores nothing about the draw. Card images load from
tarotap.com. The plugin itself runs no code on your computer.

Privacy policy: https://tarotap.com/en/privacy-policy

## Support

https://tarotap.com/en/contact

## License

MIT
