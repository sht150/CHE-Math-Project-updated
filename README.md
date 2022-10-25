# ChE-Math-Project1: Covid-19 dependence on population of children and diversity index

### Influence of diversity index and population of children on Covid-19 cases in the New England region during holiday season 2020

The holiday season in 2020 was marked with confusion as the Covid-19 pandemic started escalating and one of the major decisions was to determine if the K-12 schools should conduct remote or in-person learning for the upcoming semester. In order to statistically determine the impact that re-opening schools for in-person learning could have, a study of  Influence of diversity index and population of children on Covid-19 cases in the New England region during holiday season 2020 would be helpful. Thus, the following problem was formulated.


#### Using Regression tools ( U test and Linear regression with interaction) to analyze county-wise data and answer the following questions:
1. Did counties with population of children higher than 18% have lower percentage of Covid-19 cases during the holiday season of the year 2020?

2. Did counties with diversity index higher than 25% have higher percentage of Covid-19 cases during the holiday season of the year 2020?

3. Were Covid-19 cases higher in counties with more than 18% population of children and diversity index greater than 25%?

#### Raw data collection and analysis of their dependence
The raw data for Covid-19 cases was collected from New York Times. The data for percentage of population of children and diversity index was obtained from census.gov website. 2020 censis data was used. Scatter plots as shown below were plotted to qualitatively determine the dependence of the factors.


![Figure_6](https://github.com/sht150/CHE-Math-Project-updated/blob/main/Figure%206.png)
![Figure_7](https://github.com/sht150/CHE-Math-Project-updated/blob/main/Figure%207.png)

The data obtained is for a narrow range of factors and is clustered. A single line cannot effectively capture this these trends due to high non-linearity and uneven distribution. Thus, for all analyses, the data was discretized into two groups based on the median of factors to study the relative effect of factors on Covid-19 cases as high or low.


The Percentage of population of children is divided into two group based on higher or lower than 18%
The Diversity Index is divided into two groups based on higher or lower than 25%

#### Statictical tests
1. Performing a U-test with null hypothesis that counties with the population of children (age < 18 years) less than 18 % had lower percent of Covid-19 cases during the holiday season of 2020 results in a p-value of almost zero. This suggests that the null hypothesis is invalid and the counties with a population of more than 18 % of children had higher percentage of Covid-19 cases during the holiday season in 2020 than the counties with a population of children being less than 18 % in the New England region. 

```
stats.mannwhitneyu(data_less18["% Population with Covid 19 cases"], data_more18["% Population with Covid 19 cases"], alternative = 'less')
```
MannwhitneyuResult(statistic=345.0, pvalue=0.007922793114228993)

2. Performing a U-test with null hypothesis that counties with the diversity index greater than 25 % had higher percentage of Covid-19 cases during the holiday season of 2020 results in a p value very close to unity. This suggests that the null hypothesis is valid and the counties with a diversity index of more than 25 % had higher percentage of Covid-19 cases during the holiday season in 2020 than the counties with a diversity index of less than 25 % in the New England region. 

```
stats.mannwhitneyu(data_more25["% Population with Covid 19 cases"], data_less25["% Population with Covid 19 cases"], alternative = 'greater')
```
MannwhitneyuResult(statistic=94.0, pvalue=0.9999999942675446)

3. Using linear regression to determine how diversity index and population percentage of children in the counties of the New England region during the holiday season of the year 2020 and their interaction is associated with percentage Covid-19 cases. The factors are treated as discrete variables.
Group 0 indicates population of children < 18% / Diversity Index < 25%
Group 1 indicates population of children > 18% / Diversity Index > 25%

```
cases = np.array(data["% Population with Covid 19 cases"])
group_divind = np.array(data["group_diversity"])
group_age = np.array(data["group_age"])
group_inter = np.array(group_divind * group_age)

X2 = np.c_[np.ones(len(cases)),group_divind, group_age, group_inter]

from numpy.linalg import inv
tmp2 = inv(np.matmul(np.transpose(X2),X2))

temp2 = np.matmul(tmp2, np.transpose(X2))
Intercept2, Group_Divind2, Group_Age2, Group_Inter2 = np.matmul(temp2, cases)

print("Our intercept is ",Intercept2, "and our slope for diversity index dependence is", Group_Divind2, 
      "and our slope for age dependence is", Group_Age2, "and our interaction parameter is", Group_Inter2)
```
Our intercept is  1.2374917541176456 and our slope for diversity index dependence is 0.9302407661045783 and our slope for population of children dependence is 0.16064950753452517 and our interaction parameter is 1.2679716065765838

This shows that there is a significant dependence of diversity index on Covid-19 cases and slight dependence on percentage of population of children. But the effect on Covid-19 cases due to interaction of both the factors is enhanced. The interaction plot below depicts the same.

![Figure_8_interaction_plot](https://github.com/sht150/CHE-Math-Project-updated/blob/main/Figure%208_interaction%20plot.png)

These findings indicate that there was a strong dependence of Covid-19 cases on the diversity index and interaction of diversity index and population of children in the New England region during the holiday season of 2020 as discrete variab;es. To generalize this data, further studies need to be done to incorporate more data points over a larger range. For example, this can be done by taking city-wise data instead of county-wise data. The current data is clustered and a linear regression model does not accurately capture the trends of the data. More accuarte analysis can be obtained by selecting a non-linear model or linearilzing the data before applying linear regression.
