Prophet, developed by Facebook, is a popular time series forecasting tool that includes several hyperparameters to fine-tune the model. Here is a list of the main hyperparameters in Prophet:

### Model Parameters
1. **`growth`**: String specifying the type of trend to fit. Either `'linear'` or `'logistic'`.
2. **`changepoints`**: List of dates at which to include potential changepoints. If not specified, potential changepoints are automatically selected.
3. **`n_changepoints`**: Number of potential changepoints to include.
4. **`changepoint_range`**: Proportion of the history in which trend changepoints will be estimated. Defaults to 0.8 for the first 80%.

### Trend Parameters
1. **`changepoint_prior_scale`**: Parameter controlling the flexibility of the automatic changepoint selection. Larger values allow for more changepoints.
2. **`seasonality_prior_scale`**: Parameter controlling the strength of the seasonality model.
3. **`holidays_prior_scale`**: Parameter controlling the strength of the holiday components.
4. **`mcmc_samples`**: If greater than 0, will do full Bayesian inference with the specified number of MCMC samples. Defaults to 0 for MAP estimation.
5. **`interval_width`**: Width of the uncertainty intervals provided for the forecast. Defaults to 0.8.

### Seasonalities
1. **`seasonality_mode`**: Either `'additive'` (default) or `'multiplicative'`.
2. **`yearly_seasonality`**: Boolean or integer. If `True`, include yearly seasonality (default). If `False`, no yearly seasonality. If an integer, specify the Fourier order.
3. **`weekly_seasonality`**: Boolean or integer. Similar to `yearly_seasonality`, but for weekly data.
4. **`daily_seasonality`**: Boolean or integer. Similar to `yearly_seasonality`, but for daily data.
5. **`seasonality_prior_scale`**: Parameter controlling the strength of the seasonality model.

### Holidays and Events
1. **`holidays`**: DataFrame with columns `holiday` (name of the holiday), `ds` (date of the holiday), and optionally `lower_window` and `upper_window` for adding days around the date as holiday effect.
2. **`holidays_prior_scale`**: Parameter controlling the strength of the holiday components.

### Additional Regressors
1. **`add_regressor(name, prior_scale, standardize)`**: Adds an additional regressor to the model.
2. **`add_seasonality(name, period, fourier_order, prior_scale)`**: Adds a custom seasonal component.

### Training Parameters
1. **`stan_backend`**: Specifies the backend to use for fitting the model. Options include `'cmdstanpy'` and `'pystan'`.

### Others
1. **`uncertainty_samples`**: Number of simulated draws used to estimate uncertainty intervals.

These hyperparameters allow you to control various aspects of the Prophet model, including the trend, seasonality, holidays, and additional regressors, providing flexibility for different types of time series data.