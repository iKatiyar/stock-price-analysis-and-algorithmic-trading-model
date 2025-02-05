📈 Stacked LSTM Stock Price Prediction with Mock Trading Environment

This project demonstrates the development and training of a stacked Long Short-Term Memory (LSTM) model for predicting stock prices using historical data. Additionally, a mock trading environment is included to simulate buy/sell decisions based on the predicted prices, helping to evaluate potential trading strategies.

Table of Contents

	•	Installation
	•	Project Structure
	•	Data Collection
	•	Function Explanations
	•	Model Training
	•	Mock Trading Environment
	•	Running the Code
	•	Results
	•	License

Installation

To run this project, you will need to install the required Python packages:
pip install numpy pandas scikit-learn tensorflow matplotlib yfinance pandas-datareader seaborn

Project Structure;
- StackedLSTM.ipynb         # Jupyter Notebook containing the full code and workflow
- README.md                 # This README file
- AAPL_daily.csv            # Example dataset (Apple stock data)

Data Collection
Stock price data is fetched from the Yahoo Finance API using the yfinance package. You can modify the code to collect data for any stock symbol by changing the ticker.
Example Code to Fetch Data:
# Example to fetch Apple (AAPL) stock data from June 1, 2004
stock_data = prepare_ticker_data("AAPL", start_date="2004-06-01")
stock_data.to_csv("AAPL_daily.csv", index=False)

Function Explanations

Here is a breakdown of the key functions used in this project:

1. get_ticker_data(ticker_code: str, start_date=None, end_date=datetime.today())

	•	Fetches stock data using the Yahoo Finance API, based on the ticker symbol and date range.

2. clean_ticker_data(df)

	•	Cleans the data by resetting the index, renaming columns, and converting the date to a proper datetime format.

3. resample(df)

	•	Resamples the time-series data to daily frequency, filling any missing days.

4. basic_preprocess(df)

	•	Interpolates missing values and fills data gaps. The data is cast into float type for easier processing.

5. prepare_ticker_data(ticker_code: str, start_date=None, end_date=datetime.today())

	•	A utility function to fetch, clean, resample, and preprocess the stock data in one step.

Model Training

The LSTM model is built using TensorFlow’s Keras API. Here’s an overview of the model and training process:

Key Steps:

	1.	Data Normalization: The stock data is scaled between 0 and 1 using MinMaxScaler for better performance.
	2.	Splitting Data: The dataset is split into training and testing sets.
	3.	Model Definition: The model is a stacked LSTM with multiple layers followed by a Dense layer for output.
	4.	Callbacks: Early stopping and learning rate reduction are used to optimize training performance.
	5.	Evaluation: The model is evaluated using Mean Squared Error (MSE) and other metrics to compare predicted prices with actual prices.

Mock Trading Environment

This project includes a mock trading environment to simulate trading based on the predicted stock prices. The strategy assumes that:

	•	Buy when the predicted price is higher than the previous actual price.
	•	Sell when the predicted price is lower than the previous actual price.

Key Steps:

	1.	Buy Condition: Purchase stock if the predicted price is higher than the current price.
	2.	Sell Condition: Sell stock if the predicted price is lower than the current price.
	3.	Profit Calculation: Keep track of your capital and owned stocks to calculate total profit.

Results

After running the notebook:

	•	You will have a trained LSTM model that predicts future stock prices.
	•	A plot comparing actual vs predicted prices will be displayed.
	•	The mock trading environment will provide simulated results, showing how profitable the predictions would have been.

License

This project is licensed under the MIT License. See the LICENSE file for more details.

This README is structured to guide users through installation, running the code, and understanding the project. You can customize the explanations or add more sections if needed before pushing it to your GitHub repo.
