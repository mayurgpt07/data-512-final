

## Title: Energy and demographics, how do we use it?
## Data: https://www.kaggle.com/mirichoi0218/insurance
## Description
Smart meter readings from the United Kingdom over a three year period (2011 to 2014) at half hour intervals. What this means is that from ~5500 households we have total energy draw / usage at 30 minute intervals. They were "recruited as a balanced sample representative of the Greater London population". There are two types of groups, those under dynamic time of use pricing and others under static pricing. The main objective of this data collection process to understand how users of various demographics respond to dynamic pricing compared to static pricing. "The signals given were designed to be representative of the types of signal that may be used in the future to manage both high renewable generation ... and also test the potential to use high price signals to reduce stress on local distribution grids during periods of stress"
## Motivation / Problem Statement
In light of the current situation, I realized that there exists a knowledge gap in insurance policies and services, therefore I wanted to understand more about how individuals are billed for their medical insurances. Putting myself in the position of a customer, I thought that I'll only be aware of my personal details amd won't have any visibility to the internal parameters of the insurance companies. Hence, with the basic details can I figure out the reasons for my bill? or how much bill I can get in future?  

## Terms of use
Republishing is not prohibited by kaggle
#### License: Database: Open Database, Contents: Database Contents

## Unknowns and dependencies
- Although in the real world these features are not enough to adequately describe the health insurance bills, we can start with these limited columns and then gradually improve our analysis as we get new data
- The data is a small random subset of the whole population and inferences from this data cannot be generalized to the whole population

## Background
The following bullets highlights related and previous work done in the past and general observations on the type of work done
- https://data.london.gov.uk/blog/electricity-consumption-in-a-sample-of-london-households/
  - This comes from the same people who published the data set. They ran simple analyses using tableau on energy consumption over time of the various types of dynamic pricing algorithms. Mainly, the difference between high, avg, and low rates.
- https://www.researchgate.net/profile/James_Schofield6/publication/293176172_Low_Carbon_London_project_Data_from_the_dynamic_time-of-use_electricity_pricing_trial_2013/links/56b6889d08ae5ad36059b61c.pdf
  - This is the official publication of the dataset which describes the fields of data, along with specifics of the data collection process, bias, anonymity, and more
- https://ieeexplore.ieee.org/abstract/document/8322199
  - This article focuses on the many different data sets that have been used in the smart meter field, and the challenges within them, including visualization.
  - According to this article, as of march 2018, there were only two refernces to this data!
  - As of 2019, this has gone to 13 references.
    - 7 in 2019 alone! Clearly this is an exploding data source of interest, smart meters are on the rise!
      - I think this may be off by one as according to google scholar, [this paper](https://www.sciencedirect.com/science/article/pii/S1050173818301117), which discusses a heart disease, supposedly references this data set.
__Summary of background__
There seems to be an increasing rate of exploration and usage of this dataset among others in the smart meter field. The work so far on this dataset on its own is minimal. Most research questions referencing this dataset are exploring multiple at once, often interested in creating probabilistic models for peak load times and volumes. This ties nicely into my research questions
## Research Questions
### Basics
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
## Methodology
### References
- J. Chem. (2019). Reactive SINDy: Discovering governing reactions from concentration data. AIP The journal of chemical physics. https://aip.scitation.org/doi/10.1063/1.5066099
- Mangan, N. M., Askham, T., Brunton, S. L., Kutz, J. N., & Proctor, J. L. (2019). Model selection for hybrid dynamical systems via sparse regression. Proceedings. Mathematical, physical, and engineering sciences, 475(2223), 20180534. doi:10.1098/rspa.2018.0534
