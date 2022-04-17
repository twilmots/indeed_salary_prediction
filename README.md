# Webscraping and Salary Prediction Project

The purpose of this project was to webscrape job listing information from Indeed and then run a model to predict if the salary would be HIGH or LOW. 

The below was the brief set for the project. My solution follows the brief. 

### Directive

You're working as a data scientist for a contracting firm that's rapidly expanding. Now that they have their most valuable employee (you!), they need to leverage data to win more contracts. Your firm offers technology and scientific solutions and wants to be competitive in the hiring market. Your principal wants you to

   - determine the industry factors that are most important in predicting the salary amounts for these data.

To limit the scope, your principal has suggested that you *focus on data-related job postings*, e.g. data scientist, data analyst, research scientist, business intelligence, and any others you might think of. You may also want to decrease the scope by *limiting your search to a single region.*

Hint: Aggregators like [Indeed.com](https://www.indeed.com) regularly pool job postings from a variety of markets and industries.

**Goal:** Scrape your own data from a job aggregation tool like Indeed.com in order to collect the data to best answer this question.

---

### My Results

Our task was to scrape job information from Indeed across varying markets to try and predict whether a job would be classified as high salary or low salary. The Decision Tree Ensemble method was our most successful model achieving an accuracy score of 0.899% with strong generalization. 

#### Data Collection

In order to gather our data, I built a custom webscraper to gather data from Indeed. We leveraged this data set for the modelling. 

#### Data Cleaning

For the purpose of this task, we were only able to use data that had salary information in a yearly format. As such, we removed any rows with no salary information or salary information that was not yearly. Next, we turned the salary information into a integer that we could use for processing. In the instances where there was a salary range, we took the mean. 

After successfully cleaning the data, we turned our salary information into a target variable. As this was a classification problem, we wanted a threshold to determine if a salary was HIGH or LOW. To achieve this, we used the median salary of the entire data set. Our target variable was now a binary variable that was 1 of the salary of a specific job post was over the median, or 0 if it was below. 

With our data all ready to go, we were ready to undertake some feature engineering. 

#### Feature Engineering

As a lot of our data was in text format, we took advantage of the TF-IDF method in Natural Language Processing. This method quantifies words in a document or corpus of text providing. This quantification allows us to feed this information into a classification model. We chose to leverage this method on the 'Location' data that we had available. 

In addition to applying TF-IDF to the 'Location' data, we generated key word features that looked through the 'Title' and 'Summary' of a job post and indicated if these contained any words that could indicate a higher paying job. For example in the title, we focused on words such as 'Senior', 'Manager' and 'Executive' as these are all titles held by individuals later in their career and could indicate a higher salary. These additional features proved valuable as running the model on just the 'Location' data yielded a lower score. 

#### Results

Using the bagging method combined with a Decision Tree as the base estimator, we were able to achieve an accuracy of almost 90% with a strong level of generalization. This means our model does well on unseen data so would work as expected if we put it into production. Also, if the team is concerned about predicting a high salary when it ultimately isn't one, we can easily adjust our threshold and build this concern into our model. This will lead to more incorrect Low Salary predictions, but it will lower the instances where we predict a High Salary and it turns out to be a Low Salary. 

#### Risk & Limitations

- Not all jobs had salary information, so we risk running our model on a subset of the types of jobs. 
- Our data also only focuses on the UK Data job market. So any predictions outside this scope is not advised. 
