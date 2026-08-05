# IA Land Sites — Off-Market Sourcing for a Potential Energy Campus

Working repo for sourcing 500+ acre land in Iowa for a potential energy campus.
Built around **off-market origination**: assemblages, willing-but-unlisted sellers,
and local relationship channels.

**Live desk:** https://ezraharris385.github.io/IA-Land-Sites/
Link-only — excluded from search indexing, no login required.

## The desk

`index.html` is the working tool. It reads `data/*.json` at load time and derives
everything on screen.

| Tab | Purpose |
|---|---|
| **Target screen** | Every screened Iowa county scored on landform, assemblage difficulty, ordinance status and pool depth. Positions held are marked. |
| **Pipeline** | Every site on record, with the county screen joined on and net buildable acreage derived. |
| **Analyst** | Re-derives on every load and every refresh. Cross-references private records against the public screen and reports contradictions, gaps, concentration risk and coverage holes. |
| **Execution** | Contacts ranked by acres reachable per hour, each mapped to the sites and counties it covers. |
| **Progress** | Append-only record of what has been done. Retrospective only. |
| **Data** | Everything ingested, what it held, and what it was missing. |

## How it updates

The repo is the database. **Editing a JSON file and pushing is the entire update
path** — no build step.

```
data/counties.json    public county screen (USDA farm structure, landform, ordinance, COG)
data/sites.json       every site pursued — acreage, hydrology, status, owner, flags
data/contacts.json    organisations and people, mapped to counties and sites
data/activity.json    append-only log of what has been done
data/documents.json   every file ingested, what it held, what it lacked
data/brief.json       the written analysis, regenerated when data lands
```

Net buildable acreage, owners per section, county scores, coverage gaps and every
analyst finding are computed in the browser. None of it is hardcoded — change the
data and the conclusions change.

### Adding data

Send any file — spreadsheet, PDF, notes, a call log, a parcel export, a photo of a
plat book page. It gets normalised into the schema above, appended, and pushed. The
site updates in about thirty seconds and every number re-derives.

To log outreach by hand, append to `data/activity.json`:

```json
{ "id": "A-008", "date": "2026-08-06", "type": "outreach",
  "subject": "Called MIGP — Jefferson Fosbender",
  "detail": "Asked for land inventory over 300 acres across the nine counties.",
  "outcome": "Sending a Kossuth and Wright list this week.",
  "refs": ["C-002"], "metric": {} }
```

Then set that contact's `status` in `contacts.json` to anything other than
`not_contacted` and the analyst stops flagging it.

## Derived fields — read these with care

- **Owners per section** = 640 ÷ county median farm size. An optimistic floor: the
  USDA census counts *operations*, and large operators farm rented ground across
  several owners, so true ownership is more fragmented. Calibrate against a real
  parcel dissolve.
- **Net buildable acres** = gross × (1 − hydrology haircut), keyed to recorded
  hydrology; a real tillable figure overrides the estimate. Screening estimates,
  not delineations.
- **County scores** weight landform 30, assemblage 28, ordinance 27, pool depth 15.
  The farm data is USDA's; landform and ordinance inputs are researched judgments.
- **Ordinance status moved nine times during 2026.** Re-verify with the county
  before spending money.

## Reference material

| File | Purpose |
|---|---|
| [survey.html](survey.html) | Narrative survey — method, incentive stack, off-market channels, assemblage arithmetic |
| [docs/site-criteria.md](docs/site-criteria.md) | What we're looking for — screen parcels before spending time on owners |
| [docs/sourcing-playbook.md](docs/sourcing-playbook.md) | Channel list — data-driven, relationship, and creative plays |
| [docs/assemblage-strategy.md](docs/assemblage-strategy.md) | Assembling multiple parcels without blowing up pricing |
| [docs/outreach-scripts.md](docs/outreach-scripts.md) | Call scripts, voicemail, letter templates, objection handling |
| [docs/iowa-data-sources.md](docs/iowa-data-sources.md) | Where to pull ownership, parcel, and infrastructure data for free |
| [tracker/pipeline-tracker.csv](tracker/pipeline-tracker.csv) | Original parcel/owner schema that `data/sites.json` follows |
| [tracker/outreach-log.csv](tracker/outreach-log.csv) | Original touch-log schema that `data/activity.json` follows |

## Operating principles

1. **Desk work before phone work.** Build the parcel universe from county GIS and
   transmission maps first. Every call should be to an owner whose land already
   passes the screen.
2. **Discreet, not deceptive.** We describe the project as exploring the feasibility
   of a potential energy campus. That's the real story. We don't name the end user,
   and we never claim to be something we're not.
3. **Options over purchases.** Early control via option agreements keeps cost and
   risk down and lets us walk from an assemblage that doesn't complete.
4. **Local faces open local doors.** A trusted county-seat attorney, farm manager,
   or broker making the introduction beats a cold call every time.
5. **Log everything.** Owner conversations in rural Iowa travel fast. Knowing
   exactly what we've said to whom is how we stay consistent.

## Sources

USDA 2022 Census of Agriculture (Iowa county tables, parsed for all 99 counties) ·
Iowa Geological Survey landform regions · Iowa DOR data centre tax guidance and
HF 976 · Iowa Code 427B · ICOG council directory · county ordinance research.
