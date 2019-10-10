# SDS 355 Notes 



## Regression 

### Linear Regression

* Predictor variable: a predictor variable is like an X in the linear regression equation
* RSS is the residual sum of squares
    * ![image-20190913155907422](notes.assets/image-20190913155907422.png)



#### Standard error of estimates

We need to see how well B~1~ and B~0~ do under repeated sampling 



![image-20190913160044822](notes.assets/image-20190913160044822.png)



* Sigma^2^ is the variance of the noise around the line 
* B~1~ / slope
    * The standard error is directly proportional to the noise around the line
    * The standard error is inversely proportional to how much the x values are spread across the x-axis. The more spread out the x values, the more precise the line. (i.e. there is a spread of values on the horizontal axis, which kind of makes intuitive sense: if all the x values in the sample concentrated together, then it would be hard to visually even fit a slope/line)
* B~0~ / intercept
    * somewhat similar reasoning 



#### 95% confidence interval

The 95% confidence interval: 

* the range of values such that, with 95% probability, the range will contain the true unknown value of the parameter. 

<img src="notes.assets/image-20190913160451356.png" alt="image-20190913160451356" style="zoom: 50%;" />



#### R^2^ and Correlation



The meaning of the R-squared statistic is the proportion of the variance **in the response variable of the data used to train the model**that is explained by the model. While you can calculate this statistic for a test dataset, it has no such meaning. The fact that this homework problem gives a negative answer, and that a meaningful R-squared is between 0 and 1, attests to this fact. 



<img src="notes.assets/image-20190912234813361.png" alt="image-20190912234813361" style="zoom:50%;" />



R^2^ is the squared correlation of sample data (for linear models)

![image-20190912234905632](notes.assets/image-20190912234905632.png)



#### Categorical to Numerical Data

##### Integer Encoding

As a first step, each unique category value is assigned an integer value.

For example, “*red*” is 1, “*green*” is 2, and “*blue*” is 3.

This is called a label encoding or an integer encoding and is easily reversible.

For some variables, this may be enough.

The integer values have a natural ordered relationship between each other and machine learning algorithms may be able to understand and harness this relationship.

For example, ordinal variables like the “place” example above would be a good example where a label encoding would be sufficient.

##### One-Hot Encoding

For categorical variables where no such ordinal relationship exists, the integer encoding is not enough.

In fact, using this encoding and allowing the model to assume a natural ordering between categories may result in poor performance or unexpected results (predictions halfway between categories).

In this case, a one-hot encoding can be applied to the integer representation. This is where the integer encoded variable is removed and a new binary variable is added for each unique integer value.

In the “*color*” variable example, there are 3 categories and therefore 3 binary variables are needed. A “1” value is placed in the binary variable for the color and “0” values for the other colors.

For example:



![image-20190913014615372](notes.assets/image-20190913014615372.png)



The binary variables are often called “dummy variables” in other fields, such as statistics.

### Multiple Linear Regression

* The **ideal** scenario is if all the predictors are **uncorrelated** - this is called a **balanced design**
* Correlations amongst predictors cause problems 
    * Interpretations become hazardous 
    * Variance of all coefficients increase dramatically
        * E.g.: two predictors that are almost identical (TMAX and TMIN from PSET 1). Their coefficients cannot be separated. 
    * We can't make interpretations that theorize what will happen to Y when X~1~ changes, because a change in X~1~ could also change X~2~, X~3~ etc.
    * In summary, predictors can change together



---



* Again, we try to minimize the RSS



![image-20190913162532013](notes.assets/image-20190913162532013.png)



* Intercept is not very important: the sales value when all other predictors are zero

* But the slopes coefficients are more importtant

* T-statistic:

    * $t-statistic = \frac{coefficient}{ std. error}$
    * At alpha = 0.05, a t-value of > 2 is significant

* TV and radio have very big effects, but newspaper is not much of an effect

* On its own, newspaper might be significant, but in the presence of the other two predictors, it is not significant 

    * This might be because radio and newspaper are correlated at 0.3541, so tt might be the case that the radio has **soaked up** all of newspaper's effect

        

#### F-statistic



* R^2^ : percentage of variance explained
* ![image-20190913163629994](notes.assets/image-20190913163629994.png)

* Huge F-statistic says that atleast one of the predictors has a strong effect on the outcome.



#### Deciding on best variables



##### All subsets / best subsets regression



* Compute the least squares fit for all possible subsets, and then choose between them based on some criterion that balances training error with model size.
* There are 2^p^ subsets, where *p* is the number of predictors, this can become very large

##### Forward selection 

* Keep adding one variable at a time, which best improves the RSS

![image-20190913164013963](notes.assets/image-20190913164013963.png)



* Stop when all variables have a p-value below some threshold. 

##### Backward selection



![image-20190913164056679](notes.assets/image-20190913164056679.png)



* Remove the variable with the least significant t-statistic



#### Synergy or Interaction effects

Suppose spending money on radio advertsiing actually increases effectiveness of radio advertising. 

![image-20190913165234460](notes.assets/image-20190913165234460.png)



A way to check this is by multiplying the two predictors to create a new one. 



The rearranged equation is saying: when radio changes, the coefficient of TV changes by amount: $(B_1 +B_3)* radio$

![image-20190913165429289](notes.assets/image-20190913165429289.png)

And we can see the interaction is significant, because **TV*radio** t-stat is high, and p-value is low. 



The R^2^ for the model also increased as a result. More variance was explained by adding that extra predictor.



Continue watching the video at this point: 5:45: https://youtu.be/IFzVxLv0TKQ?t=345



### Qualitative / Categorical / Factor variables

E.g.

* gender: male/femaile
* marital status
* ethnicity



**Dummy variables** are new variables that can numerically represent categorical features



![image-20190913164515626](notes.assets/image-20190913164515626.png)



Here we see that while the coefficient is 19.73, i.e. if the sample is female, then the credit card statement is expected to be 19.73 times, given the other predictors.  

![image-20190913164623383](notes.assets/image-20190913164623383.png)

But the coefficient is not statistically significant, because the t-statistic is small, and p-value is large. 

---

For categorical variables like month, make more dummy variables. 

![image-20190913164838955](notes.assets/image-20190913164838955.png)

ISLR says: **have one fewer dummy variable than the number of categorical states.** Why? Because one state could be when no other dummy variable is present.  



### Decision Tree Regression

* A Non-linear, Non-continuous regression model 



#### Intuition



* CART: classification and regression trees 



* Imagine two predictors on the x and y axis, and you have to predict the dependent variable $y$ on the z-axis

![image-20190930165024377](notes.assets/image-20190930165024377.png)



* The algorithm will create tree-like splits
    * This is based on information entropy 
    * the algorithm stops when an information entropy threshold is met and no more splits are created or if there is a minimum leaf size 

![image-20190930165301271](notes.assets/image-20190930165301271.png)



* Example decision tree. Each node is testing points against the splits:



![image-20190930165554342](notes.assets/image-20190930165554342.png)

![image-20190930165600788](notes.assets/image-20190930165600788.png)



* How to turn knowledge about leaves into y-values? 

    * Take averages of all points in a leaf, and this is the value/label assigned to all of them

    

![image-20190930170006779](notes.assets/image-20190930170006779.png)



* Any future points will follow the decision tree and be assigned the same label as the leaf they end up in

![image-20190930170159700](notes.assets/image-20190930170159700.png)



* These predictions can be tested against ground truth in a confusion matrix



#### Code

![image-20190930231240522](notes.assets/image-20190930231240522.png)



* Most non-linear regression models are continuous, but this one is not

![image-20190930231652775](notes.assets/image-20190930231652775.png)





### Ensemble learning 

- Take the same algorithm multiple times to make something more powerful 

    

#### Random forest regression



##### Intuition 



Same as decision trees: 

* Non-linear regression model
* Non-continuous regression 



![image-20190930232900539](notes.assets/image-20190930232900539.png)

* Usually you use 500 trees or so
    * And average 500 predictions for the value of y
    * So you're predicting based on a forest of trees



##### Code

![image-20190930233821612](notes.assets/image-20190930233821612.png)



* More decision trees in forest -> more steps in the graph
    * However there is convergence, so number of steps wont increase that much from 50 trees to 100 trees
        * But perhaps the steps will be better chosen to make better predictions 

![image-20190930234208345](notes.assets/image-20190930234208345.png)

* E.g. the prediction at position level 4 is the result of averaging the 10 tree predictions for level 4



As the 





### Regression performance 







## Classification

### KNN



![0*5OA0zZ_L7_IK5F48](notes.assets/0*5OA0zZ_L7_IK5F48.png)



### Naive Bayes

#### Bayes theorem 



#### Naive Bayes classifier



P(category | features) 

e.g. P(walks | X) = P(walks | age, salary)



Here X is the list of features = [age value, salary value]



![image-20190917173558876](notes.assets/image-20190917173558876.png)



* The prior is easiest to calculate 
* Marginal likelihood is the next easiest to calculate 



You do the same to find P(Drives | X)

Once you have both probabilities, you determine which class to put the data point in. 



#### Calculating priors



Easy, just take all the data points that are in a class and divide by the total  number of points 

#### Calculating marginal likelihood

No point will have the exact same feattures, so you can set a tthreshold instead:



![image-20190917175927610](notes.assets/image-20190917175927610.png)



Here the grey circle has a center, which is where the new point would go. 

The radius is the threshold of similar points to include.



So there are 4 points out of 30 points total that have a similar features



Hence P(X) = 4/30

![image-20190917180107626](notes.assets/image-20190917180107626.png)

#### Calculating likelihood



**P(X | walks)**



You know there are only 4 points that are similar to X

The conditional probability is on the **walks** class in red, of which there are 10 points



So, given the 10 points in the **walks** class, how many points are similar to X?



That's just 3/10 

![image-20190917180348949](notes.assets/image-20190917180348949.png)

#### Posterior probability



![image-20190917180410547](notes.assets/image-20190917180410547.png)



P(Drives | X) turns out to be 0.25 



So we can guess that the new data point, with similar features X, should be in the **walks** class

#### Why Naive?



Requires some independence assumptions which are part of the Bayes theorem

E.g. we assume Age and Salary are independent, but there might be correlation bettween theme

I.e. the **features are assumed to be independent of each other**

#### Dropping marginal likelihood



- **P(X)**: points deemed to be similar to the point we are about to add into the data set
- P(X) doesnt change, whether you calculate it in the step for P(Walks | X) or for P(Drives | X)
- At the end of the day you divide both expressions by it
- so you can drop it! but only **for comparison purposes**. Calculating actual value requires the full expression though

#### More than 2 classes 



- In current example, you had P(class 1 | X) and P(class 2 | X), where class 1 = walks, and class 2 = drives. The probabilities added up to 1.0 e.g. 0.75 + 0.25 = 1.0 
- For more than 2 classes, you can do calculations in the same way, and P(class 1 | X) + P(class 2 | X) + P(class 3 | X) = 1.0

#### Python code

https://www.udemy.com/machinelearning/learn/lecture/5740200#overview

![image-20190917182521923](notes.assets/image-20190917182521923.png)  



### Logistic Regression

* Logistic regression is a linear classifier, even though it uses a non-linear sigmoid function 
    * With two predictors, the result is a straight line
    * With three predictors, it is a straight plane 



### Decision tree classification



![image-20190930235731586](notes.assets/image-20190930235731586.png)



![image-20190930235747570](notes.assets/image-20190930235747570.png)









#### Intuition

![image-20190930161325032](notes.assets/image-20190930161325032.png)

* simple linear regression is a straight line ($ y = b_0 + b_1x$) through the data





* Logistic regression helps us fit a line through data separated into classes
* Example, will people buy the car/take an action with increasing age?:



![image-20190930161920747](notes.assets/image-20190930161920747.png)



![image-20190930162055496](notes.assets/image-20190930162055496.png)



* Plug the linear regression $y$ into the sigmoid function $p$ and solve for $y$
* On the y-axis is probability $p$ and on the x-axis is the predictor
* We can't get the true value of y, but we can predict $y^{hat}$. Anything above 50% probability is classified as being in one class

![image-20190930162850035](notes.assets/image-20190930162850035.png)



#### Code

* Follow the classification template and do the preprocessing 



![image-20190930163747375](notes.assets/image-20190930163747375.png)



![image-20190930164132153](notes.assets/image-20190930164132153.png)

* This is a logistic regression with two predictors: salary and age
* Red points are people who took action/purchased SUV (class 1) and green points are people who did not (class 2)
* The red and green regions are called "prediction regions" according to the classifier
    * These are not fully accurate, since some ground truth red and green points are in opposite regions

### Confusion matrix

![image-20190930163517380](notes.assets/image-20190930163517380.png)

* Parameters
    * The true labels 
    * The labels predicted by the classifier

* Output

    * ![image-20190930163648095](notes.assets/image-20190930163648095.png)

    * 65 and 24 are correct
        * True positive
        * True negative
    * 8 and 3 are incorrect
        * False positive
        * False negative



### Classification template

#### Import libraries

#### Import data

![image-20190918152852638](notes.assets/image-20190918152852638.png)



* What is `[:, [2,3]]` ? The first with the colon is saying: select all rows
* The next part with `[2,3]` is saying: the columns at indexes 2 and 3
* For `y`, we are selecting a single dependent variable column at index 4. 

#### Train test split

![image-20190918153127630](notes.assets/image-20190918153127630.png)

#### Feature scaling

![image-20190918153208064](notes.assets/image-20190918153208064.png)



* Don't scale the `y` / dependent variable
* Maybe scale categorical variables - it might help but other times it might not make sense to do it
* Scale the independent variables for train
* And scale the test independent variables according to the train data



## Model selection



### Complexity of model 



![image-20191008194228433](notes.assets/image-20191008194228433.png)



### K-fold cross-validation

* usually we do test/train set
* but we get variance problem:
    * multiple test sets are needed to judge performance
    * but we only have one test set!
* So we split training set into k=10 folds
    * we iterate 9 times to train the model with 9 folds
    * we validate on the 10th fold



![image-20191008194120222](notes.assets/image-20191008194120222.png)









## Quiz



* stochastic gradient descent 
* cross validation
* model selection
	* section 38 in udemy 
* decision trees
	* regression
	* classification
	* random forest
* bias variance tradeoff

