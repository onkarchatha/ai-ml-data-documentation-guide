# Schema and metadata standards

Consistent schema and metadata make datasets easier to understand, validate, and use across teams.

## Use clear field naming conventions

Field names should be descriptive, consistent, and easy to interpret.

A useful naming pattern is:

`[entity]_[attribute]_[unit]`

For example:

`user_login_count_daily`

Avoid:

- Unclear abbreviations
- Inconsistent casing
- Special characters
- Naming patterns that vary across datasets

## Document field metadata

For each field, record:

- Data type
- Plain-language description
- Null handling
- Units or range, when applicable
- Example value

For example:

| Field | Type | Description | Nullable | Notes |
| --- | --- | --- | --- | --- |
| `user_id` | String | Unique identifier for each user | No | Primary key |
| `login_timestamp` | Timestamp | Time of last login | Yes | UTC format |
| `region` | String | User's country or region | Yes | ISO country code |

## Record transformations

When fields are created or modified through transformation or feature engineering, document:

- Source datasets
- Transformation scripts or queries
- Purpose of the transformation
- Dependencies
- Change history

Link transformation changes to version-control records where possible.
