# PlanIndex open data: new UK planning applications

Planning applications that PlanIndex first saw in the last 30 days, one
CSV per local planning authority, refreshed every night.

Last updated 21 October 2026: 289645 applications across 360 councils.

- `councils.csv` lists every council with a file and how many rows it holds.
- `councils/<council>.csv` holds that council's applications.
- `data-dictionary.md` describes every column.

## Licence and credit

CC BY 4.0 (see `LICENSE`). Credit "PlanIndex, planindex.co.uk" with a link to
https://planindex.co.uk/ or to the `planindex_url` of the record you use.

## What is in it, and what is not

Each row is a public planning record as its council published it, with a
link to its page on PlanIndex. Records withdrawn from PlanIndex at the request
of the people involved are left out. There are no applicant or agent
names. Coverage follows what each council publishes; a council missing
here may simply have had nothing new, or may not publish to a source we
can read.

More about the data: https://planindex.co.uk/open-data
