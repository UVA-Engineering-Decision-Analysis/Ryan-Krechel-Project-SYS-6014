# SYS 6014 PROJECT - RYAN KRECHEL - FEB 18, 2020

### INTRODUCTION

For this project, I intend to create a model for seasonal investing to find a way to beat a buy-and-hold investment strategy. In theory, there are certain market trends pertaining to certain days of the year. For instance, the beginning of December tends to be a time when investors sell off stocks to cover the cost of taxes. This mass tendency to sell generally causes a decrease in the stock market. If an investor is aware of this trend, he or she should choose to invest in less aggressive accounts (perhaps bonds). My goal is to find other trends based on historical data and find a strategy for trading on a day to day basis within a calendar year to maximize returns.

Success is defined as beating buy-and-hold. If the strategy output by the decision making tool has a return greater than any of the individual funds alone, then a better investing strategy has been found.

I have chosen seven Vanguard funds to analyze. Each represents a different level of risk and different sector of the market.  
   1. VTI - Large Cap Blend, Stock Market ETF  
   2. VXF - Mid Cap Blend, Extended Market ETF  
   3. VBK - Small Cap, Small-Cap Growth ETF  
   4. VEA - International, FTSE Developed Markets ETF  
   5. VWO - Emerging Markets, FTSE Emerging Markets ETF  
   6. VPU - Utilities, Utilities ETF  
   7. BLV - Bond, Long-Term Investment Bond

Data will be collected from 2008 to 2019. This is a common timeframe that all of these ETFs share. This will allow the performance of each ETF to be compared to each other fairly.

### ACTION SET

_The decision-maker's action set A : A complete itemization of all the options available to the decision-maker, from which the decision-maker selects a unique choice._

There are 8 decisions in this model:  
   1. Invest in VTI  
   2. Invest in VXF
   3. Invest in VBK  
   4. Invest in VEA  
   5. Invest in VWO  
   6. Invest in VPU
   7. Invest in BLV
   8. Do Not Invest

### STATE SPACE

_The state space or sample space X : The space from which observation data are drawn. _

Data will be collected using Yahoo's share price history tool from 2008-2019. Preprocessing will be done on the "open" and "close" prices to convert the share prices into daily losses or gains. This will be produced and uploaded into Matlab code with the corresponding dates to use in the analysis.

### DATA GENERATING PROCESS

_Some description of the data generating process. This might take the form of a statistical model describing the statistical properties of random variables X1,X2,…,XN∈X. For example, you might posit that each observed data points x1,…,xN∈X are the realization of a independent, identically distributed (i.i.d.) normal random variables X1,…,XN, each with mean θ and variance σ2 : Xn N(θ,σ2). Here, θ and σ2 are unobserved parameters: we don't observe them directly, but the sampling process provides us with data that is useful to refine our beliefs about their values._

Once the raw data is uploaded into Matlab, it will need to be sorted by date and by gain/loss. The code will be written to assess January 2nd as a specific decision node with historical data from all other January 2nd data points. Within this day's worth of data, there will be a set of positive gains and a set of negative losses. In this way, I will be able to track success of each historical success of each ETF for any given day, both in likelihood of positive return and average value of positive/negative return. The code will repeat this process for each calendar day to develop a "strategy" for the year.

### PARAMETER SPACE

_The parameter space Θ : the set of possible values for the unobserved parameters.
For the example above, in which the data are generated as a set of i.i.d. normal random variables, the mean θ might be any real number, while the variance σ2 might be any non-negative real number: θ∈R and σ2≥0. The parameter space is then the set of all possible values of θ and σ2 : Θ=R×[0,∞)._

I began to describe this above. By breaking each day into positive and negative returns, I will be able to track the percentage of positive days for each ETF on any given calendar day.

Ideally, I will be able to identify an ETF for each day that has more than a 50% chance of providing a positive return.

### PRIOR BELIEFS

_A description of the decision-maker's prior beliefs. These beliefs describe the information or beliefs the decision-maker has about the values of the unobserved parameters before collecting data. These beliefs can generally be represented as a probability distribution over the parameter space Θ. In the case in which data are normally distributed, it might be that, based on previous experience, the decision-maker has a strong belief that the mean parameter θ is greater than 4, and less than 6. She feels, though, that she has no basis for seeing any of the values between 4 and 6 as being more likely than any other. In this situation, she might represent her prior beliefs about θ by treating θ as a random variable drawn from a uniform distribution over the intervel [4,6] : θ U[4,6]._

It is a commonly known fact that the stock market tends to average an 8% return. However, this is an average for the year, and I as the decision maker do not know much about any particular day. For the sake of simplicity, I will assume no prior beliefs and take the percentage of a particular investment returning a positive gain as 50%. 

However, I have many years of data available to me which I will apply to my ignorant prior beliefs to build a more reliable model.

### IMPROVING THE MODEL

_A description of the process for getting better information, to sharpen the decision-maker's beliefs about uncertain parameter values. Bayesian analysis provides a rigorous procedure for combining prior information with sample data to generate updated beliefs. These beliefs are represented by the decision-maker's posterior distribution over the unobserved parameter values._

Every year adds new data to the model, albeit very slowly. However, I will assess the performance of my model's ability to accurately improve investments by taking smaller samples of data. For instance, I will write the code to have the ability to only use data from 2008-2017. In this way, I can allow the model to make a decision about 2018, and use the extra data I already have to prove the validity of the model. I also will have the ability to use January to April of 2020 as a secondary test.

### PAYOFFS

_The relevant payoffs that could result from the action. Payoffs will be a function of the selected action a, and the realized value of an uncertain random variable. In many applications, it makes sense to model payoffs as a function of the action a and the value of unobserved parameter(s) θ. In other applications, it may make sense to model payoffs as a function of the chosen action and a future value of a random state variable X. In a typical application, one action might best under some values of the uncertain parameter value, while others are better for other values. In such applications, the uncertainty genuinely matters. This situation creates incentives for getting better information, to reduce the decision-maker's uncertainty, in order to guide choices reliably towards actions that generate higher payoffs. When payoffs are uncertain as a function of the selected action a, it can be helpful to think of each action as associated with a lottery over a set of possible payoffs._

The payoffs will change based on the data set being observed and will be calculated directly using the historical data. For instance, in a situation where data from 2008 to 2019 is used, up to 12 different data points will exist for each calendar day (depending on where weekends fall because weekends are non-trading days with no data). For each calendar day, the data points will be separated by positive, negative, and net-zero return. The positive days will be averaged to find the positive payoff, and the negative days will be averaged to find the negative payoff.



### UTILITY FUNCTION

_The decision-maker's utility function or loss function._

Here is a sample utility function for choosing to invest in VTI on Feb 2:  
$$EU(VTI_Feb2)=(AvgPosReturn_Feb2) \cdot (PercPosReturn_Feb2) + (AvgNegReturn_Feb2) \cdot (PercNegReturn_Feb2)$$

Here is an example from data collected from 2008 to 2019 for January 2, the first trading day of the year.

| Decision        | Avg Pos Return | Percent Pos Return |Avg Neg Return | Percent Neg Return | Estimated Utility |
| :-------------: |:-------------:| :-----:             |:-------------:| :-----:| :-----:|
| Invest in VTI   | 1.32          |67                |-0.62          |33   | 0.6752 |
| Invest in VXF   | 0.95          |67               |-0.63          |33   | 0.4215 |
| Invest in VBK   | 1.37          |50                |-0.64          |50   | 0.3652 |
| Invest in VEA   | 0.87          |50               |-0.64          |33   | 0.2235 |
| Invest in VWO   | 1.48          |67               |-1.49          |33   | 0.4875 |
| Invest in VPU   | 0.92          |50               |-1.18          |50   | -0.1283 |
| Invest in BLV   | 0.31          |67               |-1.52          |33   | -0.2965 |

It is important to note that the chance of VTI returning positive and the chance of VTI returning negative will no necessarily add up to 1. There is a chance of VTI returning 0 return, and I will be sure to include this if it shows up in the data.

### DECISION MAKING RULE

_The rule the decision-maker will use to choose a preferred action a∗ from the menu A of possible actions._

The model will find the utility function for each particular action and pick the action with the highest utility for each day of the year.

### NOTES
