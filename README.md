# OLS
Math 540 Statistical Learning Ordinary Least Squares project 
## There are 3 different codes with the the names "REALDATA", "RandomDataDeltaFixed", "deltaNotFIXED"
## REALDATA
Code was written in order to check the error bound and real error of OLS on real data.<br />
`from sklearn.datasets import load_diabetes` was used in order to use dataset Diabetes which consists of 10 features and 442 samples.<br />
`m = ` you can assign value in a range [10,400], to the training sample size by simply putting needed number to the equation `m = ` <br />
`d =` you can assign value in a range [1,10], to the training sample's number of features by putting needed number to the equation `d = `<br />
`delta=0.01` confidence parameter is fixed for this code (the value 0.01 was chosen in order to have approximately 100 percent probability of error bound formula working), because this code is written in order to check  error bound in a cases when d is fixed m is not, m is fxed d is not. So DO NOT CHANGE the value of delta <br />
Number of datapoints for test sample is fixed (Last 42 datapoints are used as an test sample) <br /> 
`x_test=diabetes.data[-42:,-d:]` <br />
`y_test=diabetes.target[-42:]`<br />
Train sample is fully determined by the assigned values for m and d.
`x_train=diabetes.data[:m,-d:]`<br />
`y_train=diabetes.target[:m]`<br />
Having assigned the values for m and d you can compile the code.<br />
After pressing the compile button the code will give the Coefficients of the regression, Mean squared error which is equal to Real error RH, Loss function bound M, Empirical risk RS, Error bound, and difference between Error bound and Real error.<br />
## RandomDataDeltaFixed
Code was written in order to check the error bound and real error of OLS on randomly generated data.<br />
`m = ` you can assign value in a range [10,400], to the training sample size by simply putting needed number to the equation `m = ` <br />
`d =` you can assign value in a range [1,10], to the training sample's number of features by putting needed number to the equation `d = `<br />
`delta=0.01` confidence parameter is fixed for this code (the value 0.01 was chosen in order to have approximately 100 percent probability of error bound formula working), because this code is written in order to check  error bound in cases when d is fixed m is not, m is fixed d is not. So DO NOT CHANGE the value of delta <br />
Sample data was generated using `x,y, coef=datasets.make_regression(n_samples=442, n_features=10, n_informative=10, noise=10, coef=True, random_state=0)`, with the number of datapoints equal to 442, number of features equal to 10 (all are informative), noise equal to 10, and `random_state=0` which means that the same dataset will be generated across multiple function calls <br />
Data is scaled by using `x=np.interp(x,(x.min(),x.max()), (0,50))` and `y=np.interp(y, (y.min(), y.max()),(1000,2000))` <br />
Sizes of Training sample and Test sample are determined as in the previous code <br />
Having assigned the values for m and d you can compile the code.<br />
After pressing the compile button the code will give the Coefficients of the regression, Mean squared error which is equal to Real error RH, Loss function bound M, Empirical risk RS, Error bound, and difference between Error bound and Real error.<br />
## deltaNotFIXED
This code was written in order to check the probability of Error Bound Formula working given the random data with fixed dimensionality and number of samples by varying the confidence parameter delta .<br />
`m=17`, `d=2` training sample size and dimensionality are fixed with this values (values were given not so small and not so big because compilation time is long) .<br />
Dataset is generated using `x,y, coef=datasets.make_regression(n_samples=20, n_features=2, n_informative=2, noise=10, coef=True)`(20 samples, 2 features, all features are informative, noise =10, random_state=NONE which guarantess that every time the function is called different dataset will be generated) .<br />
Number of datapoints for test sample is fixed (Last 3 datapoints are used as an test sample) <br /> 
`x_test=x[-3:,-d:]` <br />
`y_test=y[-3:]`<br />
Train sample is fully determined by the assigned values for m and d.
`x_train=x[:m,-d:]`<br />
`y_train=y[:m]`<br />
The code will be generating different datasets and for each dataset it will check the sign of difference between Error bound and Real Error. It will put 1 in the new array if the difference is positive and -1 otherwise. Then it will derive the number of all 1's in the array and will divide it by length of an array (in our case 1000). This number is probability of error bound working tested on 1000 different datasets.  <br />
  `for k in range(0,1000):.......` <br />
    `TEST=ErrorBound-RH;`<br />
    `if (TEST>=0):`<br />
      `LST[k]=1;`<br />
    `else:`<br />
      `LST[k]=-1;`<br />
   `PN=0;`<br />
   `for o in range(0,1000):`<br />
     `if (LST[o]>=0):`<br />
       `PN=PN+1;`<br />
   `Probability=PN/len(LST);`<br />
However It will not guarantee the good accuracy so for each delta another 1000 probabilities derived and their mean is used as an final value for probability of error bound formula working. In total function is called 1000000 times. <br />
Assigned the value for delta the code will compile about 14 minutes and give the probability.
## License 
[MIT]
(https://choosealicense.com/licenses/mit/)
