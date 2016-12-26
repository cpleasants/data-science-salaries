# Web Scraping Indeed.com & Predicting Salaries
### Problem Statement:
As a job seeker, it is important for me to be able to know whether a job I'm applying to will be well-paid or not. Unfortunately, most job postings are not up-front about their salary range. So, I would like to be able to make a more educated guess about whether a job I'm interested in will be well-paid or not. 

### Goal
My goal is to create a statistical model that will accurately predict whether a job without a listed salary will be well-paid or not. I also want to identify features that are positively associated with higher-paid jobs so I could consider those things while I search.

### Methods
I started by scraping web data from https://www.indeed.com: 200 pages of results from each of 10 cities in the United States. I then extracted company name, location, page the post appeared on, job title, summary, salary (if it exists), date posted, whether or not it is a sponsored post, number of reviews, and star rating (if applicable). I then used this extracted data to calculate yearly salaries, whether or not it is inside the city, and common text features. Finally, I compared several models and found a Logistic Regression using Recursive Feature Reduction and Ridge Regularization to be the best model, and the most interpretable.

### Results
It is possible to predict whether a Data Science job will be higher or lower than the median pay based on star rating, city, and certain features in the title of the job postings. Based on cross-validated predictions, I correctly predicted 83.5% of the jobs correctly. 81% of the jobs I predicted would be high-salary were in fact high-salary, and I was able to correctly label 83% of all high-salary jobs. The following features all affect the odds a job will be higher-paid:
- Having the words "associate", "risk", "assistant", "analyst", or "research" in the title are associated with lower-payed jobs (12x, 5x, 4x, 3.5x, and 2.5x lower odds, respectively)
- Having the words "scientist" or "looking" in the summary are associated with higher pay (2.5x and 3.5x higher odds for each time each word, respectively, appears)
- Having the words "science", "data science/scientist", "machine", "learning", "engineer", "software", or "quantitative" are associated with higher pay (3.5x, 4x, 4x, 4.5x, 4.5x, 5.5x, and 11.5x higher odds, respectively)
- Being in an expensive city like DC or New York is associated with higher pay (over 4x higher odds)
- Being in the city limits is associated with higher pay (over 5x higher odds)


Jobs that have none of these features have about 1:11.9 odds (or  abouat a 8% chance) of being a high-paid job. To illustrate what all this means, I will provide an example. One job without a salary listed is:
- Data Scientist at Home Depot
- Summary: Strong communication and data presentation skills. Insights from data to solve business problems. The Data Scientist will develop the analytical infrastructure...
- In Atlanta, GA (one of the non-expensive cities, but inside the city).

Because of the words "Data Scientist" in the title, the base odds of 1:11.9 gets multiplied by 3.927. The fact that it is inside the city multiplies it by 5.013. The word "scientist" in the summary multiplies the odds again by 2.667. Therefore, the odds that this job's salary is higher than the median of $100,000 is about 4.4:1, or about 81.5%. I have chosen to set the threshold for considering something to be high-paid at the standard 50% because the stakes of false negatives and false positives are about equal (low either way), so this job would be labeled by my model as a high-paid job.

One way to truly test my model would be to continue to monitor jobs as they get posted and compare my predictions to future job postings that actually do provide salary info. Another way I could check my model would be to investigate the jobs a bit more and see if I can find a salary for jobs that don't list a salary in the search results. This would also help me to know whether my assumption that the jobs containing salaries and the ones not containing salaries are essentially equivalent.

### Risks and Assumptions:
The biggest assumption that I'm making in creating and applying this model is that there are no substantial differences between the types of jobs that include salary info and the types that don't. For instance, if only jobs that pay relatively well include salary information, this could completely spoil the application of my model. This goes along with the assumptions inherent in a logistic regression model, including no multicollinearity between variables and independence of errors.

### Data Dictionary (before final feature extraction):

Column Name|Data Type|Description
-----------|---------|-----------
company|String|Listed company name
location|String|Listed location
summary|String|Job Summary (cut off at about 160 characters)
title|String|Listed job title
salary|String|Listed salary (only a small portion included this)
date_posted|String|Time since posted (in hours or days)
star_rating|Float|Length of full-star image divided by length of empty-star image, multiplied by 5
start|Integer|Index of the first result in the page
number_reviews|String|Listed number of reviews
