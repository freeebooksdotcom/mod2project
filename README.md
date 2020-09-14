# Austin Animal Shelter
by Anton Haugen and Ignacio Ruiz

### Sources
-Database<br>
https://www.kaggle.com/aaronschlegel/austin-animal-center-shelter-outcomes-and<br>
-Webscrape<br>
https://docs.thedogapi.com/api-reference/models/breed


# Introduction
The goal of this project is to assist the Austin Animal Shelter predict the potential length of time that a dog will spend in the shelter. We used a version of Austin Animal Shelter's data provided on Kaggle by Aaron Schlegel as our base. To complement the data provided we used the Dog API and webscraped American Kennel Club for breed statistics. In doing so, we hoped to providing a predictive timeline for this and other shelters across the country. Although Austin Animal Shelter does not suffer from such, our model hoped to provide accurate prediction to better prepare the shelter to avoid issues such as lack of adequate living conditions and avoidable expense.

# Model
![Image](images/target_distribution.png?raw=true)


### The Data
While the data we had was a good base, we needed more continuous variables to create a Linear Regression model. Most of the values on our data were categorical and thus were binned. We proceeded by making several dummy variables such as intake_month, age_bins, and color_bins so that these string variables could have an impact in our modelling process.

While analyzing our data by analyzing our data we found that dogs tend to be adopted more during the weekend than any other day. 
![Image](images/weekly_adoptions.png?raw=true)

We discovered through data cleaning that most dogs aside from being stray dogs, were mostly surrendered by their owners, which could give us the insight of what the center can expect their intakes to be.
                    ![Image](images/intake_reason.png?raw=true)


### Modeling
Since our data is not normally distributed we decided to also explore using a Poisson distribution for our predictive model in addition to our Linear Regressions. 

We started with linear regression. Using linear regression without polynomial interaction our model turned out with a quite low R2. 

While using different methods like k-best, T score or lasso, we found that K-best and T score were better fits when using polynomial interactions.

The model tended to be over fit, but we were able to find the best option which would result in using Lasso for the final model.
![Image](images/scaled_coefficients.png?raw=true)
When we tried our poisson distribution, we realized models based on our features were not capturing extreme values, even when the dependent variable was capped at 60.
![Image](images/poisson_error250.png?raw=true)
![Image](images/poisson_error.png?raw=true)

We performed a secondary eda and found that most of these dogs were Pit Bulls. 
![Image](images/value_count_breeds.png?raw=true)

Through a one-way ANOVA, we found that Pit Bulls had a mean number of days statistically significant from other breeds. 
![Image](images/average_days.png?raw=true)

So we reengineered our models to introduce a 'is_pitbull' feature, which improved our models
![Image](images/poisson_error250_pitbull.png?raw=true)
![Image](images/pitbull_coefficients.png?raw=true)

Though the Poisson model provided great insights, our best predictive model was that from Lasso feature selection because it captured interactions between features that our poisson could not.
![Image](images/lassopredictions.png?raw=true)

### Conclusions
While initially we believed that adopters' breed preferences would cancel each other out, our EDA for our final model allowed us to understand how significant cultural factors were to dog selection. For a future predictive model we would like to find other contributing factors to extreme values that are not represented in the data set.
Considering how Austin's demographics are changing, we would also like to find ways to better consider adopter preferences and cultural milieu compared to those of former owners. 


