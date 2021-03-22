
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


Automated Machine Learning is the process of automating the time-consuming, iterative tasks of ML model development. It allows to build the models with high scale efficiency & productivity all while sustaining the model quality.


Below is the screenshot of the configurations I used for automl.

![AutoML_Config](https://user-images.githubusercontent.com/55974694/111916814-c9359880-8aa2-11eb-824f-f8a61a4c191a.png)

The first configuration that we used here is experiment timeout time. Here we have used 30 mins as the maximum times as such automations do take a longer amount of time to run and can cost significantly high. Next, for the task, we have selected classification as we are predicting a categorical variable here and that comes under the category of classification. The next configuartion that we have selected here is primary metric. Since we are comparing models here based on their prediciting power, accuracy has been used here. The target variable that we have provided is 'Target' as that is the feature of this model that we are predicting.


### Results

**Run Details**

![runwidget_automl(1)](https://user-images.githubusercontent.com/55974694/111917278-2599b780-8aa5-11eb-8b96-16b0d12038ce.png)


![runwidget_AutoML(3)](https://user-images.githubusercontent.com/55974694/111917286-33e7d380-8aa5-11eb-91cf-d2a499e8a2b0.png)


Best Run model-ID and accuracy, along with other parameters:


![Best_AutoML(1)](https://user-images.githubusercontent.com/55974694/111917304-482bd080-8aa5-11eb-9d9c-f284b1aa8538.png)


![Best_AutoML(2)](https://user-images.githubusercontent.com/55974694/111917320-524dcf00-8aa5-11eb-8c2a-9871e30e983e.png)


From the screenshot below, we can see that Voting Ensemble was the best model with an accuracy of 80.04%


![Best_AutoMLmodel_RunId](https://user-images.githubusercontent.com/55974694/111917322-57ab1980-8aa5-11eb-9975-cc76d64ca1ae.png)



One of the major issue with this dataset is of class imbalance. That is something that can be taken care of to improve the prediction accuracy. Also, from the screenshots above we can see the parameters of the best auto ml model such as max_iter, n_jobs, etc.


The model can be improved by increasing the number of iterations or trying for various cross-validation folds. Deep learning/neural network based classification can also be used for better results.

## Hyperparameter Tuning

For this technique, I decided to choose logistic regression as:

1.   It is the most basic algorithm when it comes to classification and one should always start from basic models.

2.   It is easy to understand the results and simple to train

3.   The execution time is very fast

The two parameters: '--C' (Inverse of regularization strength. Smaller values cause stronger regularization) and '--max_iter' (Maximum number of iterations to converge) are selected for tuning using HyperDrive.

The choice used for C are (0.5,1.0), while that for max iterations are (5,10,20,30,40,50,100,150,200,250,300).

### Results

Run Details Widget

![runwidget_hyperdrive(1A)](https://user-images.githubusercontent.com/55974694/111917705-76121480-8aa7-11eb-9398-34e468a75616.png)


Here's the screenshot of best results and optimized parameters obtained using HyperDrive


![Configuration_hyperdrive](https://user-images.githubusercontent.com/55974694/111947547-b7d0a880-8b03-11eb-8d15-5d3e1d3cd89e.png)



Here's the screenshot of the best hyperdrive model 


![Best_Hyperdrivemodel_RunId](https://user-images.githubusercontent.com/55974694/111918037-364c2c80-8aa9-11eb-871d-082b228072aa.png)


To improve the results, we can further try different ranges of hyperparameters here. However, the best thing would be to handle the class imbalance in the dataset.


## Model Deployment


As AutoML allows to build the models with high scale efficiency & productivity all while sustaining the model quality,the  model from AutoML(Voting Ensemble) was deployed. 
The model choosen with AutoML is choosen for deployment: Azure Container Instance is used for deployment of the model as webservice. 


The details for method of deployment can be found in automl.ipynb under Model Deployment section.

An inference config was created using the score.py file and the service was deployed using the following code:

![model_deployment](https://user-images.githubusercontent.com/55974694/111918110-8cb96b00-8aa9-11eb-8cbb-81d8f7c71ca9.png)


From the screenshots below, we can also verify from the azure portal that the model was successfully deployed and is in a healthy state.

![Deployment_active_state(1)](https://user-images.githubusercontent.com/55974694/111918123-9c38b400-8aa9-11eb-9d3e-2f3c85e83b6e.png)


![Deployment_active_state(2)](https://user-images.githubusercontent.com/55974694/111918130-a5c21c00-8aa9-11eb-970c-d1f86de1fac7.png)


Now we can consume the endpoint using scoring URL genereated after deployment. The sample input to the endpoint is as below. This can also be found in endpoint.py file of the repository.


![endpoint](https://user-images.githubusercontent.com/55974694/111918147-bbcfdc80-8aa9-11eb-8d4d-b1779af76324.png)



After this, we tested the model endpoint.


![Deployment_test](https://user-images.githubusercontent.com/55974694/111918151-bd99a000-8aa9-11eb-9812-d4d2d35db94e.png)



**Result**

![Deployment_result](https://user-images.githubusercontent.com/55974694/111918152-be323680-8aa9-11eb-9966-116421b4f36c.png)


The model returns the output as 0.0,0.0 and 0.0 . This means that the first set of parameters would mean that the employee is not looking for a job change, the second set of parameters would mean that the employee is not looking for a job change and the third set of parameters would mean that the employee is also not looking for a job change.




## Future Work

1.     One of the thing that we have noticed in this project is that the target variable is imbalanced. We can take actions to account for that

2.     We can try different primary metrics instead of accuracy as accuracy can be biased if the dataset is imbalanced

3.     Feature Selection can be performed to select only thsoe features that positively contribute to the prediction of the outcome variable

## Screen Recording

https://youtu.be/yVuXC2dTrQs
