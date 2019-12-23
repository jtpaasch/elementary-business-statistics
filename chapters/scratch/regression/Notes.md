
# Module 14 - Lecture 1 - Dependent and independent variables

* We talked about correlation.
  * It says whether there is a relationship between random variables.
  * And how strong it is.
* Now it's time to dig in deeper. 
  * To understand the relationship between the variables.
  * The technique we use to do this is called regression.

* We look at a data set with more than two random variables.
  * We have a hunch that one of them is explained by the other.
    One of them depends on the other.
  * Example:
    * X = Number of ad impressions on google for a book
    * Y = Number of copies of that book sold.

    Impr | Sales
    ------------
    0.25 | 0.325
    0.5  | 1.203
    0.75 | 1.735
    1    | 1.005
    1.5  | 3.230
    1.75 | 4.425
    2    | 3.765

    * We suspect that Y depends on X.
      * When X goes up, Y goes up.
      * Plot it:
    
    y
    ^
  5 +
    |                    x   
  4 +                      
    |                       x
  3 +                x
    |
  2 +        x   
    |     x      
  1 +           x
    |  x
    +--+--+--+--+--+--+--+--+--+--> x
                1           2

    * Some descriptions:
      * Y is the response variable, X is the stimulus variable.
      * Y is the response variable, X is the explainer variable.
      * Y is the dependent variable, X is the independent variable.
    * The key is, the influence goes one way.
    * With regression, we want to model this relationship. 

    * Note: you can have many explainer variables, for one response variable.
      * One explainer: simple regression.
      * Many explainers: multiple regression.


# Module 14 - Lecture 2 - Models

* So, we want to model the relationship between:
  * a response variable
  * an explainer variable
* What is a model, in general?
* Examples:
  * Think of model trains, or model boats.
    * Tiny replicas. Imagined versions of the real thing.
  * Think of a crime scene diorama, for a court case.
    * Tiny replica. Imagined version of the real thing.
* Two features of a model that matters:
  * It's an imagined version. Not exactly identical.
    * Example:
      * Trains much tinier than the real things.
      * Crime scene missing irrelevant details. Made of carbboard, not brick.
  * It helps with predictions/understanding.
    * Example:
      * Maybe you build a model boat, and you test out some big waves in the bath.
      * The crime scene diorama helps understand what must have happened.

* Let's look at our data again.
  
    Impr | Sales
    ------------
    0.25 | 0.325
    0.5  | 1.203
    0.75 | 1.735
    1    | 1.005
    1.5  | 3.230
    1.75 | 4.425
    2    | 3.765

  * Plot it.

    y
    ^
  5 +
    |                    x   
  4 +                      
    |                       x
  3 +                x
    |
  2 +        x   
    |     x      
  1 +           x
    |  x
    +--+--+--+--+--+--+--+--+--+--> x
                1           2


  * We think there's a relationship of X to Y.
  * We want to model it.
    * So what's a model? An imagined version of the real thing.
    * What's the real thing? A relation! A set of pairs.
  * We don't have all the pairs. So we have to guess.
  * We want to build a model that approximates the real relationship.

  * A good model in this case will be a line.
  * The least distance from the actual points is best.

  * Notice:
    * It helps with predictions. We can guess roughly for a given x.
    * But we're not exact. There's some error.

* Note: since the model is a line, we call it linear regression.


# Module 14 - Lecture 3 - Line algebra

* Line with some points.
  * Draw them.
* Continuous line?
  * Too many points.
  * We can make a formula, that gives us y, for any given x.

* Classic formula:
  * y = mx + b
    * where m is slope (rise over run)
    * b is intercept

* Let's take slope first.

* Example:
  * {(0, 0), (1, 1), (2, 2), (3, 3)}
  * y = x (rise over run is 1 over 1)
    * If x = 0, returns 0. Plot it.
    * If x = 1, returns 1. Plot it.
    * Etc.
* Example:
  * {(0, 0), (1, 2), (2, 4), (3, 6)}
  * y = 2x (rise over run is 2 over 1)
    * If x = 0, return 0. Plot it.
    * If x = 1, return 2. Plot it.
    * Etc.
* Example:
   * {(0, 0), (1, 0.5), (2, 1), (3, 1.5)}
   * y = 0.5x (rise over run is 1 over 2)

* Let's take intercept.
  * Our lines went through (0, 0).
  * But what if we want to push it up 2.
    * We add 2 to every y.
      * So mx + 2.
    * That's b in the original equation.


# Module 14 - Lecture 4 - Finding a regression line

* The formula for a line is mx + b.
* We have the same thing with linear regression.
  * y = beta_0 + beta_1 x + epsilon
    * beta_0 is the intercept
    * beta_1 is the slope
    * epsilon is the error
  * Note that these are population parameters.

* We can estimate (or estimate a model) like this:
  * y^ = b0 + b1x
    * b1 = Sum(x - xbar)(y - ybar) / Sum(x - xbar)^2
    * b0 = ybar - b1 xbar
    * y^ is the estimated value of y

* Example:
  
    Impr | Sales
    ------------
    0.25 | 0.325
    0.5  | 1.203
    0.75 | 1.735
    1    | 1.005
    1.5  | 3.230
    1.75 | 4.425
    2    | 3.765

    y
    ^
  5 +
    |                    x   
  4 +                      
    |                       x
  3 +                x
    |
  2 +        x   
    |     x      
  1 +           x
    |  x
    +--+--+--+--+--+--+--+--+--+--> x
                1           2


  * Find xbar: 1.107
  * Find ybar: 2.241

  * Table to find b1

    Impr | Sales | (x - xbar) | (y - ybar) | (x - xbar)(y - ybar) | (x - xbar)^2
    -----------------------------------------------------------------------------
    0.25 | 0.325 | -0.857     | -1.916     | 1.642                | 0.734
    0.5  | 1.203 | -0.607     | -1.038     | 0.630                | 0.368
    0.75 | 1.735 | -0.357     | -0.506     | 0.181                | 0.127
    1    | 1.005 | -0.107     | -1.236     | 0.132                | 0.011
    1.5  | 3.230 | 0.393      | 0.989      | 0.389                | 0.154
    1.75 | 4.425 | 0.643      | 2.184      | 1.404                | 0.413
    2    | 3.765 | 0.893      | 1.524      | 1.361                | 0.797
                                           --------------------------------------
                                             Sum: 5.739             Sum: 2.604
                                             b1 = 2.204

  * Then find b0:
    * ybar - b1 xbar = 2.241 - (2.204 * 1.107) = -0.199

  * Our line: 
    * y^ = -0.199 + 2.204x
    * Or: y^ = 2.204x - 0.199



# Module 14 - Lecture 5 - Errors and coefficient of determination

  * Fill in the y hats:

    Impr | Sales | Pred  |
    ----------------------
    0.25 | 0.325 | 0.352 |
    0.5  | 1.203 | 0.903 |
    0.75 | 1.735 | 1.454 |
    1    | 1.005 | 2.005 |
    1.5  | 3.230 | 3.107 |
    1.75 | 4.425 | 3.658 |
    2    | 3.765 | 4.209 |

  * Find the SST (Total Sum of Squares), where ybar is 2.241:

    Impr | Sales | Pred  | yi - ybar | (yi - ybar)^2
    -------------------------------------------------
    0.25 | 0.325 | 0.352 | -1.916    | 3.671 
    0.5  | 1.203 | 0.903 | -1.038    | 1.077
    0.75 | 1.735 | 1.454 | -0.506    | 0.256
    1    | 1.005 | 2.005 | -1.236    | 1.528
    1.5  | 3.230 | 3.107 | 0.989     | 0.978
    1.75 | 4.425 | 3.658 | 2.184     | 4.770
    2    | 3.765 | 4.209 | 1.524     | 2.323
                                     -----------------
                                      Sum: 14.603

  * Find SSE (Sum of Squared Errors):
    * Residual

    Impr | Sales | Pred  | yi - y^ | (yi - y^)^2
    ---------------------------------------------
    0.25 | 0.325 | 0.352 | -0.027  | 0.000729
    0.5  | 1.203 | 0.903 | 0.3     | 0.09
    0.75 | 1.735 | 1.454 | 0.281   | 0.079
    1    | 1.005 | 2.005 | -1      | 1
    1.5  | 3.230 | 3.107 | 0.123   | 0.015
    1.75 | 4.425 | 3.658 | 0.767   | 0.588
    2    | 3.765 | 4.209 | -0.444  | 0.197
                                   -------------------
                                    Sum: 1.97 

  * Find the SSR (Sum of Squares due to Regression):

    Impr | Sales | Pred  | y^ - ybar | (y^ - ybar)^2
    ------------------------------------------------
    0.25 | 0.325 | 0.352 | -1.889    | 3.568
    0.5  | 1.203 | 0.903 | -1.338    | 1.79
    0.75 | 1.735 | 1.454 | -0.787    | 0.619
    1    | 1.005 | 2.005 | -0.236    | 0.056
    1.5  | 3.230 | 3.107 | 0.866     | 0.75
    1.75 | 4.425 | 3.658 | 1.417     | 2.008
    2    | 3.765 | 4.209 | 1.968     | 3.873
                                     ---------------
                                       Sum: 12.664
  * SSR = SST - SSE

  * Coefficient of determination

    * R^2 = SSR / SST
    * R^2 = 12.6 / 14.6 = 0.86
    * So: 86% of the error is eaten up by the regression
      * Or: our regression model explains 86% of the data we have.
      * The remainder is due to error.

