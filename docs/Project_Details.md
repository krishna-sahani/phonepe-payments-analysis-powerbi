# Project details

## Scope and provenance

This repository publishes the exact file supplied as `PhonePe_ Analysis Project5(2).pbix`, renamed `PhonePe_Payments_Analysis.pbix`, plus the author's `Screenshot 2026-11-21 163927.png`. The report and screenshot have not been redesigned. No alternative corrected PBIP ZIP is included.

The current PBIX is byte-identical (SHA-256 `3a2206ea831de20926406cdbdedeed6a001232108866e6c3fb75b78bd7119f59`) to the earlier binary whose data and model metadata were inspected. The existing extraction therefore applies to this supplied file. Dataset aggregates describe the complete data, not necessarily a saved or cross-highlighted report selection.

## Tables and fields

| Table | Main fields | Purpose |
| --- | --- | --- |
| All_Transactions | Transaction_ID, Amount, User_ID, Service, Service Type, Payment_Status, Reason, Date | Payment-event records |
| All_Users | User_ID, Name, Age, Join_Date, Age Segment | Registered-user attributes |
| Date_Table | Date, Year, Month No., Month, Quarter, Weekday, Day No., Weekend | Calendar attributes used in visuals and DAX |
| Measures (2) | DAX measures | KPI and period-comparison calculations |

The parsed model metadata contains an active many-to-one relationship from All_Transactions[User_ID] to All_Users[User_ID], with single-direction filtering. No active relationship from Date_Table to the transaction table was present in the inspected metadata. Check and validate date filtering in Desktop before treating monthly or MoM outputs as dependable.

## Data checks and coverage

- 300,000 transaction records and 300,000 distinct Transaction_ID values.
- 107,658 registered users, each with a unique User_ID.
- 100,761 distinct users appear in transaction records; all transaction user keys match the user table.
- No missing values were found in the extracted source columns.
- Transaction dates cover 01 January–30 December 2024; December is partial coverage.
- User join dates extend into 2025 despite transactions being in 2024. Cohort/tenure analysis requires clarification.
- 32,404 user-table rows repeat a previously encountered name. Name is not a unique user identifier.

## Services

| Service | Transaction value (INR) |
| --- | ---: |
| Loans | 2,532,509,362.75 |
| Insurance | 512,922,965.71 |
| Money Transfer | 378,194,632.22 |
| Recharge Bills | 50,694,973.48 |

## Payment outcomes

| Payment_Status | Transactions |
| --- | ---: |
| Successful | 287,993 |
| Failed | 9,980 |
| Wrong PIN | 700 |
| Server error | 692 |
| Insufficient amount | 635 |

The separate Reason field labels Failed and Server error rows as Pending. Their business meaning is unresolved; no guessed status remapping has been applied.

## Measures and interpretation

`docs/Measures.dax` preserves the existing measure names and expressions, including their original spelling. They document the supplied report; they are not a claim that every calculation has been corrected or Desktop-tested.

- Total Transaction counts Transaction_ID; all supplied IDs are unique and nonblank.
- Total Transaction value sums Amount.
- Total Users counts distinct registered User_ID values, explaining the screenshot's rounded 108K card. This differs from active transacting users.
- Successfull Rate divides the supplied successful-transaction measure by total transactions. Its successful-count expression replaces a same-column Payment_Status filter rather than intersecting it; verify behaviour when a non-success status is selected.
- The existing Total Transaction MOM% expression references value measures, so it does not independently calculate count growth. The screenshot's two 8.98% figures are presented as supplied display outputs, not independently verified growth findings.
- The original report's MoM card bindings and associated colour rules also need review. Nothing in the uploaded binary was silently changed.
- Top 5 Users groups by names; identical names may aggregate multiple IDs.
- Age segments are source-defined registered-user labels, including the spelling “Millenials”; their official demographic boundaries were not verified.
- The insights text is fixed report text and should not be assumed to update with filters.

## Validation boundary

The PBIX ZIP container passed an integrity check, and the published PBIX and screenshot are verified against local Git blob hashes and file sizes. Full-data aggregates come from the previously decoded identical binary. Native Desktop rendering, refresh and interactive behaviour were not executed during this publication. The README screenshot is the author's actual screenshot, not a generated replacement.
