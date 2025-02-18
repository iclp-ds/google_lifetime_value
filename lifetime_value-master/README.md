# Lifetime Value

Accurate predictions of customers’ lifetime value (LTV) given their attributes
and past purchase behavior enables a more customer-centric marketing strategy.
One challenge of LTV modeling is that some customers never come back, and the
distribution of LTV can be heavy-tailed. The commonly used mean squared error
(MSE) loss does not accommodate the significant fraction of zero value LTV from
one-time purchasers and can be sensitive to extreme large LTV from top spenders.

We model the distribution of LTV given associated features as a mixture of zero
point mass and lognormal distribution, which we refer to as zero-inflated
lognormal (ZILN) distribution. This modeling approach enables us to capture the
churn probability and account for heavy-tailedness nature of LTV at the same
time, and also allows for easy uncertainty quantification of the point
prediction. The proposed loss function can be used in both linear models and
deep neural networks (DNN). We also advocate normalized Gini coefficients to
quantify model discrimination and promote decile charts to assess model
calibration.

The proposed loss function (implemented in Keras) and evaluation metrics are
integrated into a python package. And we demonstrate the predictive performance
of our proposed model in notebooks on two real-world public datasets.

## Paper

Wang, Xiaojing, Liu, Tianqi, and Miao, Jingang. (2019).
A Deep Probabilistic Model for Customer Lifetime Value Prediction.
[*arXiv:1912.07753*](https://arxiv.org/abs/1912.07753).

## Installation

The easiest way is propably using pip:

```
pip install -q git+https://github.com/google/lifetime_value
```

If you are using a machine without admin rights, you can do:

```
pip install -q git+https://github.com/google/lifetime_value --user
```

If you are using [Google Colab](https://colab.research.google.com/), just add
"!" to the beginning:

```
!pip install -q git+https://github.com/google/lifetime_value
```

Package works for python 3 only.

## Usage
Package can be imported as

```python
import lifetime_value as ltv
```

## notebooks
The best way to learn how to use the package is probably by following one of the
notebooks, and the recommended way of opening them is Google Colab.

### [Kaggle Acquire Valued Shoppers Challenge Dataset](https://www.kaggle.com/c/acquire-valued-shoppers-challenge/data)

This Kaggle challenge provides almost 350 million rows of completely anonymised
transactional data from over 300,000 shoppers. We use the transactional data to
demonstrate LTV modeling.

We download the transaction.csv (21GB) file from Kaggle server and prepare csv
files for each of top 20 most common companies. Then we train a Keras model to
predict customer's lifetime value and returning probability.

The raw data is available [here](https://www.kaggle.com/c/acquire-valued-shoppers-challenge/data).

*   [Data preparation](./notebooks/kaggle_acquire_valued_shoppers_challenge/preprocess_data.ipynb)
downloads kaggle data transaction.csv and preprocesses the top 20 most common
companies' data to customer-level one. This is optional, and running this will
save time for regression and classification because the data are cached.
*   [Regression](./notebooks/kaggle_acquire_valued_shoppers_challenge/regression.ipynb)
trains a Keras regression linear/dnn model with specified loss function and
evaluates the results.
*   [Classification](./notebooks/kaggle_acquire_valued_shoppers_challenge/classification.ipynb)
trains a Keras classification linear/dnn model with specified loss function and
evaluates the results.

### [KDD Cup 98](https://kdd.ics.uci.edu/databases/kddcup98/kddcup98.html)

The Second International Knowledge Discovery and Data Mining Tools Competition
(a.k.a., the KDD Cup 1998) provides a dataset collected by Paralyzed Veterans of
America (PVA), a non-profit organization that provides programs and services for
US veterans with spinal cord injuries or disease. The organization raised money
via direct mailing campaigns and was interested in lapsed donors: people who
have stopped donating for at least 12 months. The provided dataset contains
around 200K such donors who received the 1997 mailing and did not make a
donation in the previous 12 months. We tackle the same task of the competition,
which is to predict the donation dollar value to the 1997 mailing campaign.

The raw data is available [here](https://kdd.ics.uci.edu/databases/kddcup98/kddcup98.html).


*   [Regression](./notebooks/kdd_cup_98/regression.ipynb) trains regression models and
makes comparisons on different methods.

## People
Package is created and maintained by Xiaojing Wang, Tianqi Liu, and Jingang
Miao.
