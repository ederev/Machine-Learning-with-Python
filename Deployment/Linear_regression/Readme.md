## How to serve a linear regression model on a web API using Flask and Gunicorn
#### Run the training script,

**`$ python training_housing.py`**

This would do the following,
* Read the dataset from the `/data/USA_housing.csv`
* Train the linear regression model
* Save the model in a serialized format in the `/models/` folder
* Save the test dataset (sampled from the full dataset) in the `/data/housing_test.csv` file

#### Fire up the gunicorn server by running,

**`$ gunicorn --bind 0.0.0.0:5000 server_lm:app`**

This will start the HTTP server interface and run an `/predict` API endpoint.<br>
The exact address of this API is `http://0.0.0.0:5000/predict`.<br>
We can take advantage of this endpoint by passing data to it in JSON format. To accomplish this, run,

**`$ python request_pred.py`**

This should print the predicted values on your terminal.

#### Note 
For demo purpose, only 6 data points are passed on to the prediction server. **If you want to get preditcions for more points, simply edit the index in the following code segment in the `request_pred.py`.**

```
# Read test dataset
test_df = pd.read_csv("data/housing_test.csv")
# For demo purpose, only 6 data points are passed on to the prediction server endpoint.
# Feel free to change this index or use the whole test dataset
test_df = test_df.iloc[40:46]
```