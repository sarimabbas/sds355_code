# ISLR book

## Linear Regression

* Predictor variable: a predictor variable is like an X in the linear regression equation
* RSS is the residual sum of squares
    * ![image-20190913155907422](notes.assets/image-20190913155907422.png)



### Standard error of estimates

We need to see how well B~1~ and B~0~ do under repeated sampling 

z

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









### R^2^ and Correlation



<img src="notes.assets/image-20190912234813361.png" alt="image-20190912234813361" style="zoom:50%;" />



R^2^ is the squared correlation of sample data (for linear models)

![image-20190912234905632](notes.assets/image-20190912234905632.png)



### Categorical to Numerical Data



####  Integer Encoding

As a first step, each unique category value is assigned an integer value.

For example, “*red*” is 1, “*green*” is 2, and “*blue*” is 3.

This is called a label encoding or an integer encoding and is easily reversible.

For some variables, this may be enough.

The integer values have a natural ordered relationship between each other and machine learning algorithms may be able to understand and harness this relationship.

For example, ordinal variables like the “place” example above would be a good example where a label encoding would be sufficient.

#### One-Hot Encoding

For categorical variables where no such ordinal relationship exists, the integer encoding is not enough.

In fact, using this encoding and allowing the model to assume a natural ordering between categories may result in poor performance or unexpected results (predictions halfway between categories).

In this case, a one-hot encoding can be applied to the integer representation. This is where the integer encoded variable is removed and a new binary variable is added for each unique integer value.

In the “*color*” variable example, there are 3 categories and therefore 3 binary variables are needed. A “1” value is placed in the binary variable for the color and “0” values for the other colors.

For example:



![image-20190913014615372](notes.assets/image-20190913014615372.png)



The binary variables are often called “dummy variables” in other fields, such as statistics.



## Multiple Linear Regression

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

        

### F-statistic



* R^2^ : percentage of variance explained
* ![image-20190913163629994](notes.assets/image-20190913163629994.png)

* Huge F-statistic says that atleast one of the predictors has a strong effect on the outcome.





### Deciding on best variables

**All subsets / best subsets regression**



* Compute the least squares fit for all possible subsets, and then choose between them based on some criterion that balances training error with model size.
* There are 2^p^ subsets, where *p* is the number of predictors, this can become very large



#### Forward selection 

* Keep adding one variable at a time, which best improves the RSS

![image-20190913164013963](notes.assets/image-20190913164013963.png)



* Stop when all variables have a p-value below some threshold. 



#### Backward selection



![image-20190913164056679](notes.assets/image-20190913164056679.png)



* Remove the variable with the least significant t-statistic



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



### Synergy or Interaction effects

Suppose spending money on radio advertsiing actually increases effectiveness of radio advertising. 

![image-20190913165234460](notes.assets/image-20190913165234460.png)



A way to check this is by multiplying the two predictors to create a new one. 



The rearranged equation is saying: when radio changes, the coefficient of TV changes by amount: (B~1~ +B~3~)* radio.

![image-20190913165429289](notes.assets/image-20190913165429289.png)

And we can see the interaction is significant, because **TV*radio** t-stat is high, and p-value is low. 



The R^2^ for the model also increased as a result. More variance was explained by adding that extra predictor.



Continue watching the video at this point: 5:45: https://youtu.be/IFzVxLv0TKQ?t=345













s



p  = 3

Y = b0 +  (b1 * snow) *   (b2 * tmax) *  (b3* 



## KNN



![0*5OA0zZ_L7_IK5F48](notes.assets/0*5OA0zZ_L7_IK5F48.png)















