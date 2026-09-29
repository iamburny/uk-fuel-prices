# UK daily average fuel prices

The daily UK average pump price of unleaded (E10), super unleaded (E5), diesel (B7) and premium
diesel, in pence per litre, from every forecourt reporting to the UK Government's
[Fuel Finder scheme](https://www.gov.uk/government/collections/fuel-finder).

Published by [Fuel Tracker UK](https://fueltracker.uk), where the same series is shown as tables,
month by month, alongside a monthly report:

- **Tables and method:** https://fueltracker.uk/fuel-prices/history
- **Monthly reports:** https://fueltracker.uk/guides/uk-fuel-price-report
- **Live CSV (the source of this file):** https://fueltracker.uk/fuel-prices/history/uk-fuel-prices-daily.csv

## The file

[`data/uk-fuel-prices-daily.csv`](data/uk-fuel-prices-daily.csv), one row per fuel per day, oldest
first:

| Column | Meaning |
|---|---|
| `date` | UTC calendar day, `YYYY-MM-DD` |
| `fuel_type` | `E10`, `E5`, `B7_STANDARD` or `B7_PREMIUM`, as the Fuel Finder scheme names them |
| `fuel_name` | Human-readable name |
| `average_price_pence_per_litre` | Mean of that day's price readings for that fuel |
| `price_readings` | Number of readings behind the average |

## How the figure is made

Each day's figure is the mean of the price readings recorded that day: one per forecourt, plus one
each time a forecourt changed its price. Readings too far from that day's median to be real
(normally more than 15% below it or 30% above, such as a 299.9p placeholder) are left out; no price
is altered. A fuel's day is left out when it rests on fewer than 500 readings, and each fuel's
series starts at its first run of seven consecutive such days, so the record starts in July 2026.
Only completed days are included. Biodiesel (B10) and HVO are sold at too few forecourts to have a
national series.

The file here is refreshed from the live CSV once a day, at 02:30 UTC, by the workflow in `.github/workflows/update.yml`.

## Licence

Contains public sector information licensed under the
[Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

If you use it, please credit "Fuel Tracker UK, from UK Government Fuel Finder data" and link to
https://fueltracker.uk/fuel-prices/history.

Fuel Tracker UK is independent and is not affiliated with or endorsed by HM Government.
