# QSS20 Final Project 
## Training Wreck: A Comparative Analysis of Assessment Scores Before and After Mental Health Training

## Data Sources
The data for this analysis was sourced from pre and post-training assessments conducted by the medical school. The datasets include:

- Med student pre assessment 2.8.23.csv: Contains the survey results from students before the training.
- Foundational Post Assessment 2.8.23.csv: Contains the survey results from the foundational group after the training.
- Intermediate Post Assessment 2.8.23.csv: Contains the survey results from the intermediate group after the training.
- Advanced Post Assessment 2.8.23.csv: Contains the survey results from the advanced group after the training.
- Module Satisfaction Evaluations 2.8.23.csv: Contains the survey results for feedback of the training

## Order to Run

1. [00_pull_assessment_data.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/00_pull_assessment_data.ipynb)


- Takes in:
    - Med student pre assessment 2.8.23.csv
    - Foundational Post Assessment 2.8.23.csv
    - Intermediate Post Assessment 2.8.23.csv
    - Advanced Post Assessment 2.8.23.csv

- What it does:
    - Loads in the datasets through their file paths

2. [01_merge_data_rename_columns.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/01_merge_data_rename_columns.ipynb)

- Takes in:
    - pandas dataframes created in previous notebook

- What it does:
    - Left join merges pre df to post df for each separate cohort, on 'IPAddress' Column
    - Renames the score columns: SC0y = Pre, SC0x = Post
    - Remove missing data
 
- Output:
    - foundational_data, intermediate_data and advanced_data
    - 3 new dataframes with merged and cleaned data
 
3. [02_paired_ttest.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/02_paired_ttest.ipynb)


- Takes in:
    - pandas dataframes created in previous notebook

- What it does:
    - Takes the clean data from the previous notebook
    - ensures all scores are int
    - uses stats.ttest_rel on each of the new dataframes to calculate a paired t-test
 
- Output:
    - 3 paired t-test results for each of the cohort's scores
 
4. [03_histogram_visualization.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/03_histogram_visualization.ipynb)


- Takes in:
    - pandas dataframes (foundational_data, intermediate_data and advanced_data) created in 01_merge_data_rename_columns.ipynb notebook

- What it does:
    - Transforms the dataframes into long format
    - Repeats the same plotting code for each of the three cohorts
    - Uses seaborn to make histograms that compare the distributions of Pre and Post scores
    - Adds KDE line to each histogram

- Output:
    - 3 histograms
    - foundational_histogram.png
    - intermediate_histogram.png
    - advanced_histogram.png

5. [04_correlation_test.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/04_correlation_test.ipynb)

- Takes in:
    - pandas dataframes (foundational_data, intermediate_data and advanced_data) created in 01_merge_data_rename_columns.ipynb notebook

- What it does:
    - Select 'Pre' and 'Post' columns and tag each entry with its cohort
    - Creates a cohort color palette
    - Uses matplotlib to make regression plots of each of the cohorts in a combined figure

- Output:
    - a regression plot
    - correlation_plot.png
 
6. [05_network_analysis.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/05_network_analysis.ipynb)


- Takes in:
    - pandas dataframes (foundational_data, intermediate_data and advanced_data) created in 01_merge_data_rename_columns.ipynb notebook

- What it does:
    - Adds a column for dummy variable for each cohort
    - Uses pandas concat to combine the dataframes with the extra dummy variable columns
    - Assigns quartiles to the scores in the combined df
    - Uses conditions and choices to create a cohort column that takes the dummy variables and assigns cohorts based off of it
    - Creates a network visualization by first looping throught the combined_df to create nodes for each participant
    - Assigns the quartiles to the nodes
    - Creates cohort color palette
    - Sets the participant color based on their cohort
    - Creates the network using nx.draw_networkx
    - Creates labels for the legends
    - Plots network visualization and adds legend

- Output:
    - network_visualization.png
 
7. [06_sentiment_analysis.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/06_sentiment_analysis.ipynb)

- Takes in:
    - pandas dataframes (foundational_data, intermediate_data and advanced_data) created in 01_merge_data_rename_columns.ipynb notebook
    - module satisfaction evaluations 2.8.23.csv

- What it does:
    - Imports Vader to use for sentiment analysis
    - Loads in module satisfaction evaluations 2.8.23.csv as a pandas df = satisfaction_df
    - Merges the cohort dfs with satisfaction_df using pandas merge, left join, on the 'IPAddress' column and dropping duplicates
    - Assign cohort labels to the new dfs: advanced_sat, intermediate_sat, foundational_sat
    - Combine the new dfs using pandas concat so the cohorts are still labelled
    - Calculates the sentiment score for each entry in the 'What was most helpful' column using VADER's sentiment analysis
    - Calculates the improvement in scores by subtracting the 'Pre' score from the 'Post' score for each participant, ensuring both are integers
    - Plots a regression of sentiment against Score improvement using matplotlib's regplot
    - Defines cohort color palette
    - Separates each cohort to calculate each sentiment score vs score improvement regression
    - Creates regression plot, legend and labels

- Output:
    - combined_sentiment_correlation.png
    - cohort_sentiment_regression.png
 
8. [original_combined_notebook.ipynb](https://github.com/mkmagee/final_proj_QSS20/blob/main/code/original_combined_notebook.ipynb)
- Notebook contains all the code used in all the notebooks in one place


## Data Storage
Our project data is stored externally. Access the data here: https://drive.google.com/drive/u/1/folders/1Kmc8P-Vfl7M4JghC5iyLpNhypoZiYTDi 
