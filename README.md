📈 Stacked LSTM Stock Price Prediction with Mock Trading Environment

This project demonstrates the development of a stacked Long Short-Term Memory (LSTM) model for predicting stock prices using historical data. Additionally, it includes a mock trading environment to simulate buy/sell decisions based on the model's predictions, helping to evaluate potential trading strategies.

📌 Table of Contents

	•	Installation
	•	Project Structure
	•	Data Collection
	•	Function Explanations
	•	Model Training
	•	Mock Trading Environment
	•	Running the Code
	•	Results
	•	License

⚙️ Installation

To run this project, you will need to install the required Python packages:
pip install numpy pandas scikit-learn tensorflow matplotlib yfinance pandas-datareader seaborn

📂 Project Structure

	├── StackedLSTM.ipynb      # Jupyter Notebook with the full workflow  
	├── README.md              # Project documentation  
	├── AAPL_daily.csv         # Example dataset (Apple stock data)  

📊 Data Collection

Stock price data is fetched from Yahoo Finance using the yfinance package. You can modify the code to collect data for any stock symbol by changing the ticker.

Example Code to Fetch Data:

	# Example to fetch Apple (AAPL) stock data from June 1, 2004
	from datetime import datetime
	stock_data = prepare_ticker_data("AAPL", start_date="2004-06-01")
	stock_data.to_csv("AAPL_daily.csv", index=False)


🔍 Key Functions

This project includes several helper functions to process stock data:

1. get_ticker_data(ticker_code: str, start_date=None, end_date=datetime.today())

	•	Fetches stock data using the Yahoo Finance API for a given stock ticker and date range.

2. clean_ticker_data(df)

	•	Cleans and preprocesses stock data (e.g., renaming columns, converting date format).
3. resample(df)

	•	Resamples time-series data to daily frequency and fills any missing days.

4. basic_preprocess(df)

	•	Interpolates missing values and converts the dataset into a float-compatible format.

5. prepare_ticker_data(ticker_code: str, start_date=None, end_date=datetime.today())

	•	A pipeline function that combines fetching, cleaning, resampling, and preprocessing in one step.

🧠 Model Training

The stacked LSTM model is built using TensorFlow’s Keras API.

🔑 Key Steps:

	1.	Data Normalization: The stock prices are scaled between 0 and 1 using MinMaxScaler for better model performance.
	2.	Data Splitting: The dataset is divided into training and testing sets.
	3.	Model Definition: 
 			• A stacked LSTM architecture with multiple layers.
    			• A Dense output layer for predicting the next day's stock price.
	4.	Training Optimization:
			• Early stopping prevents overfitting.
    			• Learning rate reduction improves convergence.
	5.	Evaluation: The model is evaluated using Mean Squared Error (MSE) and other relevant metrics.

 
💰 Mock Trading Environment

A mock trading simulation is implemented to assess the model’s predictions.

💹 Trading Strategy

	•	Buy when the predicted price is higher than the previous actual price.
	•	Sell when the predicted price is lower than the previous actual price.

🔑 Key Steps:

	1.	Buying Condition: Purchase stock if the predicted price is higher than the actual price.
	2.	Selling Condition: Sell stock if the predicted price is lower than the actual price.
	3.	Profit Calculation: Track capital and owned stocks to compute total returns.
 
🚀 Running the Code

1.	Clone the repository:

		git clone https://github.com/yourusername/stacked-lstm-stock-prediction.git
		cd stacked-lstm-stock-prediction

2.	Run the Jupyter Notebook (StackedLSTM.ipynb) step by step.


📊 Results

After executing the notebook:

✅ A trained LSTM model capable of predicting future stock prices will be created.
✅ A visualization comparing actual vs predicted stock prices will be displayed.
✅ The mock trading simulation will provide insights into the profitability of using LSTM predictions for trading.

📜 License

This project is licensed under the MIT License. See the LICENSE file for more details.
