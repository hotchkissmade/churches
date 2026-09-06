<!--
  Generated file — do not edit here.

  Source: macmini/src/templates/churches-readme.md in hotchkissmade/churches-acquisition,
  written out by macmini/src/jobs/github-sync.ts on each sync. Anything changed
  directly in this repo is overwritten on the next run.
-->

# Churches

Hotchkissmade is building the open-source database of US Churches. Starting with government-released public data and enriched with biographical, theological, and service-related data.\*

\*enrichment work not yet available in public release

**Browse the data:** [churches.hotchkissmade.org](https://churches.hotchkissmade.org) · **Methodology:** [hotchkissmade.com/research/churches](https://www.hotchkissmade.com/research/churches)

## Stats

<!-- STATS_START -->
| Metric | Count |
|--------|-------|
| Churches with website | 119,265 |
| Churches with social media | 16,934 |
| **Total** | **136,199** |

*Last updated: 2026-09-06*
<!-- STATS_END -->

## What's in a record

One JSON file per organization, at `data/{STATE}/{EIN}.json`:

```json
{
  "ein": "010718551",
  "irs_name": "CHURCH OF CHRIST AT WASILLA INC",
  "irs_city": "WASILLA",
  "irs_state": "AK",
  "irs_zip": "99654-3400",
  "latitude": 61.60224151611328,
  "longitude": -149.3536376953125,
  "geocode_source": "overture_maps",
  "google_result_title": "Home ‹ church of Christ at Wasilla",
  "website": "https://churchofchristwasilla.com/",
  "website_hostname": "churchofchristwasilla.com",
  "match_reason": "The website name and content match exactly with the Church of Christ at Wasilla, Inc., and the location is the same city.",
  "match_type": "website"
}
```

| Field | Description |
| --- | --- |
| `ein` | IRS Employer Identification Number. The join key against ProPublica, GuideStar, and NCCS. |
| `irs_name` | Organization name as filed in the IRS Business Master File. |
| `irs_city` | City, as filed in the BMF. |
| `irs_state` | Two-letter state or territory code, as filed in the BMF. |
| `irs_zip` | ZIP code, as filed in the BMF. |
| `latitude` | Decimal latitude. Present only when the organization geocoded. |
| `longitude` | Decimal longitude. Present only when the organization geocoded. |
| `geocode_source` | Origin of the coordinates, e.g. `overture_maps`. Present only alongside coordinates. |
| `google_result_title` | Page title of the matched search result. |
| `website` | The matched church website. |
| `website_hostname` | Hostname of the matched website. |
| `match_reason` | The reasoning recorded when the match was accepted. |
| `match_type` | How the match was established, e.g. `website`. |

The IRS Business Master File identifies church-like nonprofits by EIN but records no web presence. The matched website, its search-result title, and the recorded match reasoning are what this dataset adds.

`stats.json` carries the same counts as the table above, plus a per-state breakdown.

## Methodology

### Step 1: Finding churches in public data 🔬

The IRS hosts a public dataset called the Exempt Organizations Business Master File. It's a quarterly released set of CSVs with basic profile information for millions of US nonprofits. With some filtering, that list can be honed to about 270,000 church-like entities. It's difficult to find a real total of churches in the US, as not every church files for nonprofit status for reasons like scale (maybe they're just some friends in a living room) or because they're anti-government zealots.

### Step 2: Church-like nonprofits 🤝🏼 Web search results

Utilizing a paid dataset containing web search results for every church-like nonprofit in the IRS data, a small LLM hosted on a baseline M4 Mac mini performed over a million prompts to determine if a church's search results appeared to match the profile information from the IRS. For around 48% of churches in the IRS data, we'll get a match. Not every match is correct, or even a website at all (lots of small churches are Facebook only!).

### Step 3: Acquire website 🧑🏼‍💻

A copy of the church website is acquired for further processing. Mostly drama-free. The web is quickly fronting itself with anti-bot armor, so retrieving updated information in the future will be more complicated. The goal is > 100,000 churches.

### Step 4: Cleanup 🧹

The IRS data we talked about before wasn't especially clean. Many entities from entirely different faiths were tagged in with church metadata. Taking some passes to clean these out. More complicated is trying to find church-like orgs like schools or missions organizations which don't have strong flags indicating so.

### Step 5: Enrich ✨

For each church, an enrichment LLM task is run to determine about 75 standardized fields.

### Step 6: Release 🆓

The enriched church records are released to GitHub in real time as they are processed or updated.

### Step 7: Derivative projects 🛠️

The bulk collection of websites contained several treasures worth diving deeper into. The biggest of which is sufficient sermon archives to help drive the /sermonsense project.

Additionally, several proof-of-concept projects will be created to help demonstrate and increase project visibility.

### Step 8: Community ⛪️

A dataset of this scale is never truly completed. The long-term aspiration is to find a team of volunteers to increase the quantity of enriched churches, the quality of the data, and to help find new ways to increase the utility of the database so that the American church can be better understood from a distance.

*The process is documented as a confidence measure for the dataset, but none of the tooling or intermediate data described above will be publicly released as part of this project.*

## License

This database is licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) (`CC-BY-NC-4.0`).

**You are free to:**
- Share and adapt this data for non-commercial purposes
- Use it for research, education, and personal projects

**Under the following terms:**
- **Attribution required**: Credit this project appropriately
- **Non-commercial only**: Commercial use is strictly prohibited

The IRS Business Master File is public domain and requires no attribution. Geocoding is derived from [Overture Maps Foundation](https://overturemaps.org) data.

## Citation

```bibtex
@misc{hotchkissmade_churches,
  title  = {US Churches Database},
  author = {Hotchkiss, Kyle},
  year   = {2026},
  url    = {https://github.com/hotchkissmade/churches},
  note   = {Licensed CC BY-NC 4.0}
}
```
