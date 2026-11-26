# Toronto & GTA emergency plumbers and electricians: open data

Open dataset of **7,011 residential emergency plumbers and electricians in Toronto and the Greater Toronto Area**, published by [Hailtrades](https://hailtrades.com). Hours, 24/7 and emergency availability, licence numbers, free-quote flags, and (where a provider publishes them) dollar call-out and hourly fees.

- **Licence:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Use it for anything, including commercially, as long as you credit Hailtrades and link to <https://hailtrades.com>.
- **Cite as:** `Hailtrades (hailtrades.com). Toronto/GTA emergency trades directory. https://hailtrades.com/data. CC BY 4.0.`
- **Live source of truth:** <https://hailtrades.com/data>
- **Query it with an AI agent:** public MCP server at `https://hailtrades.com/mcp` (Streamable HTTP, no login). Tools: `search_providers`, `get_provider`, `report_contact`. Docs: <https://hailtrades.com/for-agents>, OpenAPI: <https://hailtrades.com/openapi.json>, <https://hailtrades.com/llms.txt>
- **Snapshot in this repo:** generated 2026-11-26. Counts below are for this snapshot.

## Files

| File | Rows | What it is |
|---|---|---|
| `data/providers.csv` | 7,011 | One row per provider, flattened. Multi-value fields use `;` as separator. |
| `data/providers.json` | 7,011 | Full records: per-day hours, per-field sources, licences, service areas, contact channels, coordinates. |
| `data/fees.csv` | 929 | One row per observed fee, with source URL and date. |
| `datapackage.json` | | Frictionless Data descriptor. |
| `CITATION.cff`, `.zenodo.json` | | Citation and Zenodo metadata. |
| `distribution/` | | Dataset cards for Hugging Face, Kaggle, data.world. |

Trade split: 4,881 electricians, 2,092 plumbers, 38 both. Providers with a licence number: 3,486. Flagged 24/7: 1,750. Free-quote flag: 794 rows in `providers.csv` (see Caveats). Dollar call-out fee: 25 providers in the CSV (more in `fees.csv`). All figures are as published by the providers or their sources, not independently confirmed.

## Data dictionary: `providers.csv`

Empty means **unknown**, not "no".

| Column | Description |
|---|---|
| `id` | Stable Hailtrades provider id (`prv_...`). |
| `name` | Business name as published. |
| `trades` | `plumber`, `electrician`, or `plumber;electrician`. |
| `city`, `district`, `region` | Municipality, district (e.g. Scarborough, North York), regional municipality. |
| `postal_code`, `fsa` | Postal code and forward sortation area (first 3 characters). |
| `street_address` | Business address. |
| `phone`, `email`, `website` | Public contact details. Phone numbers are published in the form served by hailtrades.com. |
| `preferred_contact` | `call`, `text`, `email`, `form`, or `unknown`. |
| `is_24_7`, `offers_emergency`, `weekend_available` | Booleans where known. |
| `emergency_response_minutes` | Stated emergency response time, minutes. |
| `services` | `;`-separated service tags (e.g. `sewer_backup`, `panel_upgrade`). |
| `service_municipalities`, `service_districts`, `service_fsas` | `;`-separated service area. |
| `hours_regular`, `hours_emergency` | Opening hours text. Per-day structured hours are in the JSON. |
| `callout_fee_cad`, `after_hours_callout_fee_cad`, `quote_fee_cad`, `hourly_rate_cad` | Fees in CAD as stated by the provider. `quote_fee_cad` is `free` when the provider states free quotes/estimates. |
| `licences` | `;`-separated, `AUTHORITY number` (e.g. `ESA_LEC 7008435`). As published by the provider or a listing; **not** verified against the official register (see `verified_on_registry` in the JSON). |
| `years_in_business` | Years in business where stated. |
| `review_sources` | Sources with review counts and links. Review text and star ratings are **not** included. |
| `source_urls` | `;`-separated URLs the record was built from. |
| `last_verified` | Date Hailtrades last verified the record. Mostly empty in this snapshot. |
| `url` | Provider page on hailtrades.com. |
| `mock` | Always `false` in this release. |

## Data dictionary: `fees.csv`

`provider_id`, `provider_name`, `trades`, `city`, `district`; `fee_kind` (`callout_fee`, `after_hours_callout_fee`, `quote_fee`, `diagnostic_fee`, `hourly_rate`, `after_hours_hourly_rate`, `minimum_charge`); `service`; `is_free`; `amount_min_cad`, `amount_max_cad`; `waived_if_hired`; `conditions`; `source`; `source_url`; `observed_at` (UTC); `method`; `mock`.

## Caveats

- Collected from public web sources: business websites, directories, and the Ontario electrical licensing listings. Fees are as stated on the observed date. Confirm with the provider before booking.
- Hours, availability and "24/7" are claims by the provider unless noted.
- Third-party review text and star ratings are excluded because of source terms.
- Hailtrades is a directory. It does not take payment, perform work, or guarantee service quality.
- Emergency in progress (fire, smoke, gas smell, someone hurt)? Call 911 first.

## Update cadence

Refreshed quarterly, with a new snapshot tagged on GitHub. The live files at <https://hailtrades.com/data> may be newer.

## Corrections and removal

Providers can request corrections or removal via <https://hailtrades.com>. Open an issue here for data errors.

## Licence

Data: CC BY 4.0. Attribution text: "Hailtrades (hailtrades.com)" with a link to <https://hailtrades.com>.
