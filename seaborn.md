## Seaborn

### Documents
https://seaborn.pydata.org/

### Import the module
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import seaborn as sns
    sns.set(style="darkgrid")
    
### Load sample data
    tips = sns.load_dataset("tips")
    fmri = sns.load_dataset("fmri")
    iris = sns.load_dataset("iris")

### Draw a scatter plot
    ax = sns.relplot(x="total_bill", y="tip", hue="smoker", data=tips)
    

### Draw a line plot
    ax = sns.relplot(x="timepoint", y="signal", hue="event", kind="line", data=fmri)
    
### Plot with facets
    ax = sns.relplot(x="timepoint", y="signal", hue="subject",
            col="region", row="event", height=3,
            kind="line", estimator=None, data=fmri)
            
### Plot univariate distributions
    x = np.random.normal(size=100)
    ax = sns.distplot(x, kde=False)

### Plot bivariate distributions
    mean, cov = [0, 1], [(1, .5), (.5, 1)]
    data = np.random.multivariate_normal(mean, cov, 200)
    df = pd.DataFrame(data, columns=["x", "y"])
    
    ax = sns.jointplot(x="x", y="y", data=df)

### Plot pairwise relationships
    ax = sns.pairplot(iris)

### Set labels and title
    ax.set(xlabel='X', ylabel='Y')
    ax.set_title('Title')

### Save a plot to file
    fig = ax.get_figure()
    fig.savefig('fig.png')
    