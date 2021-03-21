
# Job Change of Data Scientists Prediction using Microsoft Azure
A company which is active in Big Data and Data Science wants to hire data scientists among people who successfully pass some courses which conduct by the company. MCompany wants to know which of these candidates are really wants to work for the company after training or looking for a new employment because it helps to reduce the cost and time as well as the quality of training or planning the courses and categorization of candidates.

In this project, we will predict if an individual is looking for a new job based on different factors using 2 techiques(AutoML & Hyperdrive).

## Dataset

### Overview
This dataset has been exported from Kaggle. Here's the link https://www.kaggle.com/arashnic/hr-analytics-job-change-of-data-scientists
### Task
The task is to predict whether the employee will leave the current job or not, based on the following factors-

enrollee_id : Unique ID for candidate
city: City code
city_ development _index : Developement index of the city (scaled)
gender: Gender of candidate
relevent_experience: Relevant experience of candidate
enrolled_university: Type of University course enrolled if any
education_level: Education level of candidate
major_discipline :Education major discipline of candidate
experience: Candidate total experience in years
company_size: No of employees in current employer's company
company_type : Type of current employer
lastnewjob: Difference in years between previous job and current job
training_hours: training hours completed
target: 0 – Not looking for job change, 1 – Looking for a job change

### Access
The data can be accessed by downloading the data into local server and then uploading it to Dataset subsection of Microsoft AzureML.

![Dataset(1)](https://user-images.githubusercontent.com/55974694/111916681-1b29ee80-8aa2-11eb-9e43-8f6e47db92c2.png)
![Dataset(2)](https://user-images.githubusercontent.com/55974694/111916763-896eb100-8aa2-11eb-8ef9-4b0341bb9914.png)





## Automated ML
Below is the screenshot of the configurations I used for automl.

![AutoML_Config](https://user-images.githubusercontent.com/55974694/111916814-c9359880-8aa2-11eb-824f-f8a61a4c191a.png)

The first configuration that we used here is experiment timeout time. Here we have used 30 mins as the maximum times as such automations do take a longer amount of time to run and can cost significantly high. Next, for the task, we have selected classification as we are predicting a categorical variable here and that comes under the category of classification. The next configuartion that we have selected here is primary metric. Since we are comparing models here based on their prediciting power, accuracy has been used here. The target variable that we have provided is 'Target' as that is the feature of this model that we are predicting.


### Results

![runwidget_automl(1)](https://user-images.githubusercontent.com/55974694/111917278-2599b780-8aa5-11eb-8b96-16b0d12038ce.png)

![runwidget_automl(2)](https://user-images.githubusercontent.com/55974694/111917281-2f231f80-8aa5-11eb-9a5b-ae57cd85e18f.png)

![runwidget_AutoML(3)](https://user-images.githubusercontent.com/55974694/111917286-33e7d380-8aa5-11eb-91cf-d2a499e8a2b0.png)

![Best_AutoML(1)](https://user-images.githubusercontent.com/55974694/111917304-482bd080-8aa5-11eb-9d9c-f284b1aa8538.png)

![Best_AutoML(2)](https://user-images.githubusercontent.com/55974694/111917320-524dcf00-8aa5-11eb-8c2a-9871e30e983e.png)

![Best_AutoMLmodel_RunId](https://user-images.githubusercontent.com/55974694/111917322-57ab1980-8aa5-11eb-9975-cc76d64ca1ae.png)


## Hyperparameter Tuning
*TODO*: What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search


### Results
*TODO*: What are the results you got with your model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

## Model Deployment
*TODO*: Give an overview of the deployed model and instructions on how to query the endpoint with a sample input.

## Screen Recording

https://youtu.be/yVuXC2dTrQs
