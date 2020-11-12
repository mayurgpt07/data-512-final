

## Title: Energy and demographics, how do we use it?
## Data: https://www.kaggle.com/mirichoi0218/insurance
## Description
Medical insurance cost are the premium each individual pays for getting a medical insurance from any private or government insitute. These premium are decided on the basis of the plans and services the individual applies for. According to [eHealthInsurance](https://www.ehealthinsurance.com/resources/affordable-care-act/much-health-insurance-cost-without-subsidy), for unsubsidized customers in 2019, premiums for individual coverage averaged $462 per month and around $199 with subsidy. Therefore, an individual spends in the range of $2388 to $5988 in a year. If a person in investing such an amount of money, then it is important for them to understand the details of how things work outside of selecting a plan

## Motivation / Problem Statement
In light of the current situation, I realized that there exists a knowledge gap in the insurance policies and services, therefore I wanted to understand more about how individuals are billed for their medical insurances. Putting myself in the position of a customer, I thought that I'll only be aware of my personal details amd won't have any visibility to the internal parameters of the insurance companies. Hence, with the basic details can I figure out the reasons for my bill? or how much bill I can get in future?  

## Terms of use
Republishing is not prohibited by kaggle
#### License: Database: Open Database, Contents: Database Contents

## Unknowns and dependencies
- Although in the real world these features are not enough to adequately describe the health insurance bills, we can start with these limited columns and then gradually improve our analysis as we get new data
- The data is a small random subset of the whole population and inferences from this data cannot be generalized to the whole population

## Background
The following bullets highlights related and previous work/studies done in the past and general observations on the type of work done
- https://www.ehealthinsurance.com/resources/affordable-care-act/much-health-insurance-cost-without-subsidy
  - An article by the ehealth describing the amount spent by an individual or family yearly on medical insurance premiums
- https://www.kaggle.com/mirichoi0218/insurance/activity
  - The problems has been extensively worked on by the data science community. They have employed numerous techniques including but not limited to classfication, regression and clustering. The problem provides dual benefits as it allows people to understand the medical bills based on known entities (known by customer) and allows new data scientist to test and improve their skills
- https://people.csail.mit.edu/gjw/papers/healthcare.pdf
  - Scientist at MIT worked on identyfying health insurance cost using the claims data of about 800k individuals, with about 200k individuals as the test set (out of sample). The approach used in the paper includes multiple variables outside of the indiviuals demographics. They use classification trees and clustering to create groups that can be explained by a set of characterstics. They focus on grouping people with similar claims and with the price of claim as one of the attribute

__Summary of background__

## Research Questions
- What are the different variables that impact the individual medical insurance cost 
  - To address this question, I plan on running a correlation aand colinearity analysis on the variables. The correlation will tell us about how much each variable contributes to the cost (in a linear way). The colinearity can tell us if two variables are mutually related to each other and whether we need both of them to accurately understand the medical insurance cost. We will use the packages **pandas** and **statsmodel** to calculate the correlation and colinearity respectively
  - Another method is to use **sckit-learn** package and implement **Random Forest Regression** with the medical insurance price as the predictor variable. The random forest regressor comes with an added advantages of generating the *feature importance* matrix. 
  - The third step would be to use different visualizations to understand the relations between different features and medical insurance cost
- Can we create a model that can compute the medical insurance cost of individual? What is the average error that can be expected from the new data?
  - To address the second question, I will implement **4 differnt models** using **scikit-learn** package:
    - Linear Regression Model: The linear regression model will simply try to use all the input variables to generate the best possible model
    - Polynomial Regression Model: The polynomial regression model will add higher degree variables (Squared, cubic values of given inputs) to the linear inputs. We will then use linear regression on all the variables to get the best possible model
    - L1 Polynomial Regression Model: We will use the polynomial variables generated in the previous step and use an L1 regularized linear regression model on it. The L1 regularizer automatically filters the uneccesary variables, therefore providing models with lesser complexity
    - Random Forest Model - The random forest regressor is a non linear regression model which allows us to observe more complex relations between the input and outputs 
### References
- J. Chem. (2019). Reactive SINDy: Discovering governing reactions from concentration data. AIP The journal of chemical physics. https://aip.scitation.org/doi/10.1063/1.5066099
- Mangan, N. M., Askham, T., Brunton, S. L., Kutz, J. N., & Proctor, J. L. (2019). Model selection for hybrid dynamical systems via sparse regression. Proceedings. Mathematical, physical, and engineering sciences, 475(2223), 20180534. doi:10.1098/rspa.2018.0534
