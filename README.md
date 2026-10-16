# Picture Sudoku

A maker for printable sudokus for young kids (around age 5). Instead of the digits 1 to 9 the puzzles use
pictures (shapes, simple drawings, dice dots or small numbers) on small grids: 3 × 3, 4 × 4 or 6 × 6. The sheets
have no words, so they work for kids who can't read yet, and they're made for a black-and-white printer. The answer
is hidden in a QR code: scan it with a phone camera to see the puzzle solved.

Live at **https://tb-x.github.io/picture-sudoku/**

## How it plays

- Print a sheet. Above each grid is a row showing the pictures that puzzle uses.
- Every row, every column and every thick-lined box needs each picture once. The boxes are shaded grey in turn so
  they're easy to see. The 3 × 3 grid has no boxes, just rows and columns, which makes it a good first try.
- Draw the missing pictures in the empty squares (circle, square and triangle are easy to draw), or cut out the
  pieces printed beside or below the grid and glue them in. There's one piece for each empty square, the same size
  as a square, so all of them get used. Every picture is a black outline, so the pieces can be coloured in too.
- Scan the QR code next to the puzzle. The answer page shows the same puzzle solved, with the squares that were
  empty shaded yellow.

Every puzzle has exactly one answer, and it can be found without guessing:

- **Easy**: only "one square left in this row, column or box".
- **Medium**: also "only one picture fits in this square".
- **Hard**: also "this picture fits in only one square of the row, column or box".

## The maker page

- **Grid**: 3 × 3, 4 × 4 (2 × 2 boxes) or 6 × 6 (boxes 3 wide and 2 tall).
- **Level**: Easy, Medium or Hard. The number in brackets is how many squares are empty.
- **Pictures**: Shapes (circle, square, triangle, heart, star, diamond), Sun, fish, house… (sun, fish, house,
  tree, flower, moon), Dice dots, Numbers, or A mix (each puzzle gets its own set). A 3 × 3 grid uses the first
  three of a set, a 4 × 4 the first four. Each picture has its own outline, so nothing depends on colour.
- **Per page**: 1, 2, 4 or 6 puzzles on each A4 page. The squares are made as big as the page allows.
- **Cut-out pieces**: yes or no.
- **Pages**: how many pages to print at once (up to 20).
- **New puzzles** makes new puzzles for every page, ↻ on a page makes new ones for that page only, and
  **Print** prints them. Changing the pictures keeps the same puzzles. The settings are remembered in this browser.
- Clicking a QR code on screen opens its answer page.

Print at 100 % ("actual size"), not "fit to page", so the pieces fit the squares.

The QR code holds the whole puzzle in the link: the grid size, a letter for the pictures (s, t, d or n), then
each square row by row, a digit for a picture that's given and a letter for one that's left empty (a = 1, b = 2 …),
e.g. `#4s12c4341a…`. Nothing is stored anywhere, so a printed sheet keeps working for as long as this page is
online. The QR always points at the published page on GitHub Pages, even when the maker runs on a local server.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5214
```

Then go to http://localhost:5214/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | 4 × 4, Easy, shapes, 2 a page, pieces, 1 page | Starting settings |
| `LEVELS` | Easy, Medium, Hard | Level names |
| `BLANKS` | 3 × 3: 3/4/5, 4 × 4: 5/8/10, 6 × 6: 10/16/22 | Empty squares for each level |
| `SHEETS_MAX` | 20 | Most pages printed at once |
| `GRID` | 1, 2 (stacked), 4 (2 × 2), 6 (2 × 3) | How the puzzles sit on a page |
| `MAX_CELL` | 38 mm | Biggest square on the sheet |
| `PIC` | 0.74 | A picture's size, as a share of its square |
| `TRIES` | 40 | Fresh grids to try when a level's number of empty squares is hard to reach |
| `QR_MIN` / `QR_MAX` | 16 / 22 mm | Size of the answer QR code (it grows with the squares) |
| `PUBLIC_URL` | `https://tb-x.github.io/picture-sudoku/` | Where the QR codes point |
