Things to change / correctly have
- Change `df[name] = ((df[name] - props['mu']) / props['std'])` from forecaster.py in prophet package to `df[name] = ((df[name]) / props['std'])`
- Correct the numpy.float thing in prophet package as well.
- hyperopt in regressors AND extra seasonalities.