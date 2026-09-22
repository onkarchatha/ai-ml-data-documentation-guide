# Maintenance and governance

[← Guide home](../README.md#documentation) · Document 10 of 10

## On this page

- [Treat documentation as an operating responsibility](#treat-documentation-as-an-operating-responsibility)
- [Set up the documentation location](#set-up-the-documentation-location)
- [Organize records for discovery](#organize-records-for-discovery)
- [Assign responsibilities](#assign-responsibilities)
- [Combine scheduled reviews with change-triggered updates](#combine-scheduled-reviews-with-change-triggered-updates)
- [Run a documentation review](#run-a-documentation-review)
- [Contributor and approval workflow](#contributor-and-approval-workflow)
- [Automate maintenance checks](#automate-maintenance-checks)
- [Measure usefulness](#measure-usefulness)
- [Suggested rollout plan](#suggested-rollout-plan)
- [Completion and ongoing care](#completion-and-ongoing-care)

## Treat documentation as an operating responsibility

A documentation system needs an owner, a publishing location, a contribution process, and a way to detect stale records. The objective is not to maximize page count; it is to keep the information people rely on accurate and easy to find.

Use this guide as a framework that can grow with the team's tools and workflows. Begin with important datasets and establish a repeatable process before expanding coverage.

## Set up the documentation location

The original guide proposes using an existing tool such as GitHub, Notion, or Confluence. Select a location that fits the team's access needs, review process, and ability to maintain links. If a data catalog is the main discovery surface, decide which information lives there and which records it references.

A practical setup sequence is:

1. Create a top-level home page or repository with a searchable dataset index.
2. Adopt a standard dataset template and a small shared vocabulary for statuses and ownership.
3. Assign dataset owners as maintainers with appropriate edit permissions.
4. Add links between dataset pages, dashboards, models, and code repositories.
5. Define required reviewers and the route for proposing a correction.
6. Record review dates and add a visible way to identify stale or incomplete entries.
7. Test discovery with someone who did not create the dataset.

Avoid maintaining two independently editable copies of the same definition. If information appears in several tools, identify the authoritative source and the synchronization process. Broken synchronization should be visible rather than silently presenting old metadata as current.

## Organize records for discovery

Use stable dataset IDs, descriptive page titles, and consistent sections. Provide both a contents page and links to related records. Include short business summaries before technical detail so non-specialist readers can decide whether they have found the right dataset.

Separate production datasets from experiments, deprecated records, and templates. Make status prominent. An archived page should explain its replacement or disposition rather than appear to be current.

For a public documentation project, publish synthetic examples and general guidance. Keep operational secrets, personal data, restricted evidence, and internal access details in approved systems. Link only what the intended audience can appropriately access.

## Assign responsibilities

| Role | Responsibility from the original guide | Practical evidence of completion |
| --- | --- | --- |
| Data engineer | Update schema and transformation documentation | Technical changes include updated definitions and evidence references |
| Product manager | Ensure alignment with metrics and KPIs | Business definitions and intended uses have been reviewed |
| Compliance officer | Review privacy, security, and bias sections | Relevant assessments and unresolved actions are identified |
| Technical writer or editor | Maintain clarity, consistency, and structure | Terminology, navigation, examples, and accessibility are checked |
| Team lead | Oversee periodic audits and approve updates | Review ownership, decisions, and follow-up actions are recorded |

<details>
<summary>View the responsibilities table from the original guide</summary>

![Original table assigning documentation maintenance responsibilities to engineers, product managers, compliance officers, writers, and team leads.](../assets/images/documentation-maintenance-responsibilities.png)

</details>

Adapt responsibilities to the actual organization. Security, privacy, and legal review may involve distinct specialists, and a small team may combine roles. Name an accountable owner for each decision even when several people contribute.

## Combine scheduled reviews with change-triggered updates

The original guide recommends monthly metadata checks, quarterly fairness reviews, and annual access and retention reviews. Use these as a starting schedule, then adjust for dataset criticality and rate of change.

| Cadence or trigger | What to review |
| --- | --- |
| Monthly | Schema, field definitions, new datasets, owners, source links, and metadata accuracy |
| Quarterly | Bias and fairness notes, coverage limitations, and the currency of assessment evidence |
| Annually | Access permissions, retention notes, archive decisions, and overall governance arrangements |
| Every material source or schema change | Lineage, definitions, downstream impact, compatibility, and validation rules |
| Every new use or consumer | Suitability, access, coverage, privacy constraints, and whether existing assessments apply |
| After an incident or backfill | Root cause, corrected releases, limitations, consumer notices, and preventive checks |
| During an ownership change | Maintainers, support routes, permissions, open issues, and review commitments |

A scheduled review should not delay documenting a known material change. Record **last edited**, **last reviewed**, and **next review due** separately; a formatting edit should not reset the date of a substantive review.

## Run a documentation review

A review should check claims against evidence, not merely confirm that headings are present.

1. Confirm the dataset is still used for the purpose stated.
2. Compare the documented grain, fields, sources, and cadence with the current implementation.
3. Check that validation and assessment references point to the relevant release and are accessible to the right reviewers.
4. Review consumers, metric definitions, limitations, restrictions, and unresolved incidents.
5. Confirm owners, access routes, and retention or retirement decisions remain current.
6. Test navigation and important cross-links.
7. Record the reviewer, date, findings, actions, owners, and due dates.

If a material section cannot be verified, mark it for review and state the effect on use. Do not extend an “approved” status automatically because nobody reported a problem.

## Contributor and approval workflow

Give contributors a simple route to report inaccuracies or propose changes. A useful request names the dataset, the confusing or incorrect statement, the proposed correction, and any supporting evidence. Use synthetic or redacted examples in broadly visible issue discussions.

For a change, update the affected definition, examples, references, and release note together. Have the right owner review technical meaning and consumer impact. A writer can check clarity, but should not be expected to approve an undocumented business or privacy decision.

Define when an editorial change can be handled directly and when a reviewed change request is required. Use the [version-control chapter](version-control-and-audit-trails.md) for release and migration records.

## Automate maintenance checks

Useful checks include broken relative links, missing required sections, absent owners, overdue review dates, schema differences, and references to deprecated datasets. Report failures to someone who can act on them.

Automation can flag an absent description; it cannot reliably establish that the description is true. Keep human review for definitions, suitability, limitations, and decisions requiring judgment. Identify generated content and prevent synchronization from overwriting reviewed context without notice.

## Measure usefulness

Track a small set of indicators that answer whether the documentation helps:

- **Coverage:** proportion of in-scope datasets with a current record and named owner.
- **Review currency:** proportion reviewed within the agreed interval, with the denominator defined.
- **Evidence completeness:** proportion of relevant releases linked to validation and approval records.
- **Issue response:** time to acknowledge and resolve documentation problems.
- **Reader success:** whether a new reader can find the owner, interpret a field, and identify limitations without a private explanation.

Separate presence from accuracy. A completed template can still be wrong, and page views alone do not demonstrate useful documentation.

## Suggested rollout plan

Start with a small, representative set: a dashboard dataset, an event stream, and an ML training dataset if those exist. Fill the records with their owners, identify gaps, and test the handoff with consumers. Refine the template based on what readers need, then apply it to the remaining prioritized datasets.

For each wave, define the scope, owners, review criteria, and completion date. Track unresolved gaps rather than delaying all publication until every detail is perfect. Clearly label draft or restricted records so incompleteness is not mistaken for approval.

## Completion and ongoing care

A record is ready for routine use when its meaning, provenance, evidence, limitations, and support path are sufficiently clear for its intended audience, and the required reviewers have made their decisions. The team should be able to explain what happens when it changes or fails.

Effective documentation is shared work across engineering, product, analysis, writing, and governance. Maintain the guide as those workflows evolve, archive obsolete material deliberately, and keep the reader's ability to make an informed decision at the center of each update.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Templates and examples](templates-and-examples.md) | [All documents](../README.md#documentation) | — |
