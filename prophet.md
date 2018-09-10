## Prophet

### Full Example
* import the module


    import matplotlib.pyplot as plt
    import pandas as pd
    import numpy as np
    from datetime import datetime, timedelta
    from fbprophet import Prophet
    from fbprophet.diagnostics import cross_validation, performance_metrics
    from fbprophet.plot import plot_cross_validation_metric

* create the data


    date_today = datetime(2018, 1, 1)
    days = pd.date_range(date_today, date_today + timedelta(89), freq='D')
    np.random.seed(seed=11)
    data = np.random.randint(1, high=100, size=len(days))
    df = pd.DataFrame({'ds': days, 'y': data})

* create the model and train


    m = Prophet()
    m.fit(df)

* predict future value 
    
    
    periods = 7
    future = m.make_future_dataframe(periods=periods, include_history=True)        
    df_pred = m.predict(future)

### Specify holiday effects
    
    
    valentines_day = pd.DataFrame({
        'holiday': 'valentines_day',
        'ds': pd.to_datetime(['2018-02-14']),
        'lower_window': -1, 'upper_window': 0, })
    spring_festivals = pd.DataFrame({
        'holiday': 'spring_festival',
        'ds': pd.to_datetime(['2018-02-15']),
        'lower_window': 0, 'upper_window': 6, })
    holidays = pd.concat((valentines_day, spring_festivals))
    m = Prophet(holidays=holidays)
    
### Add custom seasonality
    
    m.add_seasonality(name='monthly', period=30.5, fourier_order=5)
    
### Cross validation
* do cross validation


    df_cv = cross_validation(m, initial='59 days', horizon='7 days',
                             period='14 days')
* calculate performance metrics


    df_p = performance_metrics(df_cv)
