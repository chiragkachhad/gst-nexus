GST Nexus — GSTR-2A / 2B ↔ Books Reconciliation
World-class, offline, audit-ready ITC reconciliation for Indian GST.

Match purchase books from any accounting software against:

Source	Role
GSTR-2B	Static monthly ITC statement — claimable base (Sec 16(2)(aa))
GSTR-2A	Dynamic supplier filings — follow-up & early visibility
Books	Tally / Zoho / Busy / Marg / SAP / QuickBooks / Vyapar / Excel
Open the tool
text

gstr2b_recon/
├── index.html              ← open in Chrome / Edge
├── lib/
│   └── xlsx.full.min.js    ← required (Excel support)
├── sample_data/
│   ├── tally_purchases.csv / .xlsx
│   ├── gstr_2b_sample.json / .xlsx
│   └── gstr_2a_sample.json
└── README.md
Copy the whole folder. index.html alone will not load Excel support.

Modes
2B ↔ Books — filing-ready ITC for GSTR-3B (recommended monthly)
2A ↔ Books — live supplier follow-up
2A + 2B + Books — three-way nexus (best audit view)
2A ↔ 2B only — portal gap analysis
Supported books software
Software	How to export
TallyPrime / Tally Cloud	Purchase Register → Excel/CSV
Zoho Books	Reports → Bills → Export
Busy	Purchase register export
Marg ERP	Purchase bill register
SAP / Oracle	Vendor invoice extract with GSTIN
QuickBooks	Expense/Bill report CSV
Vyapar / myBillBook	Purchase report Excel
Any custom Excel	GSTIN + Invoice No + Taxable + Tax columns
Header names are fuzzy-mapped (dozens of aliases). Use the software preset dropdown for better mapping.

Minimum columns in books file
Supplier GSTIN
Invoice / Bill number
Invoice date
Taxable value
IGST and/or CGST + SGST
Optional: Party name, Invoice value, RCM, Voucher type (for credit notes), Place of supply.

Portal downloads
GSTR-2B
gst.gov.in → Returns Dashboard → period → GSTR-2B → Download Excel or JSON
(Available ~14th of next month)

GSTR-2A
Same portal → GSTR-2A → Download Excel/JSON

Portal multi-sheet Excel (B2B, B2BA, CDNR, IMPG, ISD…) is auto-parsed.

What makes it “world-class”
Three-way presence (Books · 2A · 2B) with source dots on every row
Smart invoice normalization (case, spaces, special chars, optional FY prefix strip)
Probable matching (GSTIN + invoice core + amount)
Strict / Smart / Loose match strength
Amount & date tolerance
Credit / debit notes & RCM flags
ITC control KPIs: Claimable · Hold · 2A-not-2B · Investigate
Supplier risk scorecard
Ready supplier follow-up messages
Multi-sheet Audit Excel workpaper with sign-off
100% offline — data never uploaded
Status legend
Status	Meaning	ITC action
MATCHED_ALL	Books + 2A + 2B	Claim (other Sec 16 conditions)
MATCHED_2B	Books + 2B	Claim for GSTR-3B
IN_2A_NOT_2B	Books + 2A, missing 2B	HOLD until in 2B
VALUE_MISMATCH / TAX_MISMATCH	Amount differences	Resolve before claim
DATE_MISMATCH	Values OK, date differs	Verify invoice
PROBABLE_MATCH	Partial invoice match	Manual confirm
ONLY_IN_BOOKS	Not on portal	HOLD + supplier follow-up
ONLY_IN_2B / ONLY_IN_2A	Not in books	Investigate booking
Quick demo
Open index.html
Click Load Sample Demo (loads three-way 2A+2B+Books sample)
Review dashboard → Export Audit Excel
Sample highlights:

Clean matches (Acme, Bharat, …)
Value mismatch (Coromandel)
Date mismatch (Delta)
Only in books HOLD (Indigo, Jupiter)
In 2A not 2B (Eagle Logistics)
Only in 2B (Zenith)
Only in 2A (Acme INV-2026-004)
Exports
Button	Output
Audit Excel	Dashboard, All, Claimable, Hold, Portal-only, Supplier scorecard, Follow-up, Methodology
Detail CSV	Flat line-level file
JSON Pack	Full machine-readable pack
Supplier Follow-up	CSV of messages to send vendors
Python CLI (optional batch / server)
Bash

python3 app.py \
  --books sample_data/tally_purchases.csv \
  --gstr2b sample_data/gstr_2b_sample.json \
  --out output \
  --company "Your Co" \
  --gstin 24XXXX \
  --period Apr-2026
Requires openpyxl for Excel audit generation.

Audit checklist
 Original GSTR-2B download retained
 Optional GSTR-2A download retained
 Books export for same period retained
 Nexus audit Excel filed with sign-off
 ONLY_IN_BOOKS / IN_2A_NOT_2B suppliers contacted
 ONLY_IN_2B invoices booked or marked N/A
 GSTR-3B ITC ≤ claimable matched ITC
 Preparer / Reviewer signed Dashboard sheet
Limitations
Does not verify actual receipt of goods/services or supplier tax payment
Sec 17(5) blocked credit & Rule 42/43 need separate workings
RCM cash tax liability is separate from this ITC match
Not a substitute for professional tax advice
Version
GST Nexus v2.0 — GSTR-2A / 2B ↔ Books · multi-software · offline audit engine
