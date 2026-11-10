# Marvel Champions LCG — Collection, Deck & Game Tracker

An Excel workbook that works like a small relational database for *Marvel Champions: The Card Game*. It tracks a full collection, every game played, every deck built, and full campaign progress, then rolls it all up into live dashboards: overall progress, hero-vs-villain results, deck win rates, and per-deck card breakdowns.

No macros or VBA. Everything runs on formulas, named ranges, and data validation.

## By the numbers

- **22 tabs** linked by shared keys (product, hero, villain, deck, and card names)
- **~10,000 formulas** driving the dashboards, all updating live as games are logged
- **~4,000-card reference database**: 1,700+ player cards and 2,200+ encounter cards
- **140 products** tracked across the Core Set and 11 release cycles
- **10 campaign logs**, one per campaign expansion

## How it fits together

| Layer | Tabs | Purpose |
|---|---|---|
| Reference data | Player Cards, Villain Cards, Card Lookup, Reference Lists | Card database and the master lists of heroes, villains, and cards that feed every dropdown |
| Input | Master Checklist, Skirmish Log, Decks, Deck Cards, 10 campaign tabs | Where data is entered, almost entirely through dropdowns |
| Analysis | Dashboard, Hero vs Villain Matrix, Deck Dashboard | Formula-driven summaries and charts |

**Data flow:** a game logged in the Skirmish Log (date, difficulty, up to 4 heroes and their decks, villain, result) instantly updates the Dashboard's win rate, every deck's record on the Decks tab, and the hero-vs-villain results in the Matrix. Cards added to a deck on Deck Cards automatically pull in their type, aspect, cost, and card text from the card database.

## Highlights

**Hero vs Villain Matrix:** a 51-hero × 60-villain grid showing net wins (wins minus losses) for every matchup. Each cell is a SUMPRODUCT that checks all four hero slots in the Skirmish Log, so a hero counts no matter which seat they played in. A color scale makes strong and weak matchups visible at a glance.

**Deck Dashboard:** pick any deck from a dropdown and the sheet rebuilds itself: full card list, card type breakdown, aspect breakdown, and cost curve, each with its own chart. The card list uses a helper column with SMALL and INDEX to pull only the selected deck's rows, a filter built without Excel's newer dynamic array functions.

**Deck win rates:** each deck's games played, wins, losses, and win % are calculated from the Skirmish Log, across all four player slots.

**Chained lookups:** each card in a deck goes through two INDEX/MATCH steps, from its display label to its canonical card name, then into the full card database for cost and card text.

## Skills demonstrated

- Relational data modeling inside a spreadsheet (separate reference, input, and analysis layers)
- Lookups: nested INDEX/MATCH with IFERROR handling
- Aggregation: SUMPRODUCT with multiple conditions, SUMIFS, COUNTIFS
- Dynamic filtered lists with helper columns, SMALL, and INDEX
- Data validation dropdowns driven by named ranges for consistent entry
- Conditional formatting (color scales) and Excel charts (bar and pie)
- Dashboard design for a non-technical user

## How to use

1. Download `Marvel_Champions_Log.xlsx` and open it in Excel.
2. **Master Checklist:** mark each product as Owned (Y/N) and Played (Not Started / In Progress / Completed), with a date and notes.
3. **Decks and Deck Cards:** add a deck on the Decks tab, then list its cards on Deck Cards. Type, aspect, cost, and text fill in automatically.
4. **Skirmish Log:** log each game. Dashboards, deck records, and the matrix update on their own.
5. **Campaign tabs:** track each campaign scenario by scenario, including boons, banes, and story choices carried forward.
6. **Deck Dashboard:** choose a deck in cell B1 to see its breakdown.

**Suggested play order:** play each Campaign Expansion start to finish before moving to the next cycle, and slot that cycle's Hero and Scenario Packs around it.

## Keeping it current

Content is current through Cycle 11 / *Fear No Evil* (mid-2026). Add new products as rows at the bottom of the Master Checklist, and new heroes or villains to Reference Lists. Extend the named ranges if new rows fall outside them.

## Possible next steps

- Win rate by difficulty level and by aspect
- Progress over time using the completion dates
- Rebuilding the data model in SQL to compare the spreadsheet and database approaches

---

*Fan-made project, not affiliated with Fantasy Flight Games or Marvel. Card data sourced from MarvelCDB.*
