# ChessTracker

A companion board for games played with real pieces on a real table.

Playing over the board means holding the whole position in your head: which
piece is where, what each one can reach, what you have already given up.
ChessTracker takes that load off. You play your move on the physical board,
tap the same move here, and the screen shows you the position, every legal
move for whatever piece you tap, and the running material count.

It is not an engine and it will not suggest moves. It is a mirror of your
board that knows the rules.

## What it does

- **Digital board** with the pieces drawn as clear symbols, in the familiar
  green-and-cream style.
- **Tap a piece to see every legal move.** Quiet moves appear as dots,
  captures as rings. Pins, checks, castling and en passant are all handled, so
  what you see really is what is legal.
- **Tap an opponent piece to preview its moves** in amber, without playing
  anything — useful for checking a threat before you commit.
- **Move recording** in standard notation (`e4`, `Nf3`, `O-O`, `exd5`,
  `hxg8=Q+`), numbered the way a scoresheet is.
- **Turns switch automatically**; the strip belonging to the side to move is
  outlined. Turn on *auto-flip* and the board rotates to face whoever is
  moving, which suits two people sharing one phone.
- **Take back a mistake** with the take-back button or `Ctrl`+`Z`. Step
  through the game with the arrow buttons, the arrow keys, or by tapping any
  move in the list.
- **Captured pieces and points.** Each player's strip shows the pieces they
  have taken and their material lead (`+3`), using the usual values —
  pawn 1, knight and bishop 3, rook 5, queen 9.
- **Game end is detected**: checkmate, stalemate, insufficient material,
  threefold repetition and the fifty-move rule.
- **Your game is saved in the browser.** Close the tab, come back, and the
  game is where you left it.
- **Copy PGN or FEN** to keep the game or drop the position into an analysis
  tool afterwards.

## Running it

There is no build step and no dependencies. Open `index.html` in a browser —
double-clicking the file works.

To serve it over HTTP instead:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

To put it online, upload the directory to any static host (GitHub Pages,
Netlify, S3 — anything that serves files).

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `←` / `→` | Step back / forward through the game |
| `Home` / `End` | Jump to the start / the latest move |
| `Ctrl`+`Z` | Take back the last move |
| `F` | Flip the board |
| `Esc` | Clear the current selection |

## Tests

The rules engine is covered by unit tests plus `perft` node counts for the
standard test positions, which is the usual way to prove move generation is
exactly right — castling rights, en passant, promotions and pinned pieces
included.

```sh
npm test
```

## Layout

```
index.html          markup for the board, panels and dialogs
css/styles.css      styling and the responsive layout
js/chess.js         the rules engine — no DOM, testable on its own
js/app.js           board rendering, tap handling, move list, storage
test/engine.test.js engine tests and perft
```

`js/chess.js` is self-contained: it knows nothing about the page and can be
reused anywhere. `js/app.js` never decides what is legal on its own; it always
asks the engine.
