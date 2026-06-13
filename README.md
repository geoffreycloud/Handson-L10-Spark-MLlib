# Handson-L10-Spark-Streaming-MachineLearning-MLlib
This project demonstrates a real-time data processing and machine learning pipeline using **Apache Spark Structured Streaming** and **Spark MLlib**. 

---

## Technologies Used

- Apache Spark Structured Streaming
- Spark SQL
- Spark MLlib
- Python (Faker, Socket)
- Linear Regression Model

---

## Task 4: Real-Time Fare Prediction Using MLlib

### Objective
Train a regression model to predict `fare_amount` based on `distance_km`, then apply it to streaming data to detect deviations.

#### 1. Offline Model Training
- Loaded historical dataset (`training-dataset.csv`)
- Converted features to numeric format
- Used `VectorAssembler` to create feature vector
- Trained `LinearRegression` model using:
  - Feature: `distance_km`
  - Label: `fare_amount`
- Saved trained model locally


#### 2. Streaming Inference
- Ingested real-time ride data via socket stream
- Parsed JSON into structured DataFrame
- Transformed incoming data using same feature pipeline
- Applied trained model to predict fare
- Calculated deviation: deviation = |actual_fare - predicted_fare|

### Output

<img width="1303" height="420" alt="Screenshot 2026-06-12 155407" src="https://github.com/user-attachments/assets/32deb62c-fd44-47b5-9947-4c4c2b3c4b8c" />

--- 
## Task 5: Time-Based Fare Trend Prediction

### Objective
Build a regression model to predict average fare trends using windowed aggregations and time-based features.

#### 1. Offline Training
- Loaded historical dataset
- Converted timestamp to `event_time`
- Applied 5-minute window aggregation: avg(fare_amount)
- Extracted time features:
  - hour_of_day
  - minute_of_hour
- Trained Linear Regression model on time features
- Saved model for reuse

#### 2. Streaming Inference
- Ingested real-time stream
- Applied same 5-minute sliding window (sliding by 1 minute)
- Computed real-time average fare per window
- Extracted time-based features
- Applied trained model for prediction

### Output
<img width="1170" height="210" alt="Screenshot 2026-06-12 165432" src="https://github.com/user-attachments/assets/d95ea67f-b7b1-4b90-baec-fcafaf8f5695" />

---

## Key Learnings

- How Structured Streaming processes real-time data
- Importance of schema consistency between batch and stream
- Window-based aggregations for time-series analysis
- Feature engineering for machine learning models
- Integration of Spark MLlib with streaming pipelines

---

## Challenges Faced

- Handling timestamp parsing in streaming data
- Ensuring feature consistency between training and inference
- Debugging empty streaming batches due to watermark/window configuration
- Synchronizing real-time socket stream with Spark ingestion



