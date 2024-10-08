# Version history: {yet to be committed to code}
## 1.2
- Changed logic with whether to discharge from the battery or import from the grid in "Preserve battery?" energy control flow
    - Decreased when to pull from grid from 5c to 2c
    - Applies now from 10am, not 1pm, and not during demand period
- Solcast actuals/forecasts/generation filename format change to YYYY-MM-DD
- 5 minute usage logging
    - Buy price
    - Sell price
    - Current usage
    - Battery charge
    - Generation
    - kWh export last 5 mins
    - kWh import last 5 mins
- Update to logic
    - If buy price is under 3c and battery is full, turn off inverter and draw from grid instead, but only outside of demain period
- Added notifications for price alerts
    - Notification if buy price is under -$0.03 (paid to use power, turn on appliances)
    - Notification if sell price is over $0.50 (price spike)
    - Notification if difference between buy and sell is under 3c (possibly an API problem)
- Changed all 5kW export to 10kW
- Changed base battery from 19.2kWh to 38.4kWh
- Changed force charge from 90% down to 80% in preparation for upcoming demand period (due to increase of battery size)
- Changed the logic of when to charge and discharge, due to larger battery size
- Added notification to phone if it is detected that any power is being imported during a demand window.
- Added "Storm" mode
    - Will not sell power at the lower prices so that it is kept in case of power outages
    - Toggled through an HA button

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
