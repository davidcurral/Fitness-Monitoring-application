# 🏃‍♂️ IoT Exercise Monitoring System
This project is an integrated IoT solution for physical activity monitoring, designed to collect sensor data (accelerometer/gyroscope), process it in real-time and offline, and display detailed metrics on an interactive dashboard.

## 🏗️ System Architecture
The solution is built on containerized microservices via Docker, ensuring isolation and scalability:
* Mosquitto (MQTT): Broker responsible for secure communication between clients and the server, using the TLS protocol to ensure data privacy (pp. 2, 4).
* Node-RED: The central logic engine, managing data flow, database integration, and hosting the web dashboard (p. 2).
* SQLite: Relational database used for efficient storage of historical and real-time data (p. 2).
* ML App: A dedicated container for Machine Learning processing to classify physical activities (p. 2).

## 📊 Core Features
1. Data Processing (Online & Offline)
    * Offline Pipeline: Import of historical data via CSV into the SQLite database, featuring automatic date-format transformations (p. 2).
    * Online Pipeline: Device simulation via MQTT, limited to 20 msg/s to ensure system stability and reliable processing (p. 4).
    * Normalization: Data is aggregated by minute to provide a more realistic and readable view of physical activity (p. 2).

2. Intelligent Dashboard - the dashboard provides a comprehensive interface for the end-user:
    * Profile Setup: Input for weight, height, age, and gender for personalized metric calculations (p. 3).
    * Metric Calculation: Algorithms to determine calories burned and distance covered (daily and weekly) (p. 5).
    * Sedentary Analysis: Adjustable thresholds for walking and running to define active vs. sedentary periods (p. 3).

## 🧠 Machine Learning
The project includes classification models (LR, LDA, DT, KNN, GNB) to identify the type of exercise based on sensor inputs (p. 5). During testing, the Decision Tree (DT) model achieved the highest accuracy, approximately 98.8% (p. 5).

## 🛠️ Getting Started
1. Ensure Docker and Docker-Compose are installed.
2. Clone this repository..
3. Run the following command:bash -> docker-compose up -d
4. Access the Node-RED Dashboard at http://localhost:1880/ui.
5. Create new certificates in Mosquito/certs

## ⚠️ Challenges & Limitations
While the project successfully implements the core IoT pipeline, some challenges were encountered during development:
* Machine Learning Integration: Although several ML models (DT, KNN, etc.) were developed and achieved high accuracy (up to 98.8%), integrating the prediction script directly into the live MQTT flow presented synchronization issues after switching to a more complex secure MQTT setup (p. 4).
* System Complexity: The extensive requirements for real-time data processing vs. offline database management required a significant balancing act in Node-RED to ensure no data loss occurred during high-frequency bursts (20 msg/s) (p. 4).
* Real-world Accuracy: The current movement classification is a simplified model. Future iterations would benefit from more diverse training datasets to better represent the wide variety of human movement patterns in nature (p. 6).

## 🏁 Conclusion
The project successfully demonstrates an end-to-end IoT ecosystem—from sensor simulation and secure MQTT transmission to cloud processing and data visualization. It provided a practical understanding of how modern fitness applications manage and interpret user data in a secure, containerized environment (p. 6)
