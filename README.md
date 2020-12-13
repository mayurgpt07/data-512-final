

## Title: Medical Insurance Bills
## Aim 
Every student in the university has to select some kind of insurance as they enter into a new quarter or year. These insurances can be either the one provided by the university or from any external private health insurance company. But I noticed that most of the students are not aware of why they are paying a particular premium or whether different people have different charges?  
Therefore, the aim of the analysis is to understand the medical insurance charges from the perspective of the customer. Now a customer might not be aware of all the factors that an insurance company uses, hence the analysis includes details pertaining to the customer only. 

## Methods
We try to analyze the following questions to better understand the medical insurance charges:
* The first question is ***What are the different variables that impact the individual medical insurance cost?***. We use multiple statistical techniques like:
  - Correlation Analysis
  - Random Forest Feature Importance
  - Permutation Feature Importance Testing
  - Visualizations

* The second question is ***can we create a model that can compute the medical insurance cost of individual?***. To solve this question and build a robust model we use techniques like:
  - Linear Regression
  - Random Forest Regression
  - Polynomial Regression
  - L1-Regularized Polynomial Regression
  

## Data
The dataset is publically available at [Kaggle](https://www.kaggle.com/mirichoi0218/insurance)

### Folder Contents
```
.
├── README.md
├── LICENSE
├── data
│    └── insurance.csv
├── img
│    ├── ChargesInRegion.png
│    ├── ChargesinRegionForGenders.png
│    ├── ChargesInRegionForSmoker.png
│    ├── ChargesInRegionForChildren.png
│    ├── Correlation.png
│    ├── DistributionOfCharges.png
│    ├── LogDistributionOFCharges.png
│    ├── FeatureImportance.png
│    ├── ChargesVsBMIWithSmoker.png
│    ├── ChargesVsAgeWithSmoker.png
│    ├── ChargesVsChildrenWithSmoker.png
│    └── ModelComparison.png
└── Medical Insurance Bills - An analysis of individual cost.ipynb
```
  
## Finding

We performed multiple analysis to understand the data and derive some obervations. These analysis provided some very interesting results for different research questions
* We first discovered that being a **smoker** results more medical insurance charges. For each of the regions we saw the significant difference in the charges and the same was found when exploring **BMI** and **age**
* The other intersting observation was that **BMI** and **age** had some level of impact on charges. Although, the association was not as strong as being a **smoker** but they came out significant n feature importance chart and permutation feature testing
* Based on the mean squared error on test data, we saw that **Polynomial Regressor** works best on our data. This also indicates that their are exist some linear association between charges and higher degree transformation of features

![Model Comparison](https://github.com/mayurgpt07/data-512-final/blob/master/img/ModelComparison.png)

Apart from the observations pertaining to research questions, there were 2 other interesting findings:
* The distribution of medical insurance charges or cost is positively skewed. Therefore, in future we might need to use transformation for analysis that require normal distribution of variables
* If an individual has a large **bmi** and is a **smoker**, their medical insurance cost would be high. This is evident from the plot between **charges** and **bmi**, where for smokers the estimator line grows sharply as **bmi** increases

#### Limitations:
Although the analysis gave some great observations and insights, there are a few aspects that limits the analysis in the real world scenario:
* The analysis is done from the perspective of the customer, hence the data might reflect different factors medical insurance companies use to derive the premiums
* The data is a small random subset of the whole population and inferences from this data cannot be generalized to the whole population.

## Conclusion
It was a successful analysis, as we were able to determine answers for the research question and determine whether we could accept or reject the null hypothesis

**What are the different variables that impact the individual medical insurance cost?** <br />
- **Null Hypothesis** - *A particular feature has no relevance in the dataset (check for all features)* <br />
- **Result** - Since smoker, bmi and age have association with medical insurance cost we reject the null hypothesis

**Can we create a model that can compute the medical insurance cost of individual? What is the average error that can be expected from the new data?** <br />
- **Null Hypothesis** - *There will be no viable prediction of medical insurance cost by any combination of features* <br />
- **Result** - Since a polynomial regressor was able to fit the data with minimum test MSE, we can reject the null hypothesis

## License
Database: [Open Database, Contents: Database Contents](http://opendatacommons.org/licenses/dbcl/1.0/) <br />
Republishing is not prohibited by kaggle
