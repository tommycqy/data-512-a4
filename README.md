# data-512-a4
*README file for 512hw4 (explanation & reflection included)*
---

### Introduction <br>
The goal of this assignment is to explore the Covid-19 datasets and try to answer the following question.
- How did masking policies change the progression of confirmed COVID-19 cases from February 1, 2020 through October 15, 2021?
I was assigned the Maricopa County in Arizona

### Data Source and Information <br>
There are three initial data files downloaded in csv format:<br>
- The Wikipedia politicians by country dataset called 'page_data.csv'. (https://figshare.com/articles/dataset/Untitled_Item/5513449)
  - Three columns in this data are used in this project
    - 'page' - the article name
    - 'country' - the politician's country
    - 'rev_id' - the revision id for the wikipedia page
- The population data is available in CSV format as 'WPDS_2020_data.csv'. (https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit)
  - Three columns in this data are used in this project
    - 'Name' - country or region name
    - 'Type' - includes three fields (world, sub_region or country) that represent the type of the name column
    - 'Population' - the population for the world, country or region
- The population data is available in CSV format as 'WPDS_2020_data.csv'. (https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit)
  - Three columns in this data are used in this project
    - 'Name' - country or region name
    - 'Type' - includes three fields (world, sub_region or country) that represent the type of the name column
    - 'Population' - the population for the world, country or region

There are also two additional data files generated through this assignment:<br>
- 'wp_wpds_countries-no_match.csv'
  - When merging the wikipedia politicians by country dataset and the population data, the population data sometimes doesn't have an entry for the correspondnig wikipedia page (or vice versa).
  - Some entries in the population data doesn't correspond to countries, but subregions or the whole world.
- 'wp_wpds_politicians_by_country.csv'
  - The result of successfully merged dataset.
  - There are five columns in this dataset
    - 'article_name' - the article name
    - 'country' - the politician's country
    - 'revision_id' - the revision id for the wikipedia page (same as the rev_id in the initial data file)
    - 'article_quality_est.' - the prediction score (if available) gathered by using the ORES machine learning system
    - 'population' - population of the country

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
For this relection, I firstly want to talk about some of the practices I learnt on improving reproducibility. We had an in-class activity discussing the reproducibility of data science proejects, and our group was able to find many potential improvements. I attempted to install some of these improvements during this assignment. For example, I included the complete data files and their sources, keeped all the necessary comments along the way, and wrote an in-detail README file. I was surprised to find that this level of documentation actually helped me check my own work and made me work more efficient. One additional thing I noticed during this project is that the variable names should be appropiate. For instance, there are a lot of intermediate dataframes during the analysis (by_country and by_region). It's so easy to lose track of what you're working on or make mistakes if you don't name the variables carefully. <br>
Now I want to discuss the results and the biases. Since we're using the data of English wikipedia for this project, I expected the score predictions for English-speaking countries/regions are higher than non-English-speaking countries/regions, thus resulting in a higher percentage of 'FA' or 'GA' quality articles. After seeing the results, however, I was shocked that north korea, saudi arabia and romania are ranked the top 3 countries with the highest percentage of high-quality articles. It is probably due to the fact that there are very few politician articles in those countries and these articles happen to be high-quality. In addition, I found that the article proportion (article count/population*100) is not a good metric for politician coverage since countries with large populations like india and china would be ranked among the bottom natrually. Those bottom ten countries are also non-English speaking countries as well. <br>
This suggests that when using English wikipedia as a data source, we need to recognize the exsiting bias and adjust for it. For instance, if we want to evaluate the politician coverage on wikipedia, we should include other language source as well and take the population factor into consideration.

