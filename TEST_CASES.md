# VendorFlow AI — Reproducible test cases

Use synthetic data only. These scenarios are built into the live application so they can be loaded without manually editing fields.

## How to run any scenario

1. Open https://karthikeyavarmap.github.io/vendorflow-ai/
2. In the **Demo test cases** selector, choose a scenario.
3. Click **Load selected test**.
4. Click **Run verification**.
5. Confirm the expected decision and review the reasons shown below it.
6. Open **Run history** to see the saved run.

Each time you load a scenario, the app fills the vendor fields and generates the sample TXT files locally in the browser. Loading a scenario does not submit or save a verification; click **Run verification** to execute it.

## Scenario 1 — Happy path (APPROVED)

- Select **Test 1 · All valid (APPROVED)**.
- Load selected test, then run verification.
- Expected: **APPROVED**.
- Expected evidence: all five documents are present, text is readable, and configured identifier/document checks pass.

## Scenario 2 — Missing compliance declaration (PENDING)

- Select **Test 2 · Missing compliance (PENDING)**.
- Load selected test, then run verification.
- Expected: **PENDING**.
- Expected reason: the compliance declaration is missing.

## Scenario 3 — Invalid PAN (REJECTED)

- Select **Test 3 · Invalid PAN (REJECTED)**.
- Load selected test, then run verification.
- Expected: **REJECTED**.
- Expected reason: PAN format is invalid. The built-in invalid value is deliberately too short.

## Scenario 4 — Bank account-holder mismatch (PENDING)

- Select **Test 4 · Bank name mismatch (PENDING)**.
- Load selected test, then run verification.
- Expected: **PENDING**.
- Expected reason: the bank account-holder name differs from the legal company name and needs confirmation.

## Scenario 5 — Invalid IFSC (REJECTED)

- Select **Test 5 · Invalid IFSC (REJECTED)**.
- Load selected test, then run verification.
- Expected: **REJECTED**.
- Expected reason: the IFSC format is invalid.

## Interpretation

These are deterministic prototype rules, not external verification. A matching string in a document does not prove authenticity; a failed text match may also be caused by OCR, formatting, abbreviations or document quality. In a real onboarding workflow, uncertain evidence should be routed to a human reviewer and trusted registry/bank integrations should be used only with appropriate authorization.
