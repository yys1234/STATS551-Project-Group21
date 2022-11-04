# STATS551-Project-Group21

1 Purpose of Data Analysis 

Airline flight prices fluctuate over time and as customers, we are interested in knowing when is
a good time to buy a cheaper flight ticket. Our project aims to forecast the flight prices given a
certain search and flight date as well as other parameters.

2 Description of Data 

Our data comes from Kaggle (https://www.kaggle.com/datasets/dilwong/flightprices). It
collects one-way flight data on Expedia between April 16, 2022, and October 05, 2022. We use a
subset of this dataset by fixing the starting (DTW) and destination (MIA) airport which is more
related to our UMich students’ travel plan. We also delete some useless and repeated variables. Af-
terward, we get 289413 samples with 15 columns which are: (1) the date when the entry was taken
from Expedia (2) the date of the flight (3) travel duration (4) number of elapsed days (5) whether
the ticket is for basic economy (6) whether the ticket is refundable (7) whether the flight is non-stop
(8) price of the ticket (9) number of remaining seats (10) total travel distance (11) departure time
(12) arrival time (13) airline name (14) type of airplane (15) cabin. The number of samples may
be further reduced by adding more limitations to the data of interest.

The potential defect in the data is that first, it did not mention if the dataset includes all
airlines or a subset of it. Second, it only covers flight data from April to October in a single year
which may prevent us from finding seasonal patterns. Third, it has missing values in two columns
(with 38142 and 375 missing values, respectively). Besides, the value of some columns is weird with
redundant expressions we need to spend lots of time cleaning it. If we were able to collect data, we
would elongate the collecting time. We would also include some other variables or improve current 
variables like switching the variable whether the flight is non-stop to the actual number of stops.

3 Plan of Project Timeline and Contribution 

Our planned timeline for the project is: (1) In the first and a half weeks (Nov 4 to Nov 14) we will
go on doing research on the Bayesian time series model because we three group members had no
experience in time series data analysis before. And we will clean the data and do EDA and feature
selection. (2) We will then spend a week (Nov 15 to Nov 22) writing code to realize our models
and look at the result. (3) Based on the result, we will modify the model if needed or explore other
Bayesian time series models and compare the result. This will take another week (Nov 23 to 30).
(4) Then we will draw our conclusion, start finishing our report and do a presentation recording
(Dec 1 to Dec 8).

Each group member will contribute in this way: (1) Each of us will do research on the Bayesian
time series model and read different papers. After that, we will have a meeting and make sure the
model we use next. (2) Zihan and Yushan will do data cleaning and EDA and then compare our
result to finalize the data for the model. Xingjian will prepare all equations and libraries needed
for the model and make a programming plan. (3) Xingjian and Yushan will write codes to realize
the model and Zihan will prepare all equations and libraries needed for the second model and
make a programming plan. (4) Zihan and Xingjian will write codes to modify the model or build
the second model. Yushan will improve the output quality from the first model and finalize the
EDA figures. (5) Xingjian will finish the rest of figures and tables. We three will start writing the
report. (6) We three will make presentation slides and record the presentation together. Besides,
we will meet once a week to ask questions and help others. We will also keep in touch through
messages if we have small questions to ask.

4 Plan of Data Analysis 

We identify two key challenges of the data analysis. The first one is the distribution shift. We
decide to split our dataset into a train set and a test set by time. In particular, the data from
the last 30 days will be selected for testing. The disjointedness in collection time implies that two
datasets may come from different distributions. Therefore, we need to carefully select priors that
are imposed on our models, and to avoid over-fitting. The second challenge is the settings of time
series prediction, where we cannot assume independence between each data point. The prediction
of a flight’s price should be based not only on its own features but also its historical data. This
fact invalidates many common models that rely on i.i.d. data.

We will apply feature selection methods and further simplify the number of predictors before
fitting. In our data analysis, we plan to try the Bayesian structural time series (BSTs) model first
due to the aforementioned challenge. Under a BST framework, the observed variable could be
expressed as (Local level model):
yt = μt + γt + βT xt + et, et ∼ N (0, σ2
e ) (1)
μt+1 = μt + νt, νt ∼ N (0, σ2
ν ) (2)
γt = −
S−1∑
s=1
γt−s + wt, wt ∼ N (0, σ2
t ) (3)
Let yt denote our time series flight price, xt denote a set of predictors of the interested time series,
μt be the local level (trend) term capturing the tendency of time series moving over time, and γt
be the seasonal term capturing association with periodic events. If this model does not work well,
we will then try to add an additional state component into the model (Local linear trend model).
We will set the spike and slab prior for each parameter and do data analysis with the help of bsts
library in R.



