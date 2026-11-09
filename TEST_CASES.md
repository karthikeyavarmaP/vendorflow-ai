# VendorFlow AI — Test cases

Use synthetic information only. The built-in **Load sample case** button fills a known-good example and attaches five generated TXT fixtures to the matching document controls.

## 1. Happy path — complete evidence

- Click **Load sample case**.
- Click **Run verification**.
- Expected: **APPROVED**.
- Confirm the pipeline stages complete and the result explains the successful field/document checks.
- Open **Run history** and confirm the run appears.

The sample uses fictitious details and the reserved `.example` email domain.

## 2. Missing evidence — pending

- Load the sample case.
- Clear the **Compliance declaration** file input (select it and cancel, or use Clear form then reload the sample and clear this one).
- Run verification.
- Expected: **PENDING**, with the missing compliance declaration listed and a follow-up request.

## 3. Tax identifier conflict — rejected

- Load the sample case.
- Change PAN from `ABCDE1234F` to another valid-format value, for example `FGHIJ5678K`.
- Leave the GSTIN unchanged.
- Run verification.
- Expected: **REJECTED**, because the PAN segment embedded in GSTIN does not match the submitted PAN.

## 4. Bank account-holder mismatch — pending

- Load the sample case.
- Change account holder name to `Acme Trading`.
- Keep the legal company name and bank proof unchanged.
- Run verification.
- Expected: **PENDING**, with a bank-account-holder name review warning.

## 5. Unreadable or image-only evidence — pending

- Fill all required fields with the sample values.
- Replace one evidence file with a scanned/image-only PDF (or an empty TXT file).
- Run verification.
- Expected: **PENDING** because no selectable text can be extracted or compared. A human reviewer must inspect the source document.

## 6. Malformed IFSC — rejected

- Load the sample case.
- Change IFSC to `12345`.
- Run verification.
- Expected: **REJECTED** with the IFSC format issue.

## Interpretation

These are deterministic prototype rules, not external verification. A matching string in a document does not prove authenticity; a failed text match may also be caused by OCR, formatting, abbreviations or document quality. In real onboarding, route uncertain evidence to a reviewer and integrate trusted registry/bank verification APIs only with authorization.
