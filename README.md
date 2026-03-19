# 🏥 Big Data Architecture for Diabetes Prediction — Django + Kafka + Spark + Cassandra

A comprehensive real-time big data pipeline for diabetes prediction. This extended version of the diabetes prediction system includes geospatial analysis with Nepal district data, Streamlit dashboards, multiple Spark streaming configurations, batch processing, Cassandra storage, and a Django REST API backend.

---

## 📌 Description

This project builds a production-grade real-time data pipeline combining Django, Apache Kafka, Apache Spark Streaming, and Apache Cassandra to process, predict, and store diabetes patient data at scale. It extends the core diabetes prediction model with:

- **Geospatial visualization** of diabetes distribution across Nepal's districts using GeoJSON
- **Multiple Spark streaming scripts** for flexible stream processing and ML inference
- **Batch processing** alongside real-time streaming via `batch.py`
- **Cassandra output** for scalable NoSQL persistence
- **Streamlit dashboards** for interactive data exploration
- A **Django REST API** for data ingestion and serving predictions

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Django + SQLite3 | REST API backend and local database |
| Apache Kafka (3 brokers, 10 partitions) | Real-time data streaming |
| Apache Spark (PySpark) | Stream and batch ML inference |
| Apache Cassandra | Scalable NoSQL data storage |
| Apache Zookeeper | Kafka cluster coordination |
| Streamlit | Interactive data dashboards |
| TensorFlow / Keras | Diabetes prediction model |
| GeoJSON + Nepal district data | Geospatial diabetes distribution mapping |
| Pandas / NumPy | Data preprocessing |

---

## 📁 Project Structure

```
├── manage.py                         # Django management script
├── post_data.py                      # POST data to Django API (v1)
├── post_data_v2.py                   # POST data to Django API (v2)
├── consumer.py                       # Kafka consumer script
├── spark.py                          # Spark Streaming + Kafka + prediction
├── sparkdata.py                      # Spark data utilities
├── stream.py                         # Streamlit dashboard (v1)
├── stream1.py                        # Streamlit dashboard (v2)
├── streaming.py                      # Extended Spark streaming
├── batch.py                          # Batch processing script
├── batchy.py                         # Alternative batch processing
├── classifiers.py                    # Multiple ML classifier comparisons
├── cassandra_output.py               # Cassandra write utilities
├── diabetes_model.py                 # PySpark diabetes model
├── diabetes_m.py                     # Alternative model script
├── diabetes_train_model_pima.ipynb   # Model training notebook
├── training_with_4_fetaures.ipynb    # 4-feature model training
├── diabetic.csv                      # Diabetes patient dataset
├── districts.csv                     # Nepal district data
├── district_withId.csv               # Nepal districts with IDs
├── nepal.geojson                     # Nepal geospatial boundary data
├── requirements.txt                  # Python dependencies
├── finalmodel/                       # Saved ML models
├── templates/                        # Django HTML templates
├── hearts/                           # Heart disease related data
└── Git_files/                        # Demo screenshots
```

---

## ⚙️ Setup Instructions

### 1. Clone and Set Up Virtual Environment
```bash
git clone https://github.com/priya-zha/BigData-Architecture-Diabetes-Prediction.git
cd BigData-Architecture-Diabetes-Prediction
python3 -m venv dependency_env
source dependency_env/bin/activate
pip install -r requirements.txt
```

### 2. Run Django Backend
```bash
python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py runserver
# API: http://localhost:8000/api
```

### 3. Setup Kafka (3 Brokers)
```bash
cp config/server.properties config/server-1.properties
cp config/server.properties config/server-2.properties
# Update broker.id, listeners, log.dir in each config
sudo systemctl start zookeeper
sudo systemctl start kafka && sudo systemctl start kafka1 && sudo systemctl start kafka2
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 3 --partitions 10 --topic hospital
```

### 4. Post Data
```bash
python post_data.py
```

### 5. Run Spark Streaming
```bash
python spark.py
# Spark UI: http://localhost:4040
```

### 6. Setup Cassandra (Optional)
```bash
pip3 install cassandra-driver
cqlsh
# CREATE KEYSPACE diabetesdb WITH replication = {'class':'SimpleStrategy', 'replication_factor':3};
# USE diabetesdb;
# CREATE TABLE diabetesb (...);
```

---

## 🖼️ Screenshots

![Spark Job](./Git_files/sparkjob.png)
![Diabetic Prediction](./Git_files/diabetic.png)
![No Diabetes](./Git_files/nodiabetes.png)
![Cassandra](./Git_files/cassandra.png)

---

## 📋 Requirements

- Python 3.7.1 (recommended)
- Java 8+
- Apache Kafka + Zookeeper
- Apache Spark 2.4.x + `spark-streaming-kafka-0-8-assembly_2.11-2.4.5.jar`
- Apache Cassandra
- Django, Streamlit, TensorFlow/Keras

---

## 👩‍💻 Author

**Priya** — [@priya-zha](https://github.com/priya-zha)
