---
layout: post
title: "GreenForecast: Details for Energy People"
---

*Below are details about [greenforecast.au](http://greenforecast.au/) specifically for "energy nerds". For an introduction to greenforecast.au, see [here](/greenforecast)*
---
### Greenness Details:

For simplicity, the analysis assumes fuel sources are either 'Green' or 'Not Green'. Wind, solar and hydro are 'Green' while coal, diesel and gas (in various forms) are not. Reality is not so simple but these complexities don't currently substantially affect the overall result.

Batteries and pumped storage will be more important in coming years but are currently small. The model currently assumes they do not affect the level of greenness when discharging (or charging). A future improvement could be to assume they discharge with the same level of Greenness that they were charged with (typically high, because it is cheap to charge when solar is abundant). Currently, this effect would be too small to notice.

### Is your carbon footprint really lowered by using at times of high Greenness?

It's Complicated, but yes.

Currently, the vast majority of electricity that is generated is "used" in less than a second. This will remain true until we have (HEAPS) more battery and pumped storage. It makes intuitive sense that the Greenness of your electricity is calculated from whatever power plants are generating right now.

But if someone moves their consumption from a 'dirty' time to a 'clean' time, does that _cause_ the total production of green energy to increase? In the short term, generally not?Wind, solar and hydro typically generate regardless of demand; if usage increases or decreases, they rarely change output, because their fuel is free. (Hydro does respond to demand changes in the short-term, but ultimately the total amount of water available is non-negotiable). This leaves only gas that responds to changes in demand, which means moving consumption from one time to another simply changes _when_ some gas turbine runs, not how much.  
  
Now, there is an exception to this: when there is very high Greenness, excess supply (high wind and sun) the price goes negative. Here, solar and wind plants will reduce their output to avoid excess supply causing problems in the grid. Moving consumption to these times would indeed enable higher renewable generation. Currently, this happens only on occasional days in SA during spring/summer, but will increase in prevalence in coming years.: more people share the same amount of green energy. But in the long term, moving our consumption to times of high Greenness _does_ enable more green power plants to be built: money that would otherwise be needed for expensive batteries (or rapid-response gas turbines) is spent on cheap wind and solar. Indeed, there are already areas where it is less profitable to add wind/solar because of excess capacity.

Put another way, if everybody magically decided to schedule their big loads (eg heating/cooling, EV charging) during times of high Greenness, our transition to 100% renewables would be faster and our electricity bills cheaper.

### What about WA? NT?

Sorry, this system is designed around NEM data, which only covers 5 states (and ACT folded in with NSW). If you're a machine learning engineer and you'd like to design a system that uses WA/NT data, you're welcome to contribute, start a conversation on the [github page](https://github.com/mattyyeung/GreenForecastPublic). Alternatively, simply build a HVDC link across the Nullarbor and you can save yourself the ML headache.

### Could this be done in the USA? Europe?

Yes! However, it will take quite a bit of effort. Each different market (there are 10+ in the USA alone) provides similar data but in different formats. If you're interested, get in contact.

### How are Interconnectors treated - and why isn't Tasmania always 100% Greenness?

Interconnectors?The big transmission lines that link states together affect Greenness and price. Electricity imported from another state is assumed to have the same Greenness as the state it's coming from - it's split into "imported green energy" and "imported fossil energy". This is why Tasmania, with no significant fossil plants, isn't always at 100% Greenness - imported electricity from Victoria has lower Greenness. Similarly, Victoria is more Green when it is importing from Tasmania.

### What is "Wholesale Price"?

Power companies and power plants buy and sell electricity to each other on a "national" spot market, operated by AEMO. Every 5 minutes there is a new market price for each region (state). Every-day consumers typically don't have direct access to this market: their power company buys on behalf of all its customers. Customers pay a flat fee to the power company so the minute-to-minute fluctations of the market don't affect them directly. However, larger commercial/industrial customers may be directly exposed to market fluctuations and there are also some (TODO) power companies that offer 'pass-through' pricing to households.

Note that the wholesale price of electricity only makes up part of your power bill: other "fixed costs" for infrastructure eg "poles and wires" also contribute.

### When are forecasts less accurate?

*   If the weather forecasts turn out to be wrong then wind and solar projections will also be wrong. If the weather forecast for some day changes as it gets closer, the model will adjust Greenness and Price predictions too.
*   If there's an unexpected outage of a large power plant or interconnector then predictions will be wrong. This affects price predictions more than Greenness. Planned outages are taken into account.
*   Times of high market volatility (eg 2022) result in lower-accuracy price forecasts
*   This model is not specifically designed to predict the large price spikes that sporadically occur; this would not contribute to this project's goals.

### How does this compare to other predictions?

Greenness: [watttime.org](https://www.watttime.org) uses different measure in place of Greenness: a _marginal_ rate not an absolute one (see their [methodology](https://www.watttime.org/marginal-emissions-methodology/) and [API](https://www.watttime.org/api-documentation/#introduction) pages).

Price: AEMO provides "forecasts"?Predispatch arguably isn't intended as a forecast but is often used as such up to 48h in the future. Standing on these shoulders, the GreenForecast.au improves these predictions a little. Beyond 48 hours, grenforecast.au seems to be the only one.

If you would like to compare these predictions to your own forecaster or you know of any public alternatives, please get in touch! Mail info\[AT\]greenforecast.au or [@GreenForecastAu](https://twitter.com/GreenForecastAu) on twitter.

### How does performance compare across states?

NSW and VIC are more accurate, laregly due to their size (stability). SA is the hardest: it is a smaller market and has the highest proportion of unpredictable generation.

### How has the 2022 energy crisis affected predictions?

In 2022, the market is (a) more volatile and (b) has higher average prices. In particular, the market 'shutdown' in June 2022. The model certainly didn't predict that, though Greenness predictions were still pretty good.

From a machine learning point of view, the model did a mediocre job of predicting post-crisis prices (about 3x worse) when it was trained on only pre-crisis data. However, now that post-crisis data is available to train on, the model has a similar accuracy (in percentage terms) to before.

### How is the rapid growth of renewables affecting the model's accuracy?

Not much, because this growth is already reflected in the raw data coming from AEMO. Of course, Greenness factors are now much higher than they were!

### Why split state-by-state? Don't local effects matter?

There is no great reason for this. The NEM is split up this way and so is the data.

---
Related:
- [greenforecast.au](http://greenforecast.au/)
- [Introducing GreenForecast.au](/greenforecast)