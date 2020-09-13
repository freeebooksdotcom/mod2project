# Austin Animal Shelter
by Anton Haugen and Ignacio Ruiz

### Sources
-Database<br>
https://www.kaggle.com/aaronschlegel/austin-animal-center-shelter-outcomes-and<br>
-Webscrape<br>
https://docs.thedogapi.com/api-reference/models/breed


# Introduction
The goal of this project is to assist the Austin Animal Shelter in predicting the potential time that an animal will spend in the shelter. With our goal set, we decided on using their dataset as a base. To complement the data provided we took the decision of webscraping for dog weight and size information, this helped us compliment the original database and build a better predictive model. In doing so, we are looking into providing a solution to issues that are common in shelters across the country. Although our shelter does not suffer from such, our model is able to provide prediction and better prepare the shelter to avoid issues such as: dirty conditions, lack of veterinary care, lack of adequate food and water, etc.

# Model
![Image](images/target_distribution.png?raw=true)


### The Data
Whilst the data we had was a good base, most of the data needed to complement our data to add more continuous variables to better create a model. Most of the values on our data were categorical and in string form. We decided to proceed in making several dummy variables such as in the case of intakes per month. We created bins for the data that could be binned such as color or breed, by doing so, those string variables could have an impact in our modelling process.

We were able to discover whilst analyzing our data by analyzing our data we found that dogs tend to be adopted more during the weekend than any other day. 
![Image](images/weekly_adoptions.png?raw=true)

Also we were able to discover through data cleaning that most dogs aside from being stray dogs, were mostly surrendered by their owners, which could give us the insight of what the center can expect their intakes to be.
                    ![Image](images/intake_reason.png?raw=true)


### Modeling
Since our data is not normally distributed we decided to take on the route of comparing what could best fit our predictive models. We started with linear regression. Using linear regression and creating various features to accomodate the needs for linear regression our model turned out with a quite low R2. Using this we kept feature engineering.
While using different methods like k-best, T score or lasso, we found that K-best and T score did not fit our model.The model tended to be over fit, but we were able to find the best option which would result in using Lasso for the final model.

We wanted to compare if there could be a better model to predict our data. We used Poisson distribution to calculate a model that could benefit from variables being categorical. While the results of using linear regression gave us some insight, Using Poisson distribution gave the most accurate results. This conclusion comes from comparing our original data with the predictive model as seen below.
![Image](images/poisson_error250.png?raw=true)

we realized that the outliers shown above affected negatively the model and investigating showed that pitbulls who have been longer that 150 days were skewing our predictions.
![Image](images/value_count_breeds.png?raw=true)

After removing said outliers, we were able to have the most accurate model.
![Image](images/poisson_error250_pitbull.png?raw=true)


### Findings


