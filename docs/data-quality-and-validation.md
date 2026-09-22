# Data quality and validation

[← Guide home](../README.md#documentation) · Document 5 of 10

## On this page

- [Define quality in relation to intended use](#define-quality-in-relation-to-intended-use)
- [Build a validation plan](#build-a-validation-plan)
- [Choose thresholds deliberately](#choose-thresholds-deliberately)
- [Handle outliers and drift carefully](#handle-outliers-and-drift-carefully)
- [Validation report template](#validation-report-template)
- [Error reporting and resolution](#error-reporting-and-resolution)
- [Exceptions and release decisions](#exceptions-and-release-decisions)
- [Review checklist](#review-checklist)

## Define quality in relation to intended use

Data quality describes whether data is fit for a particular purpose. A dataset can be structurally valid and still be unsuitable because it is stale, incomplete, poorly sampled, or based on the wrong business definition.

Validation should produce evidence and a decision. Record what was checked, which data was checked, when the check ran, and how the result affects consumers. Store validation reports in a shared, access-controlled location and reference them from the dataset record.

## Build a validation plan

Start with the failure modes that would change a decision. For a billing report, an incorrect currency conversion may matter more than a missing optional device field. For churn prediction, using information recorded after the prediction cutoff can invalidate evaluation even when all values are present.

For each check, define an owner, frequency, scope, threshold, severity, and response. Separate checks that block release from checks that generate warnings or require investigation.

| Check | Question | Example response |
| --- | --- | --- |
| Completeness | Are required fields and expected partitions present? | Quarantine records missing a required identifier |
| Type and format | Do values match the expected schema and representation? | Reject unparseable timestamps and retain an error count |
| Uniqueness | Are rows unique under the declared key? | Investigate duplicates before aggregation |
| Range and validity | Are values within permitted ranges or categories? | Review negative counts or an undocumented subscription tier |
| Referential integrity | Do join keys resolve to expected reference records? | Report unmatched accounts and their downstream effect |
| Freshness | Did data arrive within the agreed schedule? | Mark affected dashboards stale and alert the owner |
| Reconciliation | Do totals align with the source or control totals? | Compare counts and aggregates before and after transformations |
| Schema drift | Were fields, types, or constraints changed unexpectedly? | Block incompatible output until reviewed |
| Distribution change | Have value distributions or subgroup proportions shifted? | Investigate source changes, outages, or real behavior changes |
| Temporal validity | Are feature and label windows consistent with the intended cutoff? | Exclude records that use unavailable future information |

The original guide's core checks are missing values, outliers, schema drift, types, and duplicates. The additional checks above help connect validation to downstream use.

## Choose thresholds deliberately

Thresholds should reflect known business expectations, source behavior, and the consequences of error. Record the rationale and who approved it. Revisit thresholds after an intentional collection or product change.

The following thresholds are **illustrative**, not universal defaults:

| Rule | Example criterion | Action |
| --- | --- | --- |
| Required event ID | Zero missing IDs among accepted events | Quarantine invalid rows and report the count |
| Published event uniqueness | Zero duplicate `(tenant_id, event_id)` keys | Block publication until deduplication is verified |
| Hourly pipeline freshness | Latest successful output no more than two hours old | Warn consumers and investigate the failed or delayed run |
| Thirty-day usage count | Integer between 0 and 30 under the stated day definition | Fail the affected feature check |
| Optional device type | Investigate if missingness exceeds 5% | Review collection behavior before deciding to block |

A percentage must have a defined denominator. “5% missing” should specify the field, population, batch or time window, and whether rejected records were excluded. An overall pass can hide a severe failure in a small but important subgroup.

## Handle outliers and drift carefully

An unusual value is a signal to investigate, not proof of an error. A legitimate large customer may look like an outlier. Document whether values are retained, capped, transformed, or excluded, and explain how that affects interpretation.

Distinguish structural changes from distribution changes. A renamed field is schema drift; a shift in a field's values is distribution drift. Neither automatically establishes declining model performance. Confirm the source of the change and evaluate its effect on the specific consumer.

Compare equivalent periods and populations where possible. Product launches, seasonality, outages, and changes in eligibility can all alter a baseline. Record sample size and segment coverage before drawing conclusions.

## Validation report template

```text
Dataset ID and release:
Pipeline run / snapshot / partition:
Checked at (with time zone):
Check implementation revision:
Scope (full data / new partition / sample):
Rows examined and sampling method:
Rule name and expected result:
Observed result and affected count/rate:
Status (pass / warning / fail / not run):
Evidence location:
Assigned owner:
Consumer impact:
Decision (release / restrict / quarantine / block):
Decision owner and timestamp:
Exception or issue reference:
Follow-up due date:
```

“Not run” is different from “pass.” A run with no input rows also needs explicit interpretation; a check can appear to pass simply because it evaluated nothing. Keep summaries readable while linking detailed logs for investigation.

## Error reporting and resolution

Use a shared issue system such as GitHub Issues or an approved ticket queue. Capture the error description, detection date, assigned engineer, affected dataset versions, resolution steps, and fix timestamp, as specified in the original guide.

A complete incident workflow is:

1. **Detect and record:** preserve the failing run, rule, and evidence.
2. **Assess impact:** identify affected consumers, time periods, populations, and decisions.
3. **Contain:** stop publication, quarantine a partition, or mark outputs with a limitation as appropriate.
4. **Assign and investigate:** identify an owner and distinguish source, transformation, and consumer problems.
5. **Correct:** version the fix; define any backfill or replacement data required.
6. **Revalidate:** rerun relevant checks and confirm downstream results before closing the issue.
7. **Communicate and learn:** notify consumers, document the cause, and improve checks or instructions.

Do not silently replace previously published data. If historical results change, link the corrected release and explain which reports or models may need to be regenerated.

## Exceptions and release decisions

If a team accepts a known issue, record its scope, rationale, approval, permitted uses, and expiry or review date. An exception should not turn into an undocumented permanent rule. Explain whether a consumer can use the unaffected portion safely.

For example, a missing optional field might be acceptable for an aggregate activity report but block a model that relies on that field. The release decision should identify the allowed use rather than label the entire dataset “good.”

## Review checklist

- [ ] Required checks and their rationale are documented.
- [ ] Reports identify the exact release, scope, and implementation revision.
- [ ] Failed, skipped, and empty-input checks remain visible.
- [ ] Material issues have owners and consumer-facing impact notes.
- [ ] Fixes and backfills are revalidated before closure.
- [ ] Exceptions have an approver and a review or expiry date.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Schema and metadata standards](schema-and-metadata.md) | [All documents](../README.md#documentation) | [Version control and audit trails →](version-control-and-audit-trails.md) |
