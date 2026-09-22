# Data quality and validation

[← Guide home](../README.md#documentation) · Document 5 of 10

Data quality checks help teams catch incomplete, inconsistent, or unexpected data before it affects analytics or machine learning systems.

## Run consistent validation checks

Common checks include:

- Missing value detection
- Outlier detection
- Schema drift monitoring
- Data type validation
- Duplicate record checks

Validation results should be stored in a shared location so teams can review past checks and maintain an audit trail.

## Document validation results

For each validation process, record:

- Validation method
- Date performed
- Success criteria
- Results
- Errors or exceptions
- Dataset version

## Track and resolve data issues

When a validation check identifies a problem, document how the issue moves from detection to resolution.

Include:

- Error description
- Date detected
- Assigned owner
- Resolution steps
- Date or timestamp of the fix
- Related ticket or issue

Teams may use systems such as Jira or GitHub Issues to track these problems.

## Monitor changes over time

Validation should also account for changes that may affect dataset reliability, including:

- Schema changes
- New or removed fields
- Changes in data sources
- Unexpected shifts in values
- Changes to transformation logic

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Schema and metadata standards](schema-and-metadata.md) | [All documents](../README.md#documentation) | [Version control and audit trails →](version-control-and-audit-trails.md) |
