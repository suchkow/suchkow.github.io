---
title: Statistical Thinking in Python
layout: post
---
## Graphical EDA

- EDA – Exploratory Data Analysis

> [! info] Python Libraries in Use
> matplotlib.pyplot as plt
> seaborn as sns
> numpy as np

**Most Common Plots:**
- Histogram
- Bee Swarm Plot
- Box Plot
- Scatter Plot

#### Bee-Swarm Plot
```python
# Create bee swarm plot with Seaborn's default settings
_ = sns.swarmplot(x='species', y='petal length (cm)', data=df)

# Label the axes
_ = plt.xlabel('species')
_ = plt.ylabel('petal length (cm)')

plt.show() # Show the plot
```

###### Box Plot
```python
_ = sns.boxplot(x='east-west', y='dem_share', data=df_all_states)
_ = plt.xlabel('region')
_ = plt.ylabel('percent of vote for Obama')
plt.show()
```

![[box-plot.png|center|380]]

- **IQR** – interquartile range, which is from lower quartile (Q1, 25th perc.) to upper quartile (Q3, 75th perc.)

###### Scatter Plot
```Python
# Make a scatter plot
_ = plt.plot(versicolor_petal_length, versicolor_petal_width, marker='.', linestyle='none')

# Label the axes
_ = plt.xlabel('versicolor petal length')
_ = plt.ylabel('versicolor petal width')

# Show the result
plt.show()
```

###### ECD Function

- **ECDF** – Empirical Cumulative Distribution Function

```Python
def ecdf(data):
	"""Compute ECDF for a one-dimensional array of measurements."""
	n = len(data) # Number of data points
	x = np.sort(data) # x-data for the ECDF
	y = np.arange(1, n+1) / n # y-data for the ECDF
return x, y
```

**Plotting multiple ECDFs:**
```Python
# Compute ECDFs
x_set, y_set = ecdf(setosa_petal_length)
x_vers, y_vers = ecdf(versicolor_petal_length)
x_virg, y_virg = ecdf(virginica_petal_length)

# Plot all ECDFs on the same plot
_ = plt.plot(x_set, y_set, marker='.', linestyle='none')
_ = plt.plot(x_vers, y_vers, marker='.', linestyle='none')
_ = plt.plot(x_virg, y_virg, marker='.', linestyle='none')

# Annotate the plot
plt.legend(('setosa', 'versicolor', 'virginica'), loc='lower right')
_ = plt.xlabel('petal length (cm)')
_ = plt.ylabel('ECDF')

# Display the plot
plt.show()
```


#### Quantitative EDA

> [! info ] Python Libraries in Use
> numpy as np
> scipy.stats as st

- Outliers – data points, whose values are most far from the most of others.

###### Mean, Median & Mode
```python
mean = np.mean(versicolor_petal_length)
median = np.median(versicolor_petal_length)
mode = st.mode(versicolor_petal_length)
```

###### Percentiles
```python
np.percentile(df, [25, 50, 75])
```

###### Variance & St. Deviation
```python
differences = versicolor_petal_length - np.mean(versicolor_petal_length)
diff_sq = differences**2 # squared the diff
variance_explicit = np.mean(diff_sq)

variance_np = np.var(versicolor_petal_length)

print(variance_explicit, variance_np)
```

```python
variance = np.var(versicolor_petal_length)

print(np.sqrt(variance))
print(np.std(versicolor_petal_length))
```

###### Covariance
```python
# Compute the covariance matrix: covariance_matrix
covariance_matrix = np.cov(versicolor_petal_length, versicolor_petal_width)
print(covariance_matrix)

# Extract covariance of length and width of petals: petal_cov
petal_cov = covariance_matrix[0][1]
print(petal_cov)
```

###### Pearson Correlation Coefficient
```python
def pearson_r(x, y):
	"""Compute Pearson correlation coefficient between two arrays."""
	
	# Compute correlation matrix: corr_mat
	corr_mat = np.corrcoef(x, y)
	return corr_mat[0,1]

# Compute Pearson correlation coefficient for I. versicolor: r
r = pearson_r(versicolor_petal_length, versicolor_petal_width)
print(r)
```

#### Thinking Probabilistically – Discrete Variables

> [! info ] Python Libraries in Use
> numpy as np
> numpy.random
> matplotlib.pyplot as plt
> custom ECD Function from [[stat-thinking-py#Graphical EDA#ECD Function]]

###### Pseudo RNG

- **RNG** – Random Number Generator 
Pseudo generator, because exact seed gives exact "random" number. 

```python
seed = 2
rng = np.random.default_rng(seed) # pseudo random generator
print(rng) # rng-object

random_numbers = rng.random(size=4) # amount of random-generated numbers
```

```python
# Instantiate and seed the random number generator
rng = np.random.default_rng(42)

# Initialize random_numbers array
random_numbers = np.empty(100000)

# Generate random numbers by looping over range(100000)
for i in range(100000):
    random_numbers[i] = rng.random(size=1)
    
# Plot a histogram
_ = plt.hist(random_numbers)
plt.show()
```

###### Bernoulli Trials
```python
# Instantiate and seed random number generator
rng = np.random.default_rng(42)


# Initialize the number of defaults
n_defaults = np.empty(1000)

# Compute the number of defaults
for i in range(1000):
    n_defaults[i] = perform_bernoulli_trials(100, 0.05)

# Plot the histogram with default number of bins; label your axes
_ = plt.hist(n_defaults, bins=50, density=True)
_ = plt.xlabel('number of defaults out of 100 loans')
_ = plt.ylabel('probability')
plt.show()
```

![[bernoulli-stat-thinking.png|center|350]]

###### Exercise: Will the bank fail?

> Plot the number of defaults you got from the previous exercise, in your namespace as `n_defaults`, as a CDF. The `ecdf()` function you wrote in the first chapter is available. 
> 
> If interest rates are such that the bank will lose money if 10 or more of its loans are defaulted upon, what is the probability that the bank will lose money?

```python
# Compute ECDF
x, y = ecdf(n_defaults)

# Plot the ECDF with labeled axes
_ = plt.plot(x, y, marker='.', linestyle='none')
_ = plt.xlabel('x')
_ = plt.ylabel('y')
plt.show()

# Compute the number of 100-loan simulations with 10 or more defaults
n_lose_money = np.sum(n_defaults >= 10)
print('Probability of losing money =', n_lose_money / len(n_defaults))
```
 
###### Binomial Distribution, PMF & CDF

```python
num_of_bernoulli_trials = 60
probability_of_success = 0.1
sample_size = 10000

rng.binomial(num_of_bernoulli_trials, probability_of_success, size=sample_size)
```

**Binomial CDF Plot**
```python
# Take 10,000 samples out of the binomial distribution
n_defaults = rng.binomial(100,0.05,size=10000)

# Compute CDF
x,y = ecdf(n_defaults)

# Plot the CDF with axis labels
_ = plt.plot(x,y,marker='.',linestyle='none')
plt.margins(0.02)
_ = plt.xlabel('# of successes')
_ = plt.ylabel('cdf')

plt.show()
```

![[bin-dist-cdf.png|center|350]]

###### Poisson Processes

```python
# Draw 10,000 samples out of Poisson distribution: samples_poisson
samples_poisson = rng.poisson(10, 10000)

# Print the mean and standard deviation
print('Poisson: ', np.mean(samples_poisson), np.std(samples_poisson))

# Specify values of n and p to consider for Binomial: n, p
n = [20, 100, 1000]
p = [0.5, 0.1, 0.01]

# Draw 10,000 samples for each n,p pair: samples_binomial
for i in range(3):
	samples_binomial = rng.binomial(n[i], p[i], size=10000)
	
	# Print results
	print('n =', n[i], 'Binom:', np.mean(samples_binomial), np.std(samples_binomial))
```