# VendorFlow AI — Vendor Onboarding & Verification

A browser-based PS-2 vendor onboarding prototype. It collects vendor details and five supporting documents, runs transparent deterministic checks, shows processing stages, explains the decision, and stores a local run history.

## Live application

https://karthikeyavarmap.github.io/vendorflow-ai/

## Run the demo

1. Open the live application.
2. In the **Demo test cases** selector, choose one of the five scenarios.
3. Click **Load selected test**. The form and synthetic TXT documents are populated for that scenario.
4. Click **Run verification**.
5. Review the status, reasons, pipeline stages, and (optionally) the **Run history** tab.
6. Repeat with another scenario.

You can also fill in your own synthetic vendor details and upload PDF or TXT evidence. The built-in sample data is fictitious and uses the reserved `.example` email domain.

## Built-in test scenarios

| Scenario | Expected result | What it demonstrates |
|---|---|---|
| All valid | APPROVED | Complete evidence and matching values |
| Missing compliance declaration | PENDING | Required evidence is absent |
| Invalid PAN | REJECTED | PAN format validation fails |
| Bank account-holder mismatch | PENDING | Name discrepancy is routed for review |
| Invalid IFSC | REJECTED | IFSC format validation fails |

See [TEST_CASES.md](TEST_CASES.md) for the reproducible test procedure and expected reasons.

## What the prototype checks

- Required company, contact, tax and banking fields.
- PAN, GSTIN structure, PAN-to-GSTIN consistency, IFSC, account number, email and phone formats.
- Presence and text readability of five evidence types: company registration proof, PAN document, GST certificate, bank proof and compliance declaration.
- Whether extracted document text visibly contains submitted company/tax/bank values.
- Company legal name versus bank account-holder name, routed to manual review when they differ.
- A transparent outcome: **APPROVED**, **PENDING**, or **REJECTED**, with reasons and follow-up guidance.
- A five-stage verification pipeline and browser-local submission history (up to 50 runs).

## Technology

- HTML, CSS and vanilla JavaScript.
- PDF.js for extracting selectable text from PDFs.
- Browser File API and localStorage.
- GitHub Pages static hosting; no build step or application server is required.

## Important limitations and privacy

- The current implementation uses deterministic rules; it is not a generative-AI model.
- This is a decision-support prototype, not a production KYC, legal, tax, sanctions, credit, fraud-screening or bank-account verification service.
- It does not connect to MCA, GSTN, Income Tax, banks, payment networks or external registries. A text match does not prove that a document is authentic or that a bank account belongs to the vendor.
- Scanned/image-only PDFs may not yield selectable text and should be manually reviewed.
- Uploaded files are processed in the browser and are not sent to a server. Run summaries are stored in localStorage in the current browser only and do not sync across devices.
- Use synthetic data only. Do not upload real identity, tax or banking documents.

## Repository files

- `index.html` — complete static application, styles, form, sample scenarios, document extraction and decision rules.
- `TEST_CASES.md` — test scenarios, steps and expected outcomes.
