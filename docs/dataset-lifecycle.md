# Dataset lifecycle

[← Guide home](../README.md#documentation) · Document 2 of 10

## On this page

- [Use the lifecycle as a documentation framework](#use-the-lifecycle-as-a-documentation-framework)
- [Collection: explain what entered the system](#collection-explain-what-entered-the-system)
- [Transformation: explain what changed](#transformation-explain-what-changed)
- [Validation: record evidence and a decision](#validation-record-evidence-and-a-decision)
- [Usage: connect data to the decisions it supports](#usage-connect-data-to-the-decisions-it-supports)
- [Archiving and retirement: preserve context deliberately](#archiving-and-retirement-preserve-context-deliberately)
- [Suggested lifecycle states](#suggested-lifecycle-states)
- [Release readiness checklist](#release-readiness-checklist)

## Use the lifecycle as a documentation framework

A dataset typically moves through collection, transformation, validation, usage, and archiving. Documentation should follow those stages so readers can trace how the data was created, changed, checked, and used. In practice, the stages repeat: new data arrives, validation uncovers a problem, or a consumer requests a different definition.

![Dataset lifecycle showing collection, transformation, validation, usage, and archiving](../assets/images/dataset-lifecycle.png)

*The lifecycle is a recurring process, with documentation updated as data and its uses change.*

![Table mapping lifecycle stages to descriptions and key documentation elements.](../assets/images/dataset-lifecycle-documentation-table.png)

*The original guide's summary of documentation requirements at each stage.*

| Stage | Record | Evidence that supports the next stage |
| --- | --- | --- |
| Collection | Source type, owner, extraction method, frequency, collection date, and coverage | A source record and identified input batch or snapshot |
| Transformation | Scripts, queries, transformation logic, feature purpose, and dependencies | A versioned transformation and execution record |
| Validation | Methods, success criteria, results, exceptions, and error logs | A validation decision tied to a release or run |
| Usage | Dashboards, model versions, metric definitions, approved purposes, and caveats | Consumer references and a visible suitability decision |
| Archiving | Archive location, retention period, access roles, replacement, and deletion rules | A retirement record and a documented disposition decision |

## Collection: explain what entered the system

Record whether the source is internal, external, or a combination. Identify the source owner, extraction mechanism, source revision where available, update schedule, and time span represented by each extraction.

Describe coverage separately from availability. An API might be reachable while omitting historical records, certain plans, unsupported regions, or users who do not generate events. Document sampling, filters, opt-outs, collection interruptions, and expected latency.

Distinguish event time from ingestion time. An action may happen on Monday but arrive on Tuesday because a device was offline. Readers need to know which timestamp drives reports, how late records are handled, and when a reporting period becomes final.

**Collection output:** a source record, a stable dataset ID, a responsible owner, and enough extraction context to explain what was included and excluded.

## Transformation: explain what changed

Describe cleaning, aggregation, joins, filtering, deduplication, normalization, and feature engineering in the order they occur. Link the implementation to a specific revision and explain its purpose in plain language.

For joins, identify the keys and expected relationship. Joining one customer to many subscriptions can multiply rows and inflate counts. State how unmatched records and many-to-many relationships are handled. Record assumptions about units, currencies, time zones, and changing reference tables.

If a transformation learns parameters, such as an imputation value or scaling rule for ML, record where those parameters were fitted and how they are reused. See [schema and metadata](schema-and-metadata.md) for the transformation record.

**Transformation output:** a traceable derived dataset whose row meaning, feature definitions, and upstream dependencies are clear.

## Validation: record evidence and a decision

Checks should compare a named dataset version or run with explicit expectations. Record missing values, types, duplicates, outliers, schema changes, and any checks specific to the intended use. Save reports in a shared location with appropriate access.

A report needs an interpretation: is the output acceptable, blocked, quarantined, or usable with a stated limitation? Identify who made that decision and what happens to failed rows. A passing ingestion job is not the same as a passing validation result.

For changing datasets, specify when checks run and whether they cover the full dataset, a new partition, or a sample. See [data quality and validation](data-quality-and-validation.md).

**Validation output:** a dated report, identified exceptions, and a release decision with an accountable owner.

## Usage: connect data to the decisions it supports

Link datasets to dashboards, reports, metrics, features, and model versions. Capture the consumer's purpose, any additional filters or aggregations, freshness expectations, and known restrictions.

Explain intended and unsuitable uses. A dataset of feature-click events can support observed feature activity, but by itself cannot describe people who never click. A training dataset prepared for churn prediction may not be appropriate for measuring current subscription revenue.

Keep a consumer list so changes can be communicated to the right people. Pin versions where reproducibility matters, and explain the difference between a live table and an approved historical snapshot.

**Usage output:** discoverable consumer references and enough context to judge whether reuse is appropriate.

## Archiving and retirement: preserve context deliberately

Retirement should cover both the data and its documentation. Record the last supported version, why it is being retired, the replacement if one exists, the owner, and the timeline for consumers to migrate.

Decide what can be retained and for how long under applicable organizational requirements. Explain who can retrieve an archived dataset, how restoration is requested, and whether supporting code and dependencies are still available. Archival should not silently become indefinite retention.

If data must be deleted, document the affected stores and derived artifacts, the responsible process, and how completion is recorded. Retain only the permissible metadata or evidence needed to explain the disposition. Reproducibility can be limited by deletion requirements; record that limitation honestly.

**Retirement output:** a visible status, migration instructions, and an approved retention or deletion record.

## Suggested lifecycle states

The following states are a starting convention; define their meaning before using them:

| State | Reader-facing meaning |
| --- | --- |
| Draft | Being assembled; suitability has not been approved |
| Under review | Required evidence exists and named reviewers are assessing it |
| Active | Approved for the uses stated in the record |
| Restricted | Available only for specified uses or audiences |
| Deprecated | Still available during a documented migration period |
| Archived | No longer maintained for routine use; retrieval follows the archive process |
| Retired or deleted | No longer available; the record explains the disposition |

Keep validation status separate from lifecycle status. An active dataset can have a failed latest batch, and an archived release can retain a passing historical validation report.

## Release readiness checklist

- [ ] The owner, dataset ID, grain, and intended use are documented.
- [ ] Source coverage and transformation revisions are traceable.
- [ ] Validation evidence identifies the exact output assessed.
- [ ] Material limitations and restricted uses are visible.
- [ ] Consumers know the version, freshness expectations, and support route.
- [ ] Retention, retirement, and replacement responsibilities are assigned.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Introduction](introduction.md) | [All documents](../README.md#documentation) | [Data provenance and ownership →](provenance-and-ownership.md) |
