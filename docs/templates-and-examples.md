# Templates and examples

[← Guide home](../README.md#documentation) · Document 9 of 10

Standardized templates help teams document datasets consistently across projects.

## Dataset documentation template

![Dataset documentation template with name, owner, purpose, source type, update date, and sections for overview, schema, transformations, validation, ethics, and access.](../assets/images/dataset-documentation-template.png)

*A compact dataset record template from the original guide.*

Each dataset record should include:

### Overview

- Dataset name
- Owner
- Purpose
- Source type
- Last updated

### Schema and metadata

- Field names
- Data types
- Field descriptions
- Null handling
- Units or ranges

### Transformations

- Source datasets
- Transformation logic
- Scripts or queries
- Dependencies

### Validation

- Validation methods
- Quality checks
- Results
- Known issues

### Governance

- Access permissions
- Privacy considerations
- Bias or fairness notes
- Known limitations

## Example: User behavior dataset

A product analytics dataset may document:

- User and session identifiers
- Feature interactions
- Event timestamps
- Device information
- Data source
- Update frequency
- Dataset owner
- Known representation limitations

![User behavior schema with user_id, session_id, feature_clicked, timestamp, and device_type fields and their types and descriptions.](../assets/images/user-behavior-dataset-schema.png)

*Example schema for recording product interactions.*

## Example: Predictive retention dataset

A dataset used to predict customer churn may include:

- Recent product usage
- Support activity
- Subscription tier
- Churn status
- Source systems
- Transformation logic
- Tracking or consent limitations

![Predictive retention schema with user_id, usage_days_last_30, support_tickets_opened, subscription_tier, and churned fields.](../assets/images/predictive-retention-dataset-schema.png)

*Example schema for a customer churn prediction dataset.*

Examples should demonstrate how the documentation framework applies to realistic datasets rather than acting as fixed schemas.

---

| Previous | Guide | Next |
| :--- | :---: | ---: |
| [← Privacy, fairness, and reproducibility](privacy-fairness-and-reproducibility.md) | [All documents](../README.md#documentation) | [Maintenance and governance →](maintenance-and-governance.md) |
