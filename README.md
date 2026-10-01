# Spendbook

A personal spend tracker in a single HTML file. Upload bank and credit card statements (CSV, Excel or PDF), and Spendbook sorts every transaction into categories and shows where the money went.

## Features

- **Statement import**: CSV, `.xls`/`.xlsx` and PDF (including password-protected PDFs), read in the browser. Columns are detected automatically and can be adjusted before importing. Duplicate rows are skipped.
- **Card picker**: each statement is tagged with the card or account it came from (Amex Gold Delta, Chase Sapphire, Chase Freedom Unlimited, Chase checking, Amex Blue Cash, Costco Citi Advantage, or another name).
- **Categories**: House, Car, Groceries, Gas + Costco, Travel, Dining Out + Entertainment, Utilities and Misc., plus Income, Investments and Transfers, which are kept out of spend. Unrecognised merchants are flagged for review. Settings → *How sorting works* lists every keyword.
- **Rules and bulk editing**: change one transaction or many at once, and optionally remember the choice for that merchant.
- **House cost sheet**: reads the "House cost" tab of a Google Sheet through the Google Drive connector. Bank payments that repeat a sheet entry are marked *In house sheet* and not counted twice.
- **Dashboards**: overall spend by category, a monthly chart with toggles for each category and an income line, spend by card, top merchants, and the 3 biggest costs in each category.
- **Recurring charges**: detects subscriptions and bills, and flags price rises and charges that stopped.
- **Investments**: money moved to Robinhood, Schwab, Fidelity and others, plus account values you enter.
- **Transactions list**: search, filter by category or card, sort by date or amount, and see Db (debit) and Cr (credit) markers.

## Running it

Spendbook is built to run as a **Claude artifact**, where it gets:

- private storage in your Claude account (`db` and `user` capabilities)
- Claude for reading messy PDFs and receipts and sorting unrecognised merchants (`sample`)
- Google Drive access to read the house cost sheet (`mcp`)
- CSV export (`downloads`)

To publish your own copy, ask Claude to publish `spendbook.html` as an artifact with those capabilities.

Opened directly in a browser (double-click `spendbook.html`), it still works, with these differences:

- data is saved only in that browser (`localStorage`)
- the Claude features and the Google Sheet connection are hidden
- CSV export downloads a file directly

## Libraries

Loaded from cdnjs at runtime: [SheetJS](https://sheetjs.com/) 0.18.5 for Excel files and [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 for PDFs. Fonts come from Google Fonts.

## Privacy

No statement data is stored in this repository. The house cost sheet's Google file ID is in `spendbook.html` (`HOUSE_SHEET`); only people you've shared the sheet with can open it.
