# Privacy, fairness, and reproducibility

[← Guide home](../README.md#documentation) · Document 8 of 10

## On this page

- [Make limitations and decisions visible](#make-limitations-and-decisions-visible)
- [Document representation and sampling](#document-representation-and-sampling)
- [Assess bias in the intended context](#assess-bias-in-the-intended-context)
- [Record mitigation and residual limitations](#record-mitigation-and-residual-limitations)
- [Record exclusions and limitations](#record-exclusions-and-limitations)
- [Document privacy, security, and consent](#document-privacy-security-and-consent)
- [Account for derived data and deletion](#account-for-derived-data-and-deletion)
- [Support transparency and reproducibility](#support-transparency-and-reproducibility)
- [Review checklist](#review-checklist)

## Make limitations and decisions visible

A dataset record should explain both what is present and what cannot be concluded from it. Record coverage gaps, collection choices, sensitive information, approved uses, assessment evidence, and unresolved questions. These details help people judge whether reuse is appropriate.

Separate observed evidence from assumptions and planned work. “Fairness review scheduled” does not mean “fairness assessed,” and a technical privacy measure does not establish that every use is permitted.

## Document representation and sampling

Describe the intended population and the population actually observed. Include demographic variables where their use is appropriate and approved, sampling methods, source coverage, collection conditions, and exclusions.

Questions to answer include:

- Which regions, plans, languages, devices, or user groups are represented?
- Who is missing because of opt-outs, inactivity, access barriers, or instrumentation gaps?
- Are labels collected consistently across groups and time periods?
- Do historical decisions influence which outcomes are recorded?
- Were records reweighted, resampled, filtered, or otherwise altered to address a limitation?

Record why a variable was included or excluded and what that means for assessment. Do not collect sensitive attributes merely to complete a template; document the approved assessment design and its limitations when relevant attributes are unavailable.

## Assess bias in the intended context

The original guide calls for statistical parity checks, subgroup performance testing, fairness-aware metrics, and mitigation notes. Apply these methods to a defined use and population rather than treating a single score as a universal fairness certificate.

Demographic parity compares selection rates across groups. Equalized odds compares true-positive and false-positive rates; equal opportunity focuses on true-positive rates. The appropriate assessment depends on the decision, harms, and available evidence. The [Fairlearn metrics guide](https://fairlearn.org/main/user_guide/assessment/common_fairness_metrics.html) explains these definitions and their limitations.

Dataset representation and model outcomes are different assessment targets. A balanced dataset does not guarantee equitable outcomes, and differing group proportions alone do not identify the right mitigation.

For every assessment, record the date, tool and version, dataset or model version, metric definitions, groups examined, sample sizes, results, uncertainty, and reviewer interpretation. Explain small samples, missing attributes, and groups that could not be assessed. Store sensitive assessment evidence in an appropriate restricted location.

## Record mitigation and residual limitations

Describe the problem a mitigation is intended to address, the change made, and how its effects were evaluated. Examples might include correcting a collection defect, improving label instructions, revising a sampling process, or restricting a use that the data cannot support.

Record before-and-after evidence when available, effects on other groups or metrics, and unresolved limitations. Identify who accepts any remaining risk, for which purpose, and when the decision will be revisited. A mitigation note should describe evidence, not simply say “bias removed.”

## Record exclusions and limitations

| Category | Example from the original guide | Potential impact |
| --- | --- | --- |
| Excluded region | Certain small markets are absent | Reduced generalizability to those markets |
| Missing variable | Income range is unavailable | Limits assessment of some fairness concerns in predictive scoring |

The missing-variable example illustrates an assessment limitation, not a recommendation to collect income information.

<details>
<summary>View the limitations table from the original guide</summary>

![Original table showing excluded regions and missing income-range information with potential impacts.](../assets/images/dataset-exclusions-and-limitations.png)

</details>

For each limitation, document what is excluded, why, the affected population or period, consequences for interpretation, and any prohibited or restricted uses. Include temporary limitations such as an outage or a partially completed backfill.

## Document privacy, security, and consent

A practical privacy record should identify:

| Topic | What to record |
| --- | --- |
| Information categories | Direct identifiers, linkable identifiers, sensitive attributes, free text, and other fields requiring controlled handling |
| Purpose and approval | The approved purpose and the review or policy reference supporting it |
| Collection and consent | Applicable notices, consent records where relevant, preferences, and collection restrictions |
| Minimization | Why each sensitive field is needed and whether a less detailed form would suffice |
| Protection | Masking, tokenization, hashing, encryption, access controls, and their implementation references |
| Access and sharing | Approved audiences, request process, third-party restrictions, and review responsibilities |
| Retention and deletion | Periods, triggers, storage locations, owner, and verification process |
| Assessments | Links to the relevant privacy or security review and unresolved actions |

Document the requirements identified by the responsible privacy or legal reviewers for the relevant use and jurisdiction. Consent should not be assumed to be the only possible basis for processing, or a blanket authorization for every downstream purpose.

**Hashing is not automatically anonymization.** Replacing an identifier can leave records linkable to individuals. The UK ICO distinguishes pseudonymisation from anonymisation and explains controls for additional identifying information in its [pseudonymisation guidance](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-sharing/anonymisation/pseudonymisation/). Record the actual technique and residual linkage risks; use the terminology supported by the assessment rather than labeling a dataset anonymous by default.

## Account for derived data and deletion

Map where data is copied or transformed: raw storage, curated tables, extracts, feature stores, backups, and downstream systems. Document how collection preferences, deletion requests, or other restrictions propagate through the approved process.

Do not assume deleting a source row removes derived records or information reflected in a trained model. Record the systems affected and the review needed to decide what downstream action is appropriate. Describe exceptions and their authority rather than inventing a universal retention period.

Use synthetic examples in shared documentation. Even screenshots and validation logs can reveal personal information or sensitive operational details; review what is published and who can access supporting evidence.

## Support transparency and reproducibility

The original guide calls for lineage diagrams, transformation and feature derivations, validation and bias results, and notes for reproducing exports or queries. Make these references specific enough to identify the same inputs and assumptions.

A reproduction record should include:

- Dataset and source snapshot identifiers or content checksums where appropriate.
- Extraction query or configuration revision and input cutoff.
- Transformation code, dependencies, environment, and relevant configuration.
- Feature and label definitions, split assignment, and fitted preprocessing artifacts.
- Seeds for stochastic steps and any known nondeterministic behavior.
- Validation and assessment reports, including accepted exceptions.
- Output identifiers, run times, access requirements, and verification criteria.

Define what reproduction means for the task: identical exported bytes, the same logical records, or results within a justified tolerance. A random seed alone does not guarantee identical results across changing data, code, or environments.

If inputs cannot be retained or redistributed, record that constraint and what evidence remains. Do not promise exact reproduction when permissions, deletion, or unavailable dependencies prevent it.

## Review checklist

- [ ] Population, sampling, exclusions, and unassessed groups are visible.
- [ ] Assessment methods, results, limitations, and reviewers are recorded.
- [ ] Sensitive information and permitted purposes have appropriate review references.
- [ ] Protection measures are described accurately without overstating anonymity.
- [ ] Retention and deletion responsibilities include derived artifacts.
- [ ] Reproduction instructions identify inputs, code, configuration, and practical limits.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Analytics workflows and integration](analytics-workflows-and-integration.md) | [All documents](../README.md#documentation) | [Templates and examples →](templates-and-examples.md) |
