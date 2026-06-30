This is a single self-contained HTML file — open it in any browser, no install. The accounting team drops in the daily Scully PDF (however many pages), reviews the table, and clicks Copy rows for Sigma, which puts tab-separated rows on the clipboard in the exact column order of AP_LEDGER_INPUT, ready to paste into the "Edit data" grid. There's also a CSV download. Everything parses locally in the browser — no upload.
A few things worth knowing about how I built it:
Two judgment calls I defaulted (both adjustable in "Defaults & rules"):

Amount = invoice Total, i.e. subtotal + freight + misc, not the subtotal. For invoice 1578478 that's 52.01, not 31.50. If you actually book freight/misc to separate GL lines, tell me and I'll split them out.
Date to Recognize Expense = invoice/ship date (2026-06-25), since dropship goods ship on the invoice date. You can switch it to the due date or blank. I went this way because your AP table had that column empty, suggesting it's currently hand-filled.

Things I detected vs. hardcoded: Brand is read from the billing block (Historical Emporium → HE); if a future page bills a different entity it falls back to your default and the row still shows. Vendor/currency are constants you can rename once. Memo defaults to PO — ship-to name (e.g. S6949-ALDRIDGE — TENN.HILLBILLY ALDRIDGE) for dropship traceability, with other formats in the dropdown.
The safety net: any row where invoice #, due date, or amount didn't parse gets highlighted amber and counted in the "need a look" pill, so nothing silently enters with a blank. Every cell is editable inline before you export.
