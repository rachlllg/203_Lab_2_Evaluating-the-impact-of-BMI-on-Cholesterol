# MIDS 203 Lab 2 Dataset

## Background:
The dataset we used for Lab 2 is sourced from National Health and Nutrition Examination Survey (NHANES), 2005-2006. 

Link to the original source: https://www.icpsr.umich.edu/web/ICPSR/studies/25504/datadocumentation

The zip file in the Dataset folder contains the entire original dataset downloaded from the ICPSR Institute for Social Research, University of Michigan. Each participant is identifiable via the unique SEQN in each sub-dataset. 

## Raw:
Below listed are the sub-datasets we extracted from the complete dataset for our analysis. 

The raw sub-datasets can be found in the Dataset > Raw folder. And the user guides for each sub-dataset can be found in the Dataset > User_guides foler.


|                    Dataset                       |   Variable Name   |                 Variable Description                              |  User guide page number |
|--------------------------------------------------|-------------------|-------------------------------------------------------------------|-------------------------|
|      DS13 Examination: Body Measurements         |        SEQN       | Respondent sequence number                                        |           10/129        |
|                                                  |        BMXBMI     | Body Mass Index (kg/m**2)                                         |           15/129        |
|      DS129 Laboratory: Total Cholesterol         |        SEQN       | Respondent sequence number                                        |           8/65          |
|                                                  |        LBXTC      | Total cholesterol (mg/dL).                                        |           8/65          |
|      DS111 Laboratory: HDL Cholesterol           |        SEQN       | Respondent sequence number                                        |           10/67         |
|                                                  |        LBDHDD     | Direct HDL-Cholesterol (mg/dL)                                    |           10/67         |
|       DS110 Laboratory: Glycohemoglobin          |        SEQN       | Respondent sequence number                                        |            9/66         |
|                                                  |        LBXGH      | Glycohemoglobin (%)*                                              |            9/68         |
|       DS001 DS1 Demographics                     |        SEQN       | Respondent sequence number                                        |            8/66         |
|                                                  |        RIAGENDR   | Gender of the sample person                                       |            9/25         |
|                                                  |        RIDAGEYR   | Age in years of the sample person                                 |            10/25        |
| DS242 Questionnaire: Smoking - Cigarette Use     |        SEQN       | Respondent sequence number                                        |            10/86        |
|                                                  |        SMQ020     | Smoked at least 100 cigarettes in life                            |            10/68        |
|                                                  |        SMD641     | # of days smoke cigarette in past 30 days                         |            15/68        |
|                                                  |        SMD650     | # of cigarettes smoked/day on days that you smoked                |            16/68        |

\* Glycohemoglobin is a lab test that measures the average level of blood sugar in an individual. It is the primary test used to diagnose diabetes. 

## Clean:
A series of data cleaning were performed in data_cleaning.rmd file. Below are the cleaned dataset output from the data_cleaning.rmd file. 


|       File name          |   Variable Name        |    Variable Description                |  Variable Nature         |
|--------------------------|------------------------|----------------------------------------|--------------------------|
|         main.csv         |    TC/HDL-C   	        | Ratio of total to HDL-Cholesterol      |  Primary Y variable      |
|                          |    BMI                 | Body Mass Index (kg/m**2)              |  Primary X variable      |
|                          |    Glycohemoglobin     | Glycohemoglobin (%)                    |  Supplemental X variable |
|                          |    Age                 | Age (years)                            |  Supplemental X variable |
|                          |    Gender              | Gender (Female/Male)                   |  Supplemental X variable |

Of the 6360 respondents who had valid measurements for BMI, Cholesterol, and Glycohemoglobin, only around 20% (1248) answered they have smoked at least 100 cigarettes in life and provided responses for the frequency of cigarette smoking. We are unable to determine the smoking habit of the other 80%. 

Consider the response on frequency of smoking could be inaccurate as respondents could lie about their frequency of smoking or feel a social pressure to under-report their frequency of smoking, and the physical examination results on BMI, Cholesterol and Glycohemoglobin are factual while smoking habits is subjective, we do not believe we should narrow down our main dataset to only include the 1248 respondents who answered the smoking habit question. Therefore, we will treat the sample of 1248 respondents as a separate dataset from the main dataset of the 6360 respondents and analyze the effect of smoking on Cholesterol separately.

|       File name          |   Variable Name        |    Variable Description               |  Variable Nature         |
|--------------------------|------------------------|---------------------------------------|--------------------------|
|       smoking.csv        |    TC/HDL-C   	        | Ratio of total to HDL-Cholesterol     |  Primary Y variable      |
|                          |    BMI                 | Body Mass Index (kg/m**2)             |  Primary X variable      |
|                          |    Glycohemoglobin     | Glycohemoglobin (%)                   |  Supplemental X variable |
|                          |    Age                 | Age (years)                            |  Supplemental X variable |
|                          |    Gender              | Gender (Female/Male)                   |  Supplemental X variable |
|                          |    num_cigarettes      | # of cigarettes in a year             |  Supplemental X variable |


Each output file is split to explore (30% of the output file) and confirm (70% of the output file). All data analysis are performed on explore dataset while the final results were generated from confirm dataset.


## Normal range of each variable:

|Ratio of total to HDL-Cholesterol    | Category         |
|-------------------------------------|------------------|
| Less than or equal to 3.5           | Desirable        |
| 3.5 - 5                          	  | Normal           |
| More than 5                         | High Risk        |

*Source: https://www.urmc.rochester.edu/encyclopedia/content.aspx?ContentTypeID=167&ContentID=lipid_panel_hdl_ratio#:~:text=In%20general%3A,1%20is%20considered%20very%20good.*


|BMI              | Category          |
|-----------------|-------------------|
| Less than 18.5  | Underweight       |
| 18.5 - 25       | Healthy           |
| 25 - 30         | Overweight        |
| 30 - 35         | Class 1 obesity   |
| 35 - 40         | Class 2 obesity   |
| 40 or higher    | Severe obesity    |

*Source: https://www.cdc.gov/obesity/basics/adult-defining.html#:~:text=If%20your%20BMI%20is%20less,falls%20within%20the%20obesity%20range.*


|Glycohemoglobin  | Category          |
|-----------------|-------------------|
| Below 5.7%      | Normal            |
| 5.7% - 6.4%     | Prediabetes       |
| 6.5% or higher  | Diabetes          |

*Source: https://www.cdc.gov/diabetes/basics/getting-tested.html*


