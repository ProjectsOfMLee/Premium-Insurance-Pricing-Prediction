# Premium-Insurance-Pricing-Prediction

## Loss-Cost Model 

The essence of insurance pricing comes down to the loss-cost model. The premium cost is unique for every commercial building client. 

The equation for calculating a premium is as follows:

`Premium = Cost + Profit`

I.e. we are interested in modelling the cost, and then determining the margin of profit. We seek to have the client both pay their cost, and, contribute to our company profit. 

The cost can be separated into multiple sub-components denoted as the following:

- Expected Losses (Claims from the client) 
- Loss Adjustment Expenses 
- Underwriting Expenses 

This results in the following formula: 

`Premium = Expected Losses + Loss Adjustment Expenses + Underwriting Expenses`

These components can be broken down further, however, we are going to use the pure premium method to calculate premiums 
as written in Chapter 8 of Werner & Modlin.

$$ PurePremium = \frac{ExpectedLoss * (1 + LossAllocatedExpenses) + FixedExpensesPerPolicy}{1 - VariableExpensesPerPolicy - ProfitLoading} $$

- $ ExpectedLoss $ the amount of loss the targeted client is predicted to occur.  

- $ LossAllocatedExpenses $ are claim-related expenses that are directly attributable to a specific claim; for
example, fees associated with outside legal counsel hired to defend a claim can be directly
assigned to a specific claim.

- $ FixedExpensesPerPolicy $ day-to-day running expenses for facilitating insurance coverage overall. Commercial rent, server costs, etc. 

- $ VariableExpensesPerPolicy $, expenses which are unrelated to specific policies, and, could be specific to the annual year. E.g. Covid pandemic of 2020-2021 could result in lower insurance claims therefore having a smaller  $ VariableExpensesPerPolicy $ for that annual year. 

- $ ProfitLoading $, similar to a profit margin; you as an executive, get to determine on how much to charge your customers.

Note that you can consolidate the last two variables of interest for the pure premium into one number, ultimately these are the annual business decisions the insurance company has to make. 


## Modelling Expected Loss 

Specifically, the most important aspect of this project is to correctly model the client loss. Otherwise known as the loss/cost model. 
There are several methods to model expected losses but the most ubiquitous approach is to model the frequency and severity of claims. 

### Frequency of Claims 
The frequency of claims refers to the number of claims can occur for a particular client. We can denote this by $Y_f$. 

To model $Y_f$ we should consider distributions that model count data. Those distributions include but are not limited to

- Poisson 
- Negative Binomial 
- Binomial 
- Zero-inflated Poisson 

The most standard approach for modelling such data is through the use of GLM's which we modelled in class. 

### Severity of Claims 

The Severity of claims refers to the monetary loss of an insurance claim. We denote this by $Y_s$. 

To model $Y_s$ we should consider distributions that model continous data. 

- Gaussian (log-link)
- Gamma (log-link)
- Log-normal 
- Variance-Gamma 
- Generalized Hyperbolic 

Again if we consider a GLM framework, we can easily use the data given in the project to model such losses. 


### Loss-Cost Model 

To calculate the expected loss, use the following formula. 

$$ ExpectedLoss = Y_s * Y_f $$

Essentially this is straight forward. You take the expectation of the number of claims for a particular client, and multiply by their 
severity (the expected monetary loss). 