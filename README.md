Amazon Metadata Streaming: Frequent Itemset Mining with Apriori, PCY & Anomaly Detection

[![Python](https://img.shields.io/badge/Built%20with-Python-blue.svg)](https://www.python.org/)
[![Apache Kafka](https://img.shields.io/badge/Stream-Apache%20Kafka-red.svg)](https://kafka.apache.org/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB-green.svg)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A real-time streaming pipeline to analyze **Amazon product metadata** using Kafka and Python. It features three concurrent consumers: **Apriori**, **PCY**, and **Anomaly Detection**, with results stored in **MongoDB**.

---

## 📈 Use Case

- Perform **market basket analysis** on large-scale product metadata.
- Stream data using Kafka for **real-time processing**.
- Detect **frequent itemsets**, generate **association rules**, and find **anomalies** in product patterns.

---

## 🛠️ Setup Instructions

### 1️⃣ Environment Setup

```bash
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
pip install -r requirements.txt
```

### 2️⃣ Download NLTK Resources

```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
```

---

## 📦 Requirements

- Python 3.7+
- Kafka + Zookeeper installed locally
- MongoDB running on port 27017

### 🧰 Dependencies (see requirements.txt)
- pandas, numpy, tqdm, swifter  
- nltk, bs4, streamlit  
- kafka-python, pymongo  
- scikit-learn

---

## 🧹 Data Preparation

1. Download Amazon metadata: https://cseweb.ucsd.edu/~jmcauley/datasets/amazon_v2/  
2. Sample down to 20GB: `All_Amazon_Meta_Sampled.json`
3. Preprocess:
  - Remove nulls
  - Clean HTML, punctuation
  - Tokenize and remove stopwords
4. Save cleaned output as line-separated JSON

---

## 🔁 Kafka Architecture

### 🎯 Producer
- Streams product transactions to Kafka topic (`amazon-meta`)

### 🧠 Consumer 1: Apriori
- Identifies frequent itemsets
- Generates association rules
- Stores to MongoDB:
  - `apriori`
  - `apriori_associationrules`

### 🔎 Consumer 2: PCY
- Optimized version using hashed buckets
- Saves frequent pairs to:
  - `pcy_frequent_itemsets`
  - `pcy_association_rules`

### 🚨 Consumer 3: Anomaly Detector
- Uses Z-scores to find statistical anomalies in product co-occurrences
- Stores anomalies to:
  - `anomalies`

---

## 🗄️ MongoDB Integration

**Database**: `Frequent_Itemset`

| Component   | Collection                | Description                         |
|-------------|----------------------------|-------------------------------------|
| Apriori     | `apriori`, `apriori_associationrules` | Frequent sets + rules     |
| PCY         | `pcy_frequent_itemsets`, `pcy_association_rules` | Hash-based rules |
| Anomalies   | `anomalies`                | Z-score anomaly logs                |

---

## ▶️ How to Run

1️⃣ Ensure the following before you run:
- Kafka is installed in `~/kafka`
- MongoDB is running locally on port `27017`
- All Python files and `Bash_Rc.sh` are placed in `~/Documents`

2️⃣ Give execution permissions to the script (first time only):

```bash
chmod +x Bash_Rc.sh
```

3️⃣ Run the full pipeline with:

```bash
./Bash_Rc.sh
```

✅ This will automatically:
- Start **Zookeeper** in a new terminal
- Start **Kafka Server**
- Start the **Producer**
- Start **Consumer 1** (Apriori)
- Start **Consumer 2** (PCY)
- Start **Consumer 3** (Anomaly Detection)

🖥️ Each component runs in its own terminal window using `gnome-terminal`
ℹ️ Press Enter in each terminal after execution starts to close that window

---


This starts the producer and all 3 consumers.

---

## 📂 Project Structure

```
├── producer.py                   # Kafka producer
├── apriori.py                    # Apriori consumer
├── pcy.py                        # PCY consumer
├── anomaly.py                    # Anomaly detection consumer
├── Bash_Rc.sh                    # Kafka launch script
├── Pre_Processing.ipnb           # Jupyter notebook for data prep
├── requirements.txt              # Required libraries
├── LICENSE                       # MIT license
└── README.md                     # You're here!

```

---

## 📌 Use Cases

- 🛒 E-commerce recommender systems
- 📊 Real-time product analytics
- 🧠 Research on scalable data mining

---

## 📄 License

This project is licensed under the **MIT License**.  
See the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Saim Nadeem**  
🔗 GitHub: [Saim-Nadeem](https://github.com/Saim-Nadeem)

---

## 🙌 Acknowledgments

- UCSD Amazon Metadata Dataset  
- Apache Kafka & MongoDB Docs  
- Algorithm insights from research and GfG  
- nltk, tqdm, streamlit, and Python OSS libraries

---
