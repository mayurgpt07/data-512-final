

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
- What are the differences between *dynamic* and *static* pricing households of similar demographics
  - I hypothesize that dynamic users with low tariffs will still act similar to their static counterparts, while high tariff users will act differently than their static counterparts. More concretely, within blocks of households that share similar demographics, they will show similar timing and total usage regardless of their pricing tariff __iff__ it is low tariff dynamic pricing rather than avg or high dynamic tariff pricing
- Can we create a model that can compute the next time steps worth of energy consumption? For example, knowing they utilized .5 kw/hr at 10am, what will they consume at 10:30am? Then continuing this iterative process, can we accurately model the energy over time?
  - In particular, can we do this only with the signal itself, and not the demographic information provided?
### Reach
- Can we create a model that predicts the next time steps worth of energy (similar to the basics pt2), but also utilize demographic information to create a more accurate model
## Methodology
- To address our first question, I plan on doing some basic visualizations to determine timing patterns similarities. For example, a scatter plot of avg consumption per thirty minutes over an average day of low tariff dynamic pricing. We can then compare this graphic to a similar group but with static pricing. Using boxplots, we can get an idea of how much variation aligns in these measures and see if they do or do not overlap with boxplots from our counterpart. I believe this to be a good first step as we would otherwise have to do a t-test for every 30 minute interval of the day, which would mean a total of 24 x 2=48 t-tests. Visualizing all these tests at once will be tricky. Using this scatterplot technique, I can easily visualize these results.
  - To get a more concrete result, I will use ANOVA over all groups to determine the statistical significance of these differences
    - I do want to note, that by doing so, I am worried that 30 minute intervals during periods of low activity amongst *all* groups will show no difference, and thus reduce the likelihood of finding significance. I am tempted to weight the relative importance of the difference by the volume of energy used.
- To address our second question, I plan on using SINDy, or Sparse Identification of Non-linear Dyanmics.
  - This method works by doing linear combinations of random mutations of all the signals we have and using *L1* loss functions to choose a sparse representation of our model. It has been used many times in various communities, including chemistry and physics (see references below).
  - To describe it in more detail, SINDy is basically setting up our equation as $Ax=b$, where A is all energy usage at 30 minute intervals up to the *n-1* point, and b is the same except from point 2 up to *n*. Our x acts as our mutation matrix, that may do some linear combination of our A, such as *2A+A^2 - 3log(A) + ....* Using the *L1* loss function, we can reduce this to just the most important factors of our transformation and create an easily understood equation for our system.  
  - The reason why this is a good method for solving our problem is that it can provide an easily interpretable equation that drives electric usage amongst various users in our population. Furthermore, it will not require and information on the consumer themselves.
  - One caveat is that it may not preform all too well, and that providing some information on the consumers, or fitting a model per type of consumer, might do much better. Only time will tell
- To address our reach goal, there are many tools at our disposal. Several papers have tackled demand prediction using deep neural networks along with various other tools. I will likely take a more simplistic approach, and attempt to fit a type of regression. Considering this is a reach goal I do not mind being vague on what methods to use for it.
### References
- J. Chem. (2019). Reactive SINDy: Discovering governing reactions from concentration data. AIP The journal of chemical physics. https://aip.scitation.org/doi/10.1063/1.5066099
- Mangan, N. M., Askham, T., Brunton, S. L., Kutz, J. N., & Proctor, J. L. (2019). Model selection for hybrid dynamical systems via sparse regression. Proceedings. Mathematical, physical, and engineering sciences, 475(2223), 20180534. doi:10.1098/rspa.2018.0534
