# NLLS-Gaussian + ICP Coding
Calculating and Comparing Non Linear Least Squares for Gaussian Functions

## Simple Non-Linear least squares for Gaussian function

First, go through the [solved example here](https://www.notion.so/saishubodh/From-linear-algebra-to-non-linear-weighted-least-squares-13cf17d318be4d45bb8577c4d3ea4a02#1de60a8465664d39a12af24353feef9e) from the [notes page](https://www.notion.so/saishubodh/Mobile-Robotics-2020-Students-Page-0b65a9c20edd4081978f4ffad917febb#a68cabac64754fa485144cc89b4b8c65). After understanding this, 

Coded it from scratch using `numpy` and try it out yourself for say different number of iterations with a certain tolerance for all 50 observations using Gradient Descent. Make the following plots using `matplotlib`:
   * Data and fit plot: Ground truth Gaussian, observations (points) & predicted Gaussian on the same plot.
   * Cost function ($\|r\|^2$) vs number of iterations   
   
Experiment with the hyperparameters and compile your observations in a table. Clearly mention your hyperparameters with justification.

You've used Gradient Descent above. Now implement Gauss-Newton and LM algorithms. To contrast between the three, you must experiment with 
   * Different initial estimate: Can a particular algorithm handle if the initial estimate is too far from GT?
   * Different number of observations: Can a particular algorithm handle very less observations?
   * Add [noise](https://numpy.org/doc/stable/reference/random/generated/numpy.random.normal.html) to your observations: Can a particular algorithm handle large noise?
   * What else can you think of? (For example, can an algorithm converge in less iterations compared to others?)
   
   
 ### Results
 
 |Algorithm | Learning rate          | Initialization         | No. of observations | Noise Factor    |Iterations to converge   |
| ------------- |:------------- |:-------------:| -------:| -------:|-------:|
| Gradient Descent| 0.01      | 10, 13, 19.12    | 50 |0| 1202  |
| Gradient Descent| 0.01      | 100, 50, 100    | 50 | 0| Does not converge |
| Gradient Descent| 0.02      | 10, 13, 19.12    | 50 | 0| 943 |
| Gradient Descent| 0.03      | 10, 13, 19.12    | 50 | 0|821  |
| Gradient Descent| 0.1      | 10, 13, 19.12    | 50 | 0|Does not converge  |
| Gradient Descent| 0.01      | 10, 13, 19.12    | 100 | 0| 845 |
| Gradient Descent| 0.01      | 10, 13, 19.12    | 25 | 0| > 4000  |
| Gradient Descent| 0.01      | 10, 13, 19.12    | 50 | 0.01| Error = 0.024   |
| Gradient Descent| 0.01      | 10, 13, 19.12    | 50 | 0.02|  Error = 0.009 |
| Gradient Descent| 0.01      | 10, 13, 19.12    | 50 | 0.1|  Error = 0.577  |

If we increase Learning rate by little : Performance Improves

If learning rate is increased too much : Fails to converge as when lr = 0.1

Explain your experimentations with justification here

|Algorithm | Initial Estimate      | No. of obseravtions    | Noise Factor  | No. of iterations to converge  |
| ------------- |:-------------:| -------:|-------:|-------:|
| Gauss Newton     | 10, 13, 19.12    | 50 | 0 |7|
| Gauss Newton      | 100, 50, 100     | 50 | 0 |Does not converge|
| Gauss Newton      | 10, 13, 19.12     | 100 | 0 |6|
| Gauss Newton      | 10, 13, 19.12      | 25 | 0 |6|
| Gauss Newton     | 10, 13, 19.12    | 50 | 0.01 |Error = 0.084|
| Gauss Newton     | 10, 13, 19.12    | 50 | 0.1 |Error = 3.923|

|Algorithm | Initial Estimate      | No. of obseravtions    | Lenda  | Noise Factor | No. of iterations to converge  |
| ------------- |:-------------:| -------:|-------:|-------:|-------:|
| Levenberg Marquardt      | 10, 13, 19.12      | 50 | 0.01 |0|7|
| Levenberg Marquardt      | 10, 13, 19.12      | 50 | 0.02 |0|7|
| Levenberg Marquardt      | 10, 13, 19.12      | 50 | 0.1 |0|8|
| Levenberg Marquardt      | 100, 50, 100       | 50 | 0.01 |0| 60 |
| Levenberg Marquardt      | 10, 13, 19.12      | 100 | 0.01 |0|6|
| Levenberg Marquardt      | 10, 13, 19.12      | 25 | 0.01 |0|7|
| Levenberg Marquardt      | 10, 13, 19.12      | 50 | 0.01 |0.01|Error = 0.045|
| Levenberg Marquardt      | 10, 13, 19.12      | 50 | 0.01 |0.1|Error = 2.414|


When the initialization is very far from original:

- Gradient Descend : Does not converge
- Gauss Newton : Performs worst, Does not converge
- Levenberg Marquardt : Converging slows down put still performs nicely

When the number of observations are increases: All three converge faster

When the number of observations are deacreased: 
- Gradient Descend Converges slower
- No observable effect on GN and LM

For Added Noise:
- Gradient descent : Converged better to real curve for high noise factor
- Gauss Newton : Not much effected my noise, converges efficiently
- Levemberg Marquardt : Least Effected by noise, converges to original curve best

Reason : As we add Regularisation term (lenda), LM prevents overfitting to the noise and converges to required curve.


## ICP Coding
Implement basic ICP algorithm with (given) known correspondences. 

Let X be your point cloud observed from the initial position. Your robot moved and observed P1 as your current point cloud. Same with P2 under a different transformation. Now you wish to apply ICP to recover transformation between (X & P1) and (X & P2). Use *root mean squared error (rmse)* as the error metric.


