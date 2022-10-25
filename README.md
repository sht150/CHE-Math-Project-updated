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

The data obtained is for a narrow range of factors and is clustered. A single line cannot effectively capture this these trends due to high non-linearity and uneven distribution. Thus, for all analyses, the data was dicretized into two groups based on the median of factors to study the relative effect of factors on Covid-19 cases as high or low.


The Percentage of population of children is divided into two group based on higher or lower than 18%
The Diversity Index is divided into two groups based on higher or lower than 25%

#### Statictical tests
1. Performing a U-test with null hypothesis that counties with the population of children (age < 18 years) less than 18 % had lower percent of Covid-19 cases during the holiday season of 2020 results in a p-value of almost zero. This suggests that the null hypothesis is invalid and the counties with a population of more than 18 % of children had higher percentage of Covid-19 cases during the holiday season in 2020 than the counties with a population of children being less than 18 % in the New England region. 

```
stats.mannwhitneyu(data_less18["% Population with Covid 19 cases"], data_more18["% Population with Covid 19 cases"], alternative = 'less')
MannwhitneyuResult(statistic=345.0, pvalue=0.007922793114228993
```
