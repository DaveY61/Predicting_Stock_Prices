# Predicting Stock Prices Using Machine Learning

## Summary
The purpose of this project is to predict stock prices for specific companies or a set of companies using historical stock data and related financial indicators. By leveraging machine learning techniques, particularly Long Short-Term Memory (LSTM) networks, we aim to provide investors with a tool to make informed decisions about buying or selling stocks. This project involves extracting, cleaning, and transforming historical stock data, training machine learning models, and developing an interactive application for users to predict stock prices for up to one year in advance.

## Functionality
### Long Short-Term Memory (LSTM) Networks
Long Short-Term Memory (LSTM) is a type of recurrent neural network (RNN) that is well-suited for sequence prediction problems. It is chosen for this project due to its ability to remember long-term dependencies and handle the vanishing gradient problem, which is crucial for predicting stock prices based on historical data. LSTMs have three types of gates (input, forget, and output) that regulate the flow of information, making them powerful for time series prediction.

### Financial Indicator(s)

In this project, the **closing price** was chosen as the only indicator for predicting stock prices using Long Short-Term Memory (LSTM) networks. The closing price is a key indicator that summarizes the market sentiment at the end of each trading day. Using LSTM networks, which are well-suited for sequence prediction due to their ability to remember long-term dependencies and handle the vanishing gradient problem, the closing price provides a focused and simplified approach for stock price prediction.

#### Pros:
- **Historical Trends**: Reflects the overall market sentiment and trend for the day.
- **Reduced Complexity**: Simplifies the model by using a single indicator, making it easier to train and understand.
- **Correlation**: Many other indicators are highly correlated with the closing price, so including them might not add significant value.
- **Avoids Overfitting**: Reduces the risk of overfitting by limiting the number of input features, ensuring the model generalizes better to new data.

#### Cons:
- **Lack of Context**: Does not capture intra-day price movements or trading volume.
- **Missing Insights**: Ignores other potentially valuable indicators such as trading volume and the day's high and low prices.
- **Potential for Improved Accuracy**: Other indicators might help capture more complex patterns, potentially improving the model's prediction accuracy.

In conclusion, the closing price was used exclusively due to several compelling reasons:

1. **Dominance in Technical Analysis**: The closing price is widely regarded as the most critical price in technical analysis because it represents the final consensus of the market for the trading day. Many technical trading strategies and indicators are based on closing prices, emphasizing its importance.

2. **Robustness in Trend Detection**: Historical trends and patterns in closing prices have been shown to be robust indicators of future price movements. Studies have demonstrated that closing prices tend to smooth out intra-day volatility, providing a clearer signal for long-term trend detection.

3. **Practicality and Proven Success**: Numerous successful financial models and strategies rely solely on closing prices. For instance, many moving average strategies, which are simple yet effective, use only the closing price to generate buy and sell signals.

4. **Computational Efficiency**: Using only the closing price reduces the computational complexity of the model. This is particularly important when training LSTM networks, as it allows for faster training times and requires less computational power, making the approach more feasible and efficient.

5. **Consistency and Reliability**: Closing prices are consistently available and reliable across different data sources, ensuring data quality and consistency. This reliability is crucial for building a dependable prediction model.

By focusing on the closing price, we ensure that the model is both effective and efficient, leveraging the most significant indicator in stock price analysis while avoiding unnecessary complexity and potential overfitting.

### Main Functions
1. **Data Extraction and Cleaning**
    - **Purpose**: Extract historical stock data from sources such as Yahoo Finance API, clean and transform the data for model training.
    - **Key Points**:
        - Merges data from multiple sources.
        - Converts column names to common terms for ease of understanding.
        - Displays data before and after cleaning for transparency.

2. **Model Training, Evaluation and Comparison**

    **JMari: LSTM Neural Network Model on Stock Data**
    - **Purpose**: Initialize, train, and evaluate LSTM models for predicting stock prices.
    - **Key Points**:
        - Utilizes LSTM's ability to handle sequential data for accurate predictions.
        - Demonstrates meaningful predictive power with at least 75% classification accuracy or 0.80 R-squared.
        - Documents the model optimization and evaluation process.
        - Displays overall model performance.
        
    **Antoine: XGBoost, SVG, and LR Model on Stock Data**

   **Leigh: Prophet Model on Stock Data**

    **Priscilla: XGBoost, SVG, and LR Model on Stock Data And Consumer Data**
    - **Purpose**: Data cleanup to merge the stock data with the survey of consumers data. The rationale behind retesting the stock data model with the inclusion of new consumer features is to determine if these additional variables enhance the predictive accuracy of stock prices.
      - Consumer Features: Index of Consumer Sentiment, Index of Consumer Expectations, Index of Current Condition, Probability of Adequate Retirement Income, Probability of Increase in Stock Market in Next Year, Current Value of Stock Market Investments.
    - **Models**:
       - Support Vector Regression: Performed best on Pfizer Stock Data with a low mean error score and a high R2 score of 0.90. Model performed adequately on AAPL and XOM stock with an accuracy of about 76%-80%. The model was underfit, with an accuracy score below 50% for 5/10 of the stocks tested. 
       - XGBoost: The XGBoost model results indicate an overfitting problem, as evidenced by the near-perfect R² values of 1.0 and extremely low Mean Squared Error (MSE) values for all stocks. I tried regularization Techniques by tuning parameters and using a different scaler. However, even when those techniques were applied to the model, the results were still overfit. Overall, the XGBoost model is not a good predictor of close value for the given stock data and date range. 
       - Linear Regression: The highest performing stocks were AAPL and MSFT with around 76% accuracy for both. Apart from APPL, MSFT, NVDA and XOM, the model performed poorly on all other stocks, incurring a negative R2 value for four out of ten stocks. In general, the linear regression did not accomplish an accuracy score over 77% for any stocks and it seems to have struggled with the given data.
    - **Conclusion**: In general, the SVR model generally performed better than the LR model and the XGBoost model, providing higher R² values and lower MSE across most stocks. This indicates that the SVR model is more effective at capturing the complex patterns in the stock and consumer data, making it a better choice for this dataset. However, the SVR model still has room for improvement and could benefit from further tuning of the SVR model parameters.


4. **Interactive Prediction App**
    - **Purpose**: Provide an interactive interface for users to input specific dates and parameters to see predicted stock prices.
    - **Key Points**:
        - Allows predictions for any given stock for up to 1 year in advance.
        - Enhances user experience by making predictions easily accessible.
        - Saves predictions for future reference.

5. **Saving Models**
    - **Purpose**: Save the trained LSTM model to disk.
    - **Key Points**:
        - Ensures the model can be reused without retraining.
        - Facilitates deployment and scalability.
        - Vital for maintaining model consistency across different runs and users.

6. **Saving Scalers**
    - **Purpose**: Save the data scalers used during preprocessing.
    - **Key Points**:
        - Maintains the same scaling factors for future predictions.
        - Ensures consistency in data transformation.
        - Vital for accurate predictions, as differences in scaling can lead to significant errors.

## Data Sources
- **Yahoo Finance API**: Supplies historical stock data and additional financial indicators.
- **Survey of Consumers**: The Surveys are conducted at the University of Michigan. Founded in 1946, the surveys have long stressed the important influence of consumer spending and saving decisions in determining the course of the national economy. 


## Individual Functions

### `main.ipynb`

1. **extract_data()**
    - **What it is**: Function to extract historical stock data from Yahoo Finance.
    - **Why it is in the code**: Essential for obtaining the raw data needed for training the LSTM model.
    - **Additional Point**: Handles API requests and data formatting.

2. **clean_data()**
    - **What it is**: Function to clean and preprocess the extracted stock data.
    - **Why it is in the code**: Ensures data quality and consistency for accurate model training.
    - **Additional Point**: Converts column names to user-friendly terms and handles missing values.

3. **transform_data()**
    - **What it is**: Function to transform the cleaned data into a format suitable for LSTM model training.
    - **Why it is in the code**: Prepares data by scaling and reshaping it for time series analysis.
    - **Additional Point**: Splits data into training and testing sets.

4. **initialize_model()**
    - **What it is**: Function to initialize the LSTM model with specified parameters.
    - **Why it is in the code**: Sets up the model architecture for training.
    - **Additional Point**: Defines the layers and configurations of the LSTM network.

5. **train_model()**
    - **What it is**: Function to train the LSTM model on the prepared data.
    - **Why it is in the code**: Crucial for developing the predictive capabilities of the model.
    - **Additional Point**: Tracks model performance metrics during training.

6. **evaluate_model()**
    - **What it is**: Function to evaluate the performance of the trained LSTM model.
    - **Why it is in the code**: Measures the accuracy and reliability of the model's predictions.
    - **Additional Point**: Generates performance reports and visualizations.

7. **save_model()**
    - **What it is**: Function to save the trained LSTM model to disk.
    - **Why it is in the code**: Allows reuse of the model without retraining, saving time and computational resources.
    - **Additional Point**: Facilitates deployment and sharing of the model.

8. **save_scaler()**
    - **What it is**: Function to save the data scalers used during preprocessing.
    - **Why it is in the code**: Ensures consistency in data scaling for future predictions.
    - **Additional Point**: Critical for maintaining prediction accuracy, as different scalings can lead to errors.

### `stock_price_prediction_app.py`
This script focuses on creating an interactive application for predicting future stock prices. It uses several key functions to load the pre-trained LSTM model, make predictions based on user inputs, and visualize the predicted stock prices. The application enhances user experience by providing an easy-to-use interface and clear visual representations of the predictions.

The script starts by loading the pre-trained LSTM model using the `load_model()` function, ensuring that the model is ready for making predictions. The `predict_stock_prices()` function takes user inputs, such as the stock ticker and the desired prediction date range, and uses the LSTM model to generate future stock price predictions. These predictions are then plotted alongside historical data using the `plot_predictions()` function, providing a visual comparison that helps users understand the trends and forecasts. Finally, the `run_app()` function initializes and runs the interactive application, handling user inputs and displaying the predictions.

### Streamlit
Streamlit is a powerful and easy-to-use framework for building interactive web applications with Python. It was chosen for this project because it allows for rapid development and deployment of data-driven applications. Streamlit's simplicity in turning data scripts into shareable web apps without requiring extensive knowledge of web development makes it ideal for this project.

- **Benefits**: Streamlit simplifies the creation of interactive and user-friendly applications, making it easy to visualize data and predictions. It supports rapid prototyping and deployment, which is crucial for iterative development.
- **Additional Points**:
    - **Integration**: Streamlit seamlessly integrates with Python, allowing for direct use of Python functions and libraries.
    - **Customization**: Provides various widgets and customization options to enhance user interaction.
    - **Community Support**: A large and active community provides a wealth of resources, tutorials, and extensions to enhance functionality.

### Individual Functions

1. **load_model()**
    - **What it is**: Function to load the pre-trained LSTM model.
    - **Why it is in the code**: Enables the app to use the trained model for making predictions.
    - **Additional Point**: Handles model serialization and deserialization.

2. **predict_stock_prices()**
    - **What it is**: Function to predict future stock prices based on user inputs.
    - **Why it is in the code**: Provides the core functionality of the interactive app.
    - **Additional Point**: Utilizes the LSTM model to generate predictions for up to one year in advance.

3. **plot_predictions()**
    - **What it is**: Function to plot the predicted stock prices along with historical data.
    - **Why it is in the code**: Visualizes the predictions for better user understanding.
    - **Additional Point**: Enhances the user interface by providing clear and informative charts.

4. **run_app()**
    - **What it is**: Function to run the interactive stock price prediction app.
    - **Why it is in the code**: Initializes and launches the app for user interaction.
    - **Additional Point**: Handles user inputs and displays predictions in a user-friendly manner.

## Project Findings
### Pros
- **High Predictive Power**: The LSTM models demonstrated high accuracy in predicting stock prices.
- **User-Friendly Application**: The interactive app allows users to easily access predictions.
- **Comprehensive Data Handling**: The project handles data extraction, cleaning, and merging from multiple sources efficiently.

### Cons
- **Data Quality**: The accuracy of predictions is highly dependent on the quality of the input data.
- **Model Complexity**: LSTM networks are complex and require significant computational resources for training.

### Initial Perceptions and Findings
- **Effectiveness of LSTM**: LSTM networks proved effective in capturing the temporal dependencies in stock price data, resulting in accurate predictions.
- **Data Integration**: Merging data from multiple sources enhanced the robustness of the dataset, leading to better model performance.
- **User Engagement**: The interactive app was well-received, making it easier for users to explore stock price predictions.

## Real-World Application
This stock price prediction tool can be utilized by various professionals in the finance and investment sectors. Financial analysts can use the tool to forecast stock trends and provide insights to their clients. Portfolio managers can leverage the predictions to optimize their investment strategies and balance risks. Individual investors can use the app to make informed decisions about buying or selling stocks based on predicted future prices. Additionally, the tool can be beneficial for academic researchers studying market behavior and testing new financial theories. Overall, this project aims to enhance decision-making processes and contribute to more strategic investment planning.

## Instructions for Running the Code
1. **Data Extraction and Cleaning**: Run the `main.ipynb` notebook to extract, clean, and transform the data.
2. **Model Training and Evaluation**: Execute the Python script provided to train and evaluate the LSTM models.
3. **Interactive Prediction App**: Use the `stock_price_prediction_app.py` to launch the interactive app for making stock price predictions.

### Additional Notes
- Ensure all necessary libraries are installed before running the scripts.
- Configure API keys for data extraction from Yahoo Finance.
- Follow the detailed comments and pseudocode in the provided scripts for further understanding and customization.

By following these instructions and utilizing the provided code, users can effectively predict stock prices and make informed investment decisions based on historical data and advanced machine learning techniques.
