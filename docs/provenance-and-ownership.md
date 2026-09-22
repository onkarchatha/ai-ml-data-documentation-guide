# Data provenance and ownership

[← Guide home](../README.md#documentation) · Document 3 of 10

## On this page

- [Explain both origin and accountability](#explain-both-origin-and-accountability)
- [Internal, external, and hybrid sources](#internal-external-and-hybrid-sources)
- [Make extraction reproducible](#make-extraction-reproducible)
- [Connect provenance to lineage](#connect-provenance-to-lineage)
- [Assign ownership and reviewers](#assign-ownership-and-reviewers)
- [Example source and ownership record](#example-source-and-ownership-record)
- [Handoffs and ownership changes](#handoffs-and-ownership-changes)
- [Review checklist](#review-checklist)

## Explain both origin and accountability

Provenance describes where a dataset came from and how it was created. Ownership identifies who is accountable for keeping its definition, quality expectations, and documentation usable. A source link without an owner is difficult to maintain; an owner without a source history cannot explain unexpected changes.

Use a stable dataset ID that stays the same when a page title or storage location changes. Give derived outputs their own identity and link them to their inputs.

## Internal, external, and hybrid sources

Internal sources may include company databases, product telemetry, billing records, and internal APIs. External sources may include vendor APIs, licensed datasets, or public releases. A hybrid dataset combines them and should preserve the restrictions and provenance of each input.

Record a separate source entry for every materially different input:

| Field | What to capture |
| --- | --- |
| Source name and ID | A human-readable name and stable reference |
| Source type | Internal, external, or hybrid; identify each component |
| Access reference | Approved catalog entry, storage reference, API documentation, or request route |
| Owner or maintainer | Responsible team and a durable contact route |
| Extraction method | API, scheduled ETL job, database query, file transfer, or manual import |
| Update frequency | Expected cadence, typical delay, and relevant time zone |
| Coverage | Time range, regions, customer groups, products, and record types represented |
| Source version | Release, extract ID, partition, or snapshot identifier |
| Restrictions | License, contract, permitted purposes, redistribution limits, and expiry if applicable |
| Collection choices | Filters, sampling, exclusions, opt-outs, and known gaps |

A public download is not automatically unrestricted. Record the specific usage terms and who assessed them. For internal systems, describe access through an approved route rather than placing passwords, tokens, or confidential connection strings in documentation.

## Make extraction reproducible

Document the query or extraction configuration, its revision, execution time, input cutoff, and output location. If the source changes continuously, explain how the extraction identifies a repeatable state. A query against a live table may produce different results tomorrow even when the query text is unchanged.

For incremental collection, state how new, changed, and deleted records are detected. Explain retry behavior, whether the same event can be delivered twice, and how completeness is assessed. For manual imports, identify the preparer, original file, checks applied, and reviewer.

Use timestamps with a stated time zone and clarify whether a boundary is inclusive or exclusive. A record labeled “September data” is incomplete unless readers know which dates and timestamps define membership.

## Connect provenance to lineage

A useful lineage description lets someone move upstream from a dashboard or model input to its sources and downstream from a source change to its affected consumers.

A high-level example is:

```text
Product event API ──> validated event records ──> daily usage features ──> retention dataset
Billing system ───────────────────────────────────────────────────────> retention dataset
Support CRM ──> ticket counts ─────────────────────────────────────────> retention dataset
```

For each connection, record the dataset IDs, transformation reference, relevant keys, owner, and release relationship. Use field-level lineage for high-impact outputs where a dataset-level diagram cannot explain a calculation. A metric such as net revenue needs more detail than a box labeled “billing.”

The [W3C PROV overview](https://www.w3.org/TR/prov-overview/) offers a formal provenance vocabulary for describing entities, activities, and responsible agents. Teams can use its concepts without adopting a full provenance implementation.

## Assign ownership and reviewers

The original guide distinguishes a primary owner, secondary reviewers, and a contact point. Make those responsibilities concrete:

| Responsibility | Expected contribution |
| --- | --- |
| Primary dataset owner | Maintains the record, coordinates updates, and ensures issues have an accountable response |
| Technical maintainer | Operates collection and transformation processes and updates technical evidence |
| Business definition owner | Resolves disagreements about metric meaning, population, and intended use |
| Schema or quality reviewer | Checks structure, validation rules, and the impact of changes |
| Specialist reviewer | Assesses privacy, security, fairness, or other concerns when relevant |
| Backup owner | Maintains continuity during absence or a team transition |

One person may cover several responsibilities on a small team. Record that explicitly, along with any review that should be independent. Prefer a maintained team contact route over a single individual's inbox.

## Example source and ownership record

The following is an illustrative record, not a description of an operating production system:

| Field | Example |
| --- | --- |
| Dataset ID | `product-user-events` |
| Purpose | Describe observed feature interactions across sessions |
| Source | Internal event-tracking API |
| Grain | One accepted feature-interaction event |
| Refresh | Hourly; record the actual completion time for each batch |
| Primary owner | Data Engineering |
| Business reviewer | Product Analytics |
| Extraction reference | Versioned ingestion job and batch identifier |
| Known limitation | Event-based collection underrepresents inactive users |
| Support | The team's maintained issue queue, linked in the operational record |

The limitation affects interpretation: absence from the event table does not prove a user does not exist. To estimate activation across all eligible users, connect an approved user population to the event dataset and document the join.

## Handoffs and ownership changes

Before transferring ownership, review the dataset purpose, dependencies, consumers, open issues, restricted uses, and next review date. Record the effective date of the handoff and the receiving owner's acknowledgment. Update the catalog, documentation page, and support routes together.

If a source is discontinued or a vendor changes terms, identify affected consumers before replacing it. The replacement may have different coverage or definitions even when its fields look similar.

## Review checklist

- [ ] Every source has a stable identity, owner, extraction method, and coverage description.
- [ ] The current output can be traced to its input releases and transformation revisions.
- [ ] Licensing and use restrictions have an identified reviewer and evidence reference.
- [ ] Primary and backup ownership are current.
- [ ] Known source gaps and unresolved questions are visible to consumers.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Dataset lifecycle](dataset-lifecycle.md) | [All documents](../README.md#documentation) | [Schema and metadata standards →](schema-and-metadata.md) |
