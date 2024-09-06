# Version history:
## 1.1.1
- Changed logic with whether to discharge from the battery or import from the grid in "Preserve battery?" energy control flow
    - Decreased when to pull from grid from 5c to 2c
    - Applies now from 10am, not 1pm, and not during demand period
- Solcast actuals/forecasts/generation filename format change to YYYY-MM-DD

## 1.1
- Addition of an optional "aggressive mode" to force more energy out of your battery, to potentially maximise financial return
- Alert if Localvolts API is not behaving correctly (too many "forecasts" and no "Expected"), and puts inverter into "no export" mode
- Added a check for demand pricing and will limit taking from grid if the price is really cheap if within demand period, we don't want to import anything during a demand period
- Updated Grafana dashboard to show
    - Whether solar is currently being curtailed or not
    - Daily buy and sell totals
    - Monthly "so far" buy and sell totals
    - Last 12hrs buy sell kWh on same graph as last 24hrs buy and sell prices

## 1.0
- Original compilation of the various repositories into one merged one
- Addition of preparing for evening and morning price surge/spikes
- Addition of a Grafana dashboard (bit prettier than Home Assistant)
- Addition of buy/sell price history logging
