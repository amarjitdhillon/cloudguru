# Stat 101 concepts

## Descriptive and Inferential Statistics
### Descriptive Statistics
- It provides summary statistics of the existing data. Some examples are:
    - Mean
    - Median
    - Standard deviation
    - Co-relation

### Inferential Statistics 
- It is the concept of deriving the conclusions about population using the sample data. It can be said as an extension of the descriptive statistics.
- It is used to make the business decisions. 
- It helps us think beyond data.
- `Descriptiive Statistics` can answer questions like: who were our customers while `Infrential Statistics` can answer questions like
    - Will it snow in Ottawa at 2 am on a certain day?
    - Who can be our customers in next 2 years for a particular region? We need to calculate the likeliness for this.
    - How many customers will we gain if we gain/loose if we take some decision?
  - Generally speaking, the `Descriptive Statistics` is done on the histogram whereas the `Infrential Statistics` is done using the underlying distribution
  
## Random variable
  
  
## Discrete random variable
- the sum of all the probabilities should be one
- If all the probabilities for the variables can be listed, then we can call it as `discrete random variable` 
- The term associated with this is `probability mass function`
 
## Continuous random variable
- We cannot specify all the probabilities in this case.
- The term associated with this is `probability density function`
 
 
## Various distributions

### Bernoulli Distribution
It is associated with yes and no. It is a special case of `Binomial distribution`.
The Bernoulli distribution is a `discrete distribution` having two possible outcomes labelled by `n=0` and `n=1` in which n=1 ("success") occurs with probability p and n=0 ("failure") occurs with probability `q=1-p`, where 0<p<1. It therefore has probability density function
 
$$
P(n) = \Bigg\{  \begin{matrix}
                1-p & n=0\\
                p & n=1
                \end{matrix}
$$

Examples:
- Stock prices are going up or down?
- Item sold or not sold?

#### Bernoulli Trial
It’s an experiment where you can have one of two possible outcomes. For example, “Yes” and “No” or “Heads” and “Tails.” A few examples:

`Coin tosses`: record how many coins land heads up and how many land tails up?
`Births`: how many boys and how many girls are born each day?
`Rolling Dice`: the probability of a roll of two die resulting in a double six?
  
### Binomial Distribution
 It is associated with yes and no. A binomial distribution can be thought of as simply the probability of a SUCCESS or FAILURE outcome in an experiment or survey that is repeated multiple times. The binomial is a type of distribution that has two possible outcomes (the prefix “bi” means two, or twice). For example, a coin toss has only two possible outcomes: heads or tails and taking a test could have two possible outcomes: pass or fail.
 
 $$
 P(X=x)=\binom{n}{x} (p)^x  (1−p)^{n−x}
 $$
 
 The first variable in the binomial formula, n, stands for the number of times the experiment runs.
 The second variable, x, represents the probability of one specific outcome.
 
!!! note
    Assumptions for this distribution are:
    
        - One trial is independent of another 
        - There are 2 possible outcomes of each trial are possible
        - Probability of success is p and is same for all trials
        - Number of trials are fixed
 
 The diff between binomial and Bernoulli distribution is explained below:
 
!!! tip
    The `Bernoulli distribution` is the discrete probability distribution and has only two possible outcomes.
    The`Binomial distribution` can be said as discrete probability distribution of the number of times an event is likely to occur within a given period of time.   

### Uniform Distribution
  There is equal likeliness of events happening. 
  
### Normal Distribution
   It is associated with yes and no.  
   
## Z-score


## Hypothesis testing





   
   
## Central limit theorm



## Area under curve
The integral of $f(x)$ corresponds to the computation of the area under the graph of $f(x)$. Area between points $a$ and $b$ is given as 

$$
   A(a,b) = \int_{a}^{b} f(x) dx
$$

## variability

While the central tendency, or average, tells you where most of your points lie, variability summarizes how far apart they are. 
Low variability is ideal because it means that you can better predict information about the population based on sample data. High variability means that the values are less consistent, so it’s harder to make predictions.


### What is a test statistic?
A test statistic is a number calculated by a statistical test. It describes how far your observed data is from the null hypothesis of no relationship between variables or no difference among sample groups.

The test statistic tells you how different two or more groups are from the overall population mean, or how different a linear slope is from the slope predicted by a null hypothesis. Different test statistics are used in different statistical tests.

## Nominal and Ordinal data
Nominal data is classified without a natural order or rank, whereas ordinal data has a predetermined or natural order

What is the difference between ordinal, interval and ratio variables? Why should I care?
https://www.graphpad.com/support/faq/what-is-the-difference-between-ordinal-interval-and-ratio-variables-why-should-i-care/


---

## Histogram


### Central tendency of data?

- using Arithmetic mean


