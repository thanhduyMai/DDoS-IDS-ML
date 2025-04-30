This project is the final assignment for the Big Data in Security course. It demonstrates the use of Apache Spark for processing and analyzing massive network traffic datasets to detect and understand various types of Distributed Denial of Service (DDoS) attacks.

The dataset used is CICDDoS2019, which contains real-world attack traffic, including various amplification and flooding techniques. The project provides in-depth exploration of several attack types and their network characteristics using PySpark's distributed computing capabilities.

🗂️ Dataset Summary
The dataset consists of large CSV files representing different types of DDoS attacks. Here are some key files analyzed:


File Name	Description
TFTP.csv (8.7GB)	TFTP Amplification Attack — small requests result in large responses to overwhelm the victim.
DrDoS_SNMP.csv (2.1GB)	SNMP Reflection Attack — exploits the SNMP protocol for large-volume reflection.
DrDoS_DNS.csv (2.0GB)	DNS Amplification — leverages open DNS servers to reflect traffic.
DrDoS_MSSQL.csv (1.8GB)	Uses Microsoft SQL Servers to perform traffic amplification.
DrDoS_NetBIOS.csv (1.6GB)	Exploits NetBIOS Name Service for reflection attacks.
DrDoS_UDP.csv (1.5GB)	General UDP Amplification.
DrDoS_SSDP.csv (1.2GB)	SSDP-based attacks exploiting UPnP protocol.
DrDoS_LDAP.csv (875MB)	LDAP amplification attacks.
DrDoS_NTP.csv (616MB)	NTP monlist reflection-based amplification.
Syn.csv (608MB)	SYN Flooding — sends SYN packets to exhaust server resources.
🛠 Technologies Used
Python 3.x

Apache Spark (PySpark)

Google Colab or Jupyter Notebook

Pandas, Matplotlib, Seaborn for data manipulation and visualization

📊 Project Structure
The notebook is structured into the following main parts:

1. Spark Setup and Configuration
Initializes PySpark in a Colab environment using Java 8 and Spark 3.3.0.

Sets up necessary environment variables.

2. Dataset Inspection and Management
Inspects and explains the role of each CSV file.

Loads selected large files using Spark to handle the scale efficiently.

3. Data Preprocessing
Uses Spark to:

Drop nulls

Handle schema inference

Rename columns for readability

Convert timestamp formats

4. Exploratory Data Analysis (EDA)
Computes statistics like min, max, average for key metrics: Flow Duration, Total Fwd Packets, Flow Bytes/s, etc.

Visualizes trends and distributions with:

Boxplots for feature range comparison

Histograms and heatmaps

5. Attack Pattern Investigation
Identifies distinguishing characteristics of different attack types (e.g., amplification ratio, packet size, duration).

Detects outliers or abnormal patterns using statistical techniques.

6. Conclusions
Summarizes key differences among attack types.

Discusses the effectiveness of PySpark in handling multi-gigabyte data.

🚀 How to Run
Option 1: Google Colab (Recommended)
Upload the notebook to Google Colab.

Use Google Drive to mount and access the large dataset files.

Run the notebook cells sequentially.

Option 2: Local Environment
Install the dependencies:

pip install pyspark pandas matplotlib seaborn
Download Spark and Java, configure environment variables.

Run the notebook using Jupyter:

jupyter notebook BigData_in_Security_Final.ipynb
📈 Results & Insights
Spark can process multi-gigabyte CSV logs with efficiency and flexibility.

Different DDoS attack types exhibit unique statistical signatures.

TFTP and SNMP amplification produce significantly larger Flow Bytes/s compared to SYN flooding.

Visualizations revealed distinct anomalies in packet flow, duration, and size.

🤖 Machine Learning Pipeline
To build an automated detection system for DDoS attacks, this project includes a supervised machine learning pipeline using PySpark.

🏗️ Preprocessing Steps
Label Encoding:

Categorical labels (attack types and benign traffic) are encoded using StringIndexer to create a numerical label column (Label_Index).

Feature Selection:

A wide range of numeric features are selected, such as:

Packet sizes (Fwd_Packet_Length_Max, Bwd_Packet_Length_Mean)

Flow rates (Flow_Bytes_per_s, Flow_Packets_per_s)

Time-based metrics (Flow_Duration, Idle_Mean, Fwd_IAT_Std)

TCP flags (SYN_Flag_Count, ACK_Flag_Count)

Window sizes and interarrival times.

Feature Assembly:

VectorAssembler is used to merge all selected features into a single feature vector column for ML input.

Pipeline Construction:

The ML pipeline includes:

StringIndexer for label encoding

VectorAssembler for features

(Optional) StandardScaler for normalization

📊 Model Training
Dataset: A sampled, balanced subset of the large attack data.

Train-Test Split: The data is randomly split into training (80%) and testing (20%) sets.

Classifier: RandomForestClassifier from PySpark's MLlib is used due to its:

High accuracy

Robustness to unscaled or non-normal data

Interpretability

from pyspark.ml.classification import RandomForestClassifier

rf = RandomForestClassifier(labelCol="Label_Index", featuresCol="features", numTrees=100)
model = rf.fit(train_df)
predictions = model.transform(test_df)
🧪 Evaluation Metrics
Accuracy: Measures the overall correct predictions.

Confusion Matrix: Identifies true positives, false positives, etc.

Precision, Recall, F1-Score: Evaluated using MulticlassClassificationEvaluator.

Results
The Random Forest model achieved high accuracy, correctly classifying various types of DDoS traffic.

It proved especially effective in distinguishing amplification attacks from regular UDP/TCP flows.



📚 References
CICDDoS2019 Dataset – Canadian Institute for Cybersecurity

PySpark Documentation: https://spark.apache.org/docs/latest/api/python/

Colab setup instructions for Spark and Java

👥 Authors
Mai Thanh – Project implementation and analysis
