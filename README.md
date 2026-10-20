# UK planning applications

Planning applications from every UK local planning authority, as CSV, from
[PlanIndex](https://planindex.co.uk): one file per council covering the
applications first seen by PlanIndex in the last 30 days, rebuilt every
night. 373 councils across England, Scotland, Wales and Northern Ireland.

If you use the data, credit PlanIndex with a link (see Licence below). That
is the whole price.

## Files

```
data/<council-slug>.csv   one file per council, the last 30 days
councils.csv              the councils: slug, name, nation, region, rows in file, PlanIndex hub, council portal
manifest.json             when the files were built, the window they cover, totals, schema version
data-dictionary.md        every column, with its meaning and the values it can take
LICENSE                   CC BY 4.0
```

Files are UTF-8, comma-separated, quoted where a value contains a comma or a
line break, with a header row and LF line endings. Dates are `YYYY-MM-DD`.
Empty means the council did not publish that value.

The council slug is the one in the PlanIndex URL, so
`data/leeds.csv` holds the applications at
`https://planindex.co.uk/planning-applications/leeds`.

## Columns

| Column | Meaning |
| --- | --- |
| `reference` | The council's own reference, as published, for example `26/01431/LI` |
| `council` | The planning authority's name |
| `council_slug` | Its slug on PlanIndex and in this repository |
| `address` | The site address as the council published it |
| `postcode_district` | The outward code, for example `LS6`, from the site postcode or reverse-geocoded from the council's coordinates |
| `proposal` | The description of the proposed works, as published |
| `category` | PlanIndex's classification of the application type: householder, full, outline, reserved matters, listed building, advertisement, tree works, lawful development, prior approval, discharge of conditions, variation, or other |
| `status` | Where the application is: undecided, approved, refused, withdrawn, or other, as PlanIndex reads the council's status |
| `received_date` | When the council received it |
| `validated_date` | When the council validated it |
| `decided_date` | When the council decided it, if it has |
| `decision` | The decision as published, where there is one |
| `first_seen_date` | When PlanIndex first read the record |
| `planindex_url` | The permanent page for the application |
| `source_url` | The entry on the council's own portal, where the council publishes one |

`data-dictionary.md` is generated with the files and is the authoritative
version of this table.

## What is and is not here

- Applications are included once they carry an address and a description;
  records the council published without either are left out, as they are on
  the site.
- A case that appears on more than one council's register (joint portals,
  national parks) appears once, under the authority that decides it.
- Names of applicants and agents are never included, nor are documents,
  drawings or public comments. Application pages on PlanIndex link the
  council's documents; nothing is hosted here.
- `first_seen_date` is when PlanIndex read the record, not when the council
  published it. When a council joins the index its back catalogue arrives in
  one go, so a file can hold old applications that are new to the index.
- The window is 30 days of first-seen records. For anything older, the
  PlanIndex page for the application, council, ward or postcode district is
  the place to look, and every page states the date its data was last read.

## History

Every nightly build is a commit, so the repository's history is the
day-by-day record of what each council published. `git log -- data/leeds.csv`
shows Leeds over time; checking out an older commit gives the files as they
stood that night.

## Using the files

The raw URL of any file works directly:

```
https://raw.githubusercontent.com/planindex/uk-planning-applications/main/data/leeds.csv
```

With DuckDB, all councils in one query:

```sql
SELECT council, status, count(*) AS applications
FROM read_csv_auto('data/*.csv')
GROUP BY council, status
ORDER BY applications DESC;
```

## Related data

- Decision times, every ranked council, as CSV:
  https://planindex.co.uk/planning-decision-times.csv
- Approval rates: https://planindex.co.uk/planning-approval-rates.csv
- How those are measured:
  https://planindex.co.uk/planning-decision-times/methodology

## Licence

The files are published under
[Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/)
(see `LICENSE`). Use them for anything, including commercial work, and
credit PlanIndex with a link where the data appears:

> Data: [PlanIndex](https://planindex.co.uk)

The facts in each row are the public records of the planning authority named
in it, collected from its published register. Where a council's data reaches
PlanIndex through planning.data.gov.uk or PlanIt, the data dictionary says so.

## Takedowns and contact

If you are named on an application and want its page removed or its address
withheld, use https://planindex.co.uk/takedown; the change reaches these
files on the next build. For anything else, open an issue or use
https://planindex.co.uk/contact.
