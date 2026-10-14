# BaadhProof — Test Cases

**Status:** Test plan; results must be filled in after running against the implementation.

| ID | Area | Test steps / input | Expected result | Actual result |
|---|---|---|---|---|
| TC-01 | App launch | Open the app on a supported browser | Main page loads without a blocking error | Not run |
| TC-02 | Required fields | Submit the damage form with all required fields empty | Required-field messages appear; no invalid record is saved | Not run |
| TC-03 | Valid record | Enter date, location, category, and description; submit | Record is accepted and displayed accurately | Not run |
| TC-04 | Date validation | Enter an invalid date or malformed date value | Clear validation message appears; invalid value is not accepted | Not run |
| TC-05 | Category | Choose each supported damage category | Selected category is retained and shown correctly | Not run |
| TC-06 | Long description | Enter a long description at the documented limit and beyond it | Allowed input works; over-limit input is handled clearly | Not run |
| TC-07 | Edit/review | Change a field before finalizing the record | Updated value appears in the summary | Not run |
| TC-08 | Sample data | Load or manually enter a record from `sample-data/damage-records.json` | Values display correctly; no personal data is exposed | Not run |
| TC-09 | Checklist | Open the document checklist | Checklist is readable and clearly described as general guidance | Not run |
| TC-10 | Official links | Open each listed resource link | Link destination is correct and its last-checked date is visible | Not run |
| TC-11 | Print/PDF | Use the print/export control, if implemented | Summary is readable and does not clip important fields | Not run |
| TC-12 | Mobile layout | Test a narrow phone viewport | Text and controls fit; no essential action requires horizontal scrolling | Not run |
| TC-13 | Keyboard access | Navigate forms and buttons with keyboard only | Focus is visible and controls can be operated without a mouse | Not run |
| TC-14 | Error handling | Trigger a validation or network error, where applicable | Plain-language error appears and entered data is not unexpectedly lost | Not run |
| TC-15 | Privacy | Inspect demo data and repository for real personal data/secrets | No real personal data, credentials, or `.env` secrets are committed | Not run |
| TC-16 | Access control | If cloud persistence exists, try accessing another user's record | Unauthorized access is denied | Not run |
| TC-17 | Disclaimer | Review pages containing relief/checklist information | App states it is not a government portal and does not guarantee assistance | Not run |
| TC-18 | Resource freshness | Review each official resource's last-checked date | Stale/unverified resources are clearly labelled or removed | Not run |

## How to record results

After testing, replace `Not run` with `Pass`, `Fail`, or `Blocked`. For failures, add browser/device, steps to reproduce, and a short note. Do not claim a test passed unless it was actually run.

## Suggested manual smoke test

1. Start the app using the actual setup steps in the root README.
2. Open the homepage on desktop and a mobile-sized viewport.
3. Create a fictional crop-damage record.
4. Verify validation by leaving a required field empty.
5. Review the record summary and print/export if implemented.
6. Check official resource URLs and disclaimers.
7. Confirm the app does not imply that a claim was submitted or approved.
