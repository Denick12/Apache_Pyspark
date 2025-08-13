# Apache Spark (PySpark) Setup Guide for Ubuntu & macOS

This guide explains how to install and configure Apache Spark with PySpark on both **Ubuntu** and **macOS** in one place.

---

## Ubuntu Setup

1. **Create Apache Spark Directory**
```bash
mkdir ~/apache-spark
cd ~/apache-spark
```

2. **Download Apache Spark**
```bash
wget https://dlcdn.apache.org/spark/spark-4.0.0/spark-4.0.0-bin-hadoop3.tgz
```

3. **Extract & Organize Spark**
```bash
tar -xzf spark-4.0.0-bin-hadoop3.tgz
rm -rf spark-4.0.0-bin-hadoop3.tgz
mv spark-4.0.0-bin-hadoop3 spark
```

4. **Create & Activate Virtual Environment**
```bash
python3 -m venv sparkenv
source sparkenv/bin/activate
```

5. **Install PySpark**
```bash
pip install pyspark
```

6. **Check Spark Installation Folder**
Open another terminal:
```bash
cd ~/apache-spark/spark
ls
cd bin
ls
```

7. **Go Back to Apache Spark Root**
```bash
cd ../..
```

8. **Install dos2unix and Fix .bashrc**
```bash
sudo apt install dos2unix -y
dos2unix ~/.bashrc
```

9. **Configure Environment Variables**
```bash
nano ~/.bashrc
```
Add at the bottom:
```bash
export SPARK_HOME=$HOME/apache-spark/spark
export PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH
export PYSPARK_PYTHON=python3
```
Save (`CTRL+O`) and exit (`CTRL+X`).

10. **Apply Changes**
```bash
source ~/.bashrc
```

11. **Test Spark**
```bash
spark-shell --version
```

12. **Verify PySpark**
```bash
pyspark --version
```

---

## macOS Setup

1. **Create Apache Spark Directory**
```bash
mkdir ~/apache-spark
cd ~/apache-spark
```

2. **Download Apache Spark**
```bash
curl -O https://dlcdn.apache.org/spark/spark-4.0.0/spark-4.0.0-bin-hadoop3.tgz
```

3. **Extract & Organize Spark**
```bash
tar -xzf spark-4.0.0-bin-hadoop3.tgz
rm -rf spark-4.0.0-bin-hadoop3.tgz
mv spark-4.0.0-bin-hadoop3 spark
```

4. **Create & Activate Virtual Environment**
```bash
python3 -m venv sparkenv
source sparkenv/bin/activate
```

5. **Install PySpark**
```bash
pip install pyspark
```

6. **Configure Environment Variables**
```bash
nano ~/.zshrc
```
Add at the bottom:
```bash
export SPARK_HOME=$HOME/apache-spark/spark
export PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH
export PYSPARK_PYTHON=python3
```
Save (`CTRL+O`) and exit (`CTRL+X`).

7. **Apply Changes**
```bash
source ~/.zshrc
```

8. **Test Spark**
```bash
spark-shell --version
```

9. **Verify PySpark**
```bash
pyspark --version
```

---

## Testing Spark with Python

1. **Create Test Script**
```bash
nano test_spark.py
```
Paste:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("my_spark_app").getOrCreate()

sales_df = spark.read.csv("supermarket_data.csv", header=True, inferSchema=True)

sales_df.show(5)
sales_df.printSchema()
print(f"Total Rows: {sales_df.count()}")
```

2. **Run Test**
```bash
python test_spark.py
```

---

✅ You now have Apache Spark (PySpark) working on **both Ubuntu and macOS**.
