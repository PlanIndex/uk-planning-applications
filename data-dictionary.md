# Data dictionary

Every council file has the same columns, in this order. Dates are
ISO 8601 (YYYY-MM-DD). An empty cell means the council has not
published that value.

| Column | Meaning |
| --- | --- |
| reference | The council's own application reference, as published |
| address | The site address, as shown on the PlanIndex page |
| postcode_district | The outward code of the site postcode, e.g. M20 |
| proposal | The description of the proposed works, as published |
| category | The PlanIndex category, e.g. Householder, Trees |
| status | Where the application stands: Awaiting decision, Granted, Refused, Withdrawn, At appeal |
| received_date | When the council received the application |
| validated_date | When the council validated it |
| decision_date | When it was decided |
| decision | The decision wording, as published |
| planindex_url | The record's page on PlanIndex, for credit and context |

Values are verbatim from the council register apart from whitespace,
which is collapsed to single spaces in the proposal.
