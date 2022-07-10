# Melbourne-City

This project aims to assist the City of Melbourne council's decisions to encourage
Melbournians to adopt measures that facilitate reduction of carbon content within the city,
organize events within the city to improve the financial status of the businesses affected
due to COVID-19, manage the energy consumption levels and invest in renewable energy.
The council is committed to investing in infrastructure and contribute towards the next zero
emissions. In 2021, Australia’s Technology Investment Roadmap is expected to invest $18
billion of Government investment over the next 10 years and for low emissions technologies
drive at least $70 billion of total new investment in Australia by 2030.

Our sub team was responsible for delivering two statistical model for Melbourne city
pedestrian count prediction capability services. A regression model and a time series model
were provided for integration into two features of the website.

The dataset for training both types of models were obtained using the same approach.
Firstly using this notebook, the pedestrian count for the city of Melbourne for various
sensor locations were downloaded using API endpoints from the council. The hourly
pedestrian counts obtained were then aggregated to daily counts. Now, to train statistical
models, we need to create features for these regression outputs. Weather data from
Bureau of Meteorology were used as features. Moreover, the COVID-19 restriction and the
holiday variables were also integrated. Both these features were binary in nature. For the
initial stages, Aparna Chintala was responsible for manually obtaining the data from various
sources and then merging them.

Because the regression model in the prior trimester didn’t yield desired results, Rohan
Amatya was responsible for identifying ways of improving the data pre-processing process,
modelling process, evaluating various approaches in terms of test performance, and
automating the whole ETL (Extract Transform Load) forecasting pipeline.

Firstly, in terms of pre-processing, all the data were normalized(standardized). This ensured
that the models were easier to train and resulted in faster convergence. Since time-series
modelling was also added this trimester for dedicated automated pedestrian forecasting on
a periodic basis, the pre-processing for this modelling process involved additional steps.
Feature engineering was carried out as implemented in this notebook to ensure that the
data was transformed in a format suitable for time series modelling.

Now, multiple types of statistical regressors were trained and evaluated for both types of
problems. For regression problem which was carried out by Miriam Zhu and Akhila Manchi,
ticket shows that the RandomForest Regressor yielded the smallest test error. The
scaler(pre-processing) and the trained model obtained from this evaluation was integrated
into the website resource to obtain the on-demand pedestrian count predictions capability.

Similarly, for the time-series forecasting, multiple models were trained and evaluated.
VAR(Vector Autoregression), RNN(Recurrent Neural Network), GRU(Gated Recurrent Unit),
LSTM(Long Short-Term Memory) and Stacked LSTM were evaluated by Rohan Amatya. EDA
(Exploratory Data Analysis) was also carried out to understand the data, perform
imputations, aggregate information, and perform stationarity checks. This ticket and
notebooks 1, 2 can be viewed for reference. Here, windowing technique was used for
feature engineering. Since the dataset was 2 weeks late and we were tasked with providing
prediction of at least 1 week from the current date, we needed to predict for 3 weeks in
reality. This prediction of 3 weeks has been brought down from the considerable timeframe
of 6 months as done in the prior trimester based on advice from Rohan where he
mentioned that predictions would be more uncertain as the time difference increased.

Finally, the single-step multivariate time series forecasting was converted to multi-step to
incorporate the mentioned changes. This web resource shows the customer-facing exposure
of the feature implemented. For the integration of both the features into the website,
Ayodeji Ladeinde aided the respective sub-team members.

Now, most projects would consider data collection and prediction as a one-time process.
However, to add value to the client we automated the whole ETL prediction pipeline, which
would periodically refresh the dashboard. This was envisioned, planned, and implemented
by Rohan. Here, a complete end-to-end cloud solution was used to automate the pipeline in
order to make the process robust and at the same time reduce cost as much as possible.
The data collection and the model training are an expensive process. For manual training,
Google Colab was used which provided computation resources and GPUs. However, when
using dedicated servers of similar configurations, these would yield high cost. So, in order to
automate the pipeline and reduce the server cost, the automatic ETL pipeline was
implemented using AWS services.

A lambda function is used to start the resource-intensive server in the stipulated time in a
periodically in order to perform the automation. The lambda function is triggered by a cloud
watch event rule for the cron job. The entire ETL implementation is provided here, which is
to be deployed over the server. Please note that in order to use these resources, some
knowledge regarding AWS cloud services such as lambda, EC2, cloudwatch, log groups, IAM
is required.

