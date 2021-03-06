# data-512-a4
*README file for 512hw4 (explanation & reflection included)*
---

### Introduction <br>
The goal of this assignment is to explore the Covid-19 datasets and try to answer the following question.
- How did masking policies change the progression of confirmed COVID-19 cases from February 1, 2020 through October 15, 2021?
I was assigned the Maricopa County in Arizona

### Data Source and Information <br>
There are three initial data files downloaded in csv format:<br>
- The New York Times mask compliance survey data. (https://github.com/nytimes/covid-19-data/tree/master/mask-use)
  - This dataset is not used to create the visualization!
- The RAW_us_confirmed_cases.csv file from the Kaggle repository of John Hopkins University COVID-19 data.(https://www.kaggle.com/antgoldbloom/covid19-data-from-john-hopkins-university?select=RAW_us_confirmed_cases.csv)
  - Three columns in this data are used in this project
    - 'FIPS' - the FIPS code 
    - All the date columns recording the raw confirmed cases are used
- The CDC dataset of masking mandates by county. (https://www.google.com/url?q=https://data.cdc.gov/Policy-Surveillance/U-S-State-and-Territorial-Public-Mask-Mandates-Fro/62d6-pm5i&sa=D&source=docs&ust=1636073389074000&usg=AOvVaw2UizNDNMnoGaGs9Qj9TgO0)
  - Three columns in this data are used in this project
    - 'Date'
    - 'Order Code' - unclear waht it means
    - 'FIPS' - the FIPS code 
    - 'Face_Masks_Required_in_Public' - whether face mask is mandated

### Explanation of Visualization <br>
What does the figure show? 
- This figures shows the daily new Covid-19 cases in Maricopa county, Arizona from 2020/02/01 to 2021/10/15
How does the viewer “read” the figure? 
- The line represents the daily new Covid-19 cases (represents rate of change in confirmed cases).
- The color cues represent the mask mandate situation. However in the current dataset that we have, all of the fask mask mandate for Arizona is 'NAN', there is only 'order_code=2' present in the data. I looked it up and found that Arizona never had a mask mandate! Therefore there is only one legend 'no mask mandate' in this graph.
What are the axes, and what do they represent?
- The X axis represents the date and the Y axis represent the number of daily new Covid-19 cases.
What is the underlying data and how was it processed?
- The initial data files were introduced above. The following are some processing steps.
  - I didn't use the 'mask-use-by-county' data in this particular assignment. So there weren't any processing steps for this one.
  - For the mask mandate dataset, I combined the State FIPS and County FIPS to the standard 5-digit FIPS so that I would be able to subset and merge in the future. I also dropped some unnecessary columns. Finally, I changed the date column datatype to the standard pandas datetime.
  - For the Raw US confirmed cases dataset, I firstly unpivot the columns into rows using the 'melt' function in pandas. Then I standardize the FIPS code to 5 digit and change the date column data type to datetime. Finally, I applied a 'date range mask' to filter out the data between 2020/02/01 to 2021/10/15 and calculated the daily new cases by taking the difference between number of cases.

### Analysis Results & Reflection <br>
Based on this activity, I learnt a lot from the discussions on slack. First of all, I learnt some of the useful formulas on how to reflect the COVID-19 trend. It is notable that we should use the daily new cases instead of total cases to reflect the rate of change. I also learnt 'daily infection rate' as a useful metric. However I decided not to calculate it in this assignment because the formula still is unclear. I believe it should be something like 'infected people/people at risk'. The ambiguous thing here is 'people at risk'. Do we subtract the already infected from the total population? Is it possible for a person to be infected twice? How do we take the 'risk' factor into accountability? I wish we had more data and explanation. <br>
In addition, my graph here is not very indicative of 'how mask mandate changed COVID situation' since Arizona state NEVER had a mask mandate! After discovering this, I thought about comparing the Maricopa county with counties with similar population. (As someone orignally pointed out on Slack) However, people also pointed out that different state has different statistical methods? And there are other factors that we need to count as well. Thus if I were to answer how the mask policy affected Maricopa county, I have no valid answer due to this problem. Maybe with the help of other datasets I would be able to answer this one. (Also notable that the NYT dataset had no entry on Maricopa as well!)

