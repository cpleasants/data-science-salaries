# Web Scraping Indeed.com & Predicting Salaries
### Problem Statement:
As a job seeker, it is important for me to be able to know whether a job I'm applying to will be well-paid or not. Unfortunately, most job postings are not up-front about their salary range. So, I would like to be able to make a more educated guess about whether a job I'm interested in will be well-paid or not. 

### Goal
My goal is to create a statistical model that will accurately predict whether a job without a listed salary will be well-paid or not. I also want to identify features that are positively associated with higher-paid jobs.

### Methods
I started by scraping web data from.

### Results
It is possible to predict whether a Data Science job will be higher or lower than the median pay based on star rating, city, and certain features in the title of the job postings. Based on cross-validated predictions, I correctly predicted 73.6% of the jobs correctly. 74.8% of the jobs I predicted would be high-salary were in fact high-salary, and I was able to correctly label 70.9% of all high-salary jobs. The following features all increase the odds a job will be higher-paid:
- having a low star rating (over 5x the odds compared to a high star rating)
- having no star rating (over 5x the odds compared to a high star rating)
- being in an expensive city like New York, San Francisco, Boston, or DC (over 3.5x the odds compared to the other cities)
- being inside the city instead of in surrounding areas like the suburbs (over 2x the odds)
- having words in the title that suggest high-level jobs, like "senior", "manager", "director", "chief", etc. (over 3.5x the odds)
- having the word "Data Science" or "Data Scientist" in the title (over 5x the odds compared to titles without these words)
- having the word "engineer" in the title (over 2.5x the odds compared to titles without the word)
- haing "machine learning" in the title (over 16x the odds compared to titles without the word).


Jobs that have none of these features have about 1:7 odds (or  abouat a 12.5% chance) of being a high-paid job. To illustrate what all this means, I will provide an example. One job without a salary listed is:
- Data Scientist at Cox Automotive
- In Atlanta, GA (one of the non-expensive cities, but inside the city).
- 3.40 star rating (this is considered a low star rating)

Because of the words "Data Scientist, the base odds of 1:7 gets multiplied by 5.285. The fact that it is inside the city multiplies it by 2.119. The low star rating multiplies it again by 5.167. Therefore, the odds that this job's salary is higher than the median is about 8.3:1, or about 89%. I have chosen to set the threshold for considering something to be high-paid at the standard 50% because the stakes of falsely assuming a job will be high-paid when it's low-paid and the stakes of falsely assuming a job will be low-paid when it's actually high-paid are about equal (low either way), so this job would be labeled by my model as a high-paid job.

One way to truly test my model would be to continue to monitor jobs as they get posted and compare my predictions to future job postings that actually do provide salary info. Another way I could check my model would be to investigate the jobs a bit more and see if some of the ones listed as having no salary info actually do list salary in the longer description somewhere. This would also help me to know whether my assumption that the jobs containing salaries and the ones not containing salaries are essentially equivalent.

Below, I have continued to improve my model using other text features, so I have some additional discussion below.
### Risks and Assumptions:
The biggest assumption that I'm making in creating and applying this model is that there are no substantial differences between the types of jobs that include salary info and the types that don't. For instance, if only jobs that pay relatively well include salary information, this could completely spoil the application of my model. This goes along with the assumptions inherent in a logistic regression model, including no multicollinearity between variables and independence of errors.

### Future Improvements:

### Data Dictionary (after cleaning):

