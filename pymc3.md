## PyMC3

### Full Example

###### Import the module
    import matplotlib.pyplot as plt
    import pymc3 as pm

###### Create the data
    size = 200
    true_intercept = 1
    true_slope = 2
    x = np.linspace(0, 1, size)
    y = true_slope * x + true_intercept + np.random.normal(scale=0.5, size=size)

###### Define the model and sample
    with pm.Model() as model:
        sigma = pm.HalfCauchy('sigma', beta=10, testval=1.)
        intercept = pm.Normal('intercept', 0, 20)
        slope = pm.Normal('slope', 0, 20)
        likehood = pm.Normal('y', mu=slope * x + intercept, sd=sigma, observed=y)
        trace = pm.sample(3000, cores=2)            

###### Check the summary statistics
    pm.summary(trace)

###### Plot samples histograms and values
    pm.traceplot(trace)
    
###### Plot the autocorrelation function
    pm.autocorrplot(trace)
    
    plt.show()
    
### Inference

#### Step methods
    step = Metropolis()
    pm.sample(3000, step=step, cores=2)   

#### Variational
    approx = pm.fit(100000, callbacks=[pm.callbacks.CheckParametersConvergence(tolerance=1e-4)])