# VendorFlow AI — Intelligent Vendor Onboarding

A browser-based prototype for PS-2 (Vendor Onboarding). It accepts vendor details and compliance documents, runs deterministic checks, displays each processing stage, explains the outcome, and keeps a browser-local run history.

## Run the application

**Option 1 — Run locally**
1. Download or clone this repository.
2. Open `index.html` in Chrome, Edge, or Firefox.
3. Click **Load sample case**, then **Run verification**.

No build step or server is required. An internet connection is needed for the PDF.js library used to extract text from PDF files. TXT documents work without PDF parsing.

**Option 2 — Publish with GitHub Pages**
1. Open this repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the `main` branch and `/(root)`, then save.
5. Wait for GitHub Pages to publish, then use the URL shown in Settings → Pages.

GitHub Pages publishes static files; this app deliberately uses browser-side JavaScript rather than a Python/server backend. See [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

## What it does

1. Collects legal name, business email, phone, PAN, GSTIN, bank account, IFSC and bank name.
2. Requires five evidence types: incorporation proof, PAN document, GST certificate, bank proof and compliance declaration.
3. Reads TXT files and extracts selectable text from PDFs in the browser (via PDF.js).
4. Checks required fields and identifier formats; checks the PAN embedded in the GSTIN; compares submitted values with text extracted from the relevant documents; flags a mismatch between company and account-holder names for review.
5. Returns **APPROVED**, **PENDING** or **REJECTED**, with reasons and a follow-up message.
6. Shows pipeline stages and stores the latest 50 run summaries in localStorage.

## Decision logic

- **REJECTED:** a critical identifier fails the configured format checks, or the PAN embedded in the GSTIN conflicts with the submitted PAN.
- **PENDING:** a required document is missing, unreadable, has no selectable text, or does not visibly match a submitted value; a bank account-holder/company-name difference is also routed for review.
- **APPROVED:** all required evidence is present and readable, and the configured checks find no issues.

A decision is based on transparent rules in `index.html`, not a generative AI model. “AI” is the product concept/name; the current implementation is deterministic and explainable.

## Important scope and privacy limits

- This is a decision-support demonstration, not a real KYC, legal, tax, sanctions, credit or fraud-screening service.
- It does **not** connect to MCA, GSTN, Income Tax, banks, payment networks or external registries. It cannot confirm that a company exists or that an account is owned by the vendor.
- PDF text extraction cannot reliably read scanned/image-only PDFs; those are routed to manual review. TXT is supported for test fixtures.
- Uploaded files are processed in the browser and are not sent to a server. Run summaries (vendor name, email, status, reasons and timestamp) are stored in the current browser's localStorage. Do not upload real sensitive documents or real banking information to this demo.
- Use synthetic data only. Browser-local history is not a secure production database and does not sync across devices.

## Demo checklist

1. Load the built-in sample case and run it (happy path).
2. Remove one required document and run again (pending).
3. Change the PAN while leaving the GSTIN unchanged (rejected for PAN/GSTIN inconsistency).
4. Upload a scan-only PDF or a TXT file with conflicting identifiers (pending/manual review).
5. Open **Run history** to show the saved decision and reason trail.

See [TEST_CASES.md](TEST_CASES.md) for reproducible scenarios.

## Files

- `index.html` — complete static application, styles, form, document extraction and decision rules.
- `TEST_CASES.md` — edge-case walkthrough and expected outcomes.
