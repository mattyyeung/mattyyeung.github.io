---
layout: post
title: "GreenForecast: Details for Tech People"
---

*Below are details about [greenforecast.au](http://greenforecast.au/) specifically for tech folks. For an introduction to greenforecast.au, see [here](/greenforecast)*

### Is there an API available?

Please get in contact, see links in the footer. I'd love to help.

### What kind of model is it?

For Greenness, a simple neural net (MLP) is trained for each timestep (ie 2 hours in the future, 4 hours in future, ...). The models predict the outputs of each fuel type, from which greenness is derived as a simple proportion.

For price, the models just predict the target value. The neural nets are ensembled with an XGBoost model for each timestep for a small (~5%) improvement in performance. This is all repeated for price and Greenness for each state, for a total of around a thousand sub-models.

### What are the model inputs?

Roughly a thousand features are collected at inference. Data comes from AEMO, the BoM, a government public holidays database and several derived values.

### What is the training dataset?

A custom-prepared dataset with around one million datapoints for each NEM region dating back to 2010. Some basic (hand-crafted) data augmentation bulks out scarce post-2022-energy-crisis data. For details, see TODO on github.

### What types features are used?

Date features, current/forecast weather, current/forecast NEM data (generation & availability by fuel type, price, interconnectors), price lags and Greenness lags.

Each sub-model (eg Price 48h in advance) uses a hand-crafted subset of around 100 features - largely just excluding lags that are less relevant. For example, when forecasting 48h in advance, the weather forecast 5 days in the future is irrelevant.

### How does this model compare to architecture X?

Experiments so far: Random Forests, ARIMA, DeepAR, TFT, NHiTS, NBEATS, LGBoost, Prophet, various variations on MLPs. Some experiments were extensive, others weren't. Simple MLPs and XGBoost have performed the best. \[results TODO\]. Suggestions, feedback and experimentation with alternatives welcome.

### Why might this architecture be performing best?

This problem may differ from standard time-series forecasting problems (eg M5) because there are good covariant features and forecasts (eg weather, wind output, etc) available. With basic feature engineering (eg selected past and forecast lags) it perhaps looks more like a tabular data problem than standard time-series forecasting. If so, strong performance from simple neural networks and gradient boosting is not surprising. TODO

### What other techniques were used to improve results?

In rough order of effectiveness:

*   As always, getting more data (longer timespan and extra features) made the biggest difference. For example: Some solar data is not available before 2016, but a random forests regressor does a great job of predicting this data back to 2010 from other available data (weather, installed base). See RooftopBackcast.ipynb in the dataset generator.
*   Basic data augmentation - interpolating between datapoints and duplicating points with some features scaled in a logical way (eg all price features increased by 5%)
*   Training each sub-model on a preselected subset of features, eg the submodel predicting 48 hours ahead was not shown forecasts for 96 hours ahead. This minimises ["uninformative features"](https://arxiv.org/abs/2207.08815)
*   Encoding date features as numeric rather than embeddings improved accuracy, again reducing uninformative features.
*   Using a holdout test set to choose architecture and hyperparameters but making that holdout data available for final training. Held out data is the most recent available and therefore the most releveant to today's market behaviour. A validation set was still used to prevent overfitting.
*   Various training tricks promoted by fast.ai

### Can I try my own model with the dataset?

Yes! Currently you'll need to run the dataset generator yourself, the datasets themselves are not yet uploaded. Please share your results! Contact below.

### Which metrics are used?

From most-convenient to most-comprehensive:

*   MAE for price 84h in the future on VIC1 dataset (ie the feature named 'VIC1\_Price\_Tp84'). This is selected because price is more variable than Greenness, the time is in middle of the range and not an even multiple of 24h
*   MAE for all the various fuel sources 84h ahead
*   MAE for price for all timesteps from 2h to 168h ahead for VIC1 dataset
*   MAE for price across all timesteps and all regions
*   MAE for price and Greenness separately for all timesteps and all regions

There's no strong reason for choosing MAE over MSE - brief comparison experiments were inconclusive. Price forecasts vary across several orders of magnitude (even after clamping values to ±$1000/MWh) so MSE would only emphasise that further. This project prioritises the 'every-day' case over outlier events, so MAE wins from that point of view.

### Why not use the same model/ensemble for each state?

Bespoke models for each state performed better than a single model trained on all states (perhaps because there is already a million datapoints per state to train on) or a single model that predicts all states at once (perhaps because this greatly increases the number of features)

### Can I use the dataset for my own project?

Yes. Github TODO (See contact details below for now)

### How long does training take?

Training a thousand sub-models takes about 3 days on a single consumer GPU. Inference takes around ten minutes, most of which is gathering data.

### How is the model hosted?

Dataset generation and model training are offline. Inference is in AWS Lambda, kicking off every two hours. This website frontend is just a static page on S3. For details, see the deployment diagram on [github](https://github.com/mattyyeung/GreenForecastPublic).


---
Related:
- [greenforecast.au](http://greenforecast.au/)
- [Introducing GreenForecast.au](/greenforecast)