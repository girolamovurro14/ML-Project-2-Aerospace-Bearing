# Aerospace Bearing - Machine Learning (CS-433)
The repository contains all the material used to carry out the Machine Learning (CS-433) Project 2 and it is organized as follows:
 - useful documentation and references consulted during the project (`documentation` folder)
 - the code needed to implement linear regression on the aerodynamic force (`linear regression` folder)
 - the code needed to implement a Fully Connected Forward Neural Network on the aerodynamic force (`fnn` folder)
 - the code needed to implement a Convolutional Neural Network on the aerodynamic force (`cnn` folder)
 
# Team
This project is executed by the team GiFT with the following members:

Girolamo Vurro: [@girolamovurro14](https://github.com/girolamovurro14)

Francesca Venturi: [@francescaventurigit](https://github.com/francescaventurigit)

Tommaso Farnararo: @tommasofarnararo

It is supervised by the Post-doc Dimitri Maurice Goutaudier and the PhD students Matteo Raviola and Andrea Zanoni, from the Scientific Computing and Uncertainty Quantification (CSQI) Laboratory, led by Professor Fabio Nobile.


# Project structure

## Presentation
The dataset we work on is made up of 500 trajectories of the center of gravity of a rotor held by two aerospace bearings, where the aerodynamic force is applied, and every trajectory is characterized by 2001 time instants, whose temporal distance is uniform. These data are represented by means of two 500x2001 matrices, i.e. the X-coordinates and Y-coordinates (`X.csv` and `Y.csv`) and are used to predict the corresponding aerodynamic force along x-direction and y-direction (`FX.csv` and `FY.csv`), equally represented as matrices 500x2001. The project aims at studying the memory effect of the problem, namely looking for an optimal delay parameter, which is the amount of previous time steps to consider while predicting the forces at a given time step. This goal is achieved by implementing different regression tecniques.

## Documentation
The documentation has been provided by the supervisors of the project, after a superficial, but still straightforward, explanation of the physical structure we deal with: the Aerospace Bearing. All the references are in the `documentation` folder.

## Linear Regression
The preliminary part of the project consist of performing linear regression to predict the forces. As expected, this model results in being too simple to catch the non-linear trend of both the trajectory and the forces. In particular, two different models are implemented: they are respectively `main_autoreg_true.py` and `main_dist_rot.py`. 

## Forward Neural Network
As expected, Neural Networks represent the optimal task to hit the target, being able to catch the non-linearity and periodic behaviour of the physical system they analyse. Three different Fully Connected Forward Neural Network (`fnn` folder) are therefore implemented: `FNN_coord_single.ipynb`, `FNN_predicted_single.ipynb` and `FNN_true_single.ipynb`, differing in the data they take as input.

## Convolutional Neural Network
Having to deal with times series, also Convolutional Neural Networks (`cnn` folder) may be a good fit. In particular, a 1D-convolution is suitable for encoding the time dependency of data. Similarly to FNN, three different networks are implemented: `CNN_coord_single.ipynb`, `CNN_predicted_single.ipynb` and `CNN_true_single.ipynb`, again differing in the data plugged as input.

## Tuning of the Parameters
As a consequence of some preliminary attempts, the 'coordinates' model ends up being the most appropriate according to the target, so a grid search on the hyper parameters of the model is performed both for the FNN and CNN model to choose the ones minimizing the test loss (`FNN_coord_tuning.ipynb` and `CNN_coord_tuning.ipynb`).

## Delay Parameter and Elbow Curve
Finally, once all the hyper-parameters are fixed, the optimal delay parameter is chosen as the best trade-off between computational burden and accuracy. In particular, this is obtained plotting the test-loss over the delay parameter and selecting the one corresponding to the elbow of the curve.

## Envirnment
The project is developed and tested with `python3.8.10`. The required library for running the models and training is `numpy` and `pytorch`. The library for visualization are `maptplotlib` and `seaborn`. As regards the linear regression the Python IDE used is `Spyder`, while for neural networks (both forward and convolutional) JupyterLab is more appropriate.

## Results
The results obtained are quite satisfying, reaching a test error of the order of 10^-5 and a delay parameter d=50.
