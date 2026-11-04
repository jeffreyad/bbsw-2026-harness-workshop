# ADVS Specification (fallback copy)

Source data: VS domain in `data/sdtm`, ADSL in `data/adam/adsl.parquet` (workshop project)

Work in the `harness/` subfolder.

## Variables

| Name | Label | Derivation rule | Source |
|---|---|---|---|
| STUDYID | Study Identifier | Copy from VS | VS.STUDYID |
| USUBJID | Unique Subject Identifier | Copy from VS | VS.USUBJID |
| PARAMCD | Parameter Code | VS.VSTESTCD | VS.VSTESTCD |
| PARAM | Parameter | VS.VSTEST, with unit appended in brackets | VS.VSTEST, VS.VSSTRESU |
| AVISIT | Analysis Visit | Derived from VS.VISIT per visit mapping | VS.VISIT |
| AVISITN | Analysis Visit (N) | Numeric version of AVISIT | VS.VISITNUM |
| ADT | Analysis Date | Date part of VS.VSDTC, converted to a date | VS.VSDTC |
| ADY | Analysis Relative Day | ADT - TRTSDT + 1 if ADT >= TRTSDT, else ADT - TRTSDT | ADT, ADSL.TRTSDT |
| AVAL | Analysis Value | VS.VSSTRESN | VS.VSSTRESN |
| BASE | Baseline Value | AVAL from the baseline record (ABLFL = "Y") for the same subject and PARAMCD | AVAL |
| ABLFL | Baseline Record Flag | "Y" on the last non-missing AVAL on or before TRTSDT, per subject and PARAMCD; otherwise NA | AVAL, ADT, ADSL.TRTSDT |
| CHG | Change from Baseline | AVAL - BASE on post-baseline records; NA on baseline records | AVAL, BASE |
| ANL01FL | Analysis Flag 01 | "Y" on post-baseline records with non-missing AVAL; otherwise NA | AVAL, ABLFL |
| TRTSDT | Treatment Start Date | Merge from ADSL | ADSL.TRTSDT |
| SAFFL | Safety Population Flag | Merge from ADSL | ADSL.SAFFL |

## Decisions made

- Baseline is the last non-missing value on or before TRTSDT.
- CHG is NA (not 0) on baseline records.
- Population: records for subjects with SAFFL = "Y" only.

## Open questions

- How should unscheduled visits be handled for baseline and windowing?
- Are visit windows required, or is the collected VISIT used as is?
- Should records with a missing ADT be dropped or kept with a flag?
