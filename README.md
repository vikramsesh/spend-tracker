# Spendbook

A personal spend tracker in a single HTML file. Upload bank and credit card statements (CSV, Excel or PDF), and Spendbook sorts every transaction into categories and shows where the money went. Two or more people can share one book, see each other's changes live, and edit it together.

## Features

- **Statement import**: CSV, `.xls`/`.xlsx` and PDF (including password-protected PDFs), read in the browser. Columns are detected automatically and can be adjusted before importing. When a file's amounts could mean either direction, you're asked whether negative numbers are credits or debits. Rows already imported for the same card are skipped.
- **Card picker**: each statement is tagged with the card or account it came from.
- **Categories**: House, Car, Groceries, Gas + Costco, Travel, Dining Out + Entertainment, Utilities and Misc., plus Income, Investments, Transfers and In house sheet, which are kept out of spend. Unrecognised merchants are flagged for review. Settings explains what each category means and lists every keyword.
- **Rules and bulk editing**: change one transaction or many at once, and optionally remember the choice for that merchant.
- **Repeated charges**: the same amount at the same merchant within 3 days, on any card, is flagged so you can check for double charges.
- **House cost sheet**: reads a "House cost" tab from a Google Sheet. Card charges that may already be in the sheet are shown next to the matching sheet row, and you decide whether each one is the same payment before it's left out.
- **Dashboards**: overall spend by category, a monthly chart with toggles for each category and an income line, spend by card, top merchants, and the 3 biggest costs in each category.
- **Recurring charges**: detects subscriptions and bills, and flags price rises and charges that stopped.
- **Investments**: every investment transaction is assigned to an account you choose, alongside account values you enter.
- **Transactions list**: search; filter by category, card, date range and amount range; sort by date or amount; debit and credit totals for whatever is shown.
- **Change history and undo**: every change is recorded with who made it, and any change can be undone (Undo button or Ctrl+Z).

## Running it

### On its own

Open `spendbook.html` in a browser. Data is saved only in that browser (`localStorage`), and sharing, change history and the Google Sheet connection are off.

### Shared online

Spendbook can use Firebase for sign-in and a shared database, and be hosted on any static site host such as GitHub Pages.

1. Create a Firebase project. Enable **Authentication → Google** and create a **Firestore** database in production mode.
2. Copy `firestore.rules` into **Firestore → Rules**, put the Google accounts that may use the book in the list, and publish.
3. Register a web app in **Project settings** and paste its `apiKey`, `authDomain`, `projectId` and `appId` into `FIREBASE_CONFIG` in `spendbook.html`. These values identify the project and aren't secret; the rules decide who can read and write.
4. Host the file (e.g. GitHub Pages) and add the site's domain under **Authentication → Settings → Authorized domains**.
5. To read a house cost sheet, enable the **Google Sheets API** for the same project in Google Cloud, set the sheet's ID and tab name in `HOUSE_SHEET`, and share the sheet with each person who will refresh it.

## Libraries

Loaded at runtime: [SheetJS](https://sheetjs.com/) 0.18.5 for Excel files, [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 for PDFs and the [Firebase](https://firebase.google.com/) JavaScript SDK 10.14.1 for sign-in and storage. Fonts come from Google Fonts.

## Privacy

Statements, exports and other data files are excluded by `.gitignore`, so no financial data is stored in this repository. In shared mode, data lives in your own Firebase project and can only be read by the accounts listed in your Firestore rules.
