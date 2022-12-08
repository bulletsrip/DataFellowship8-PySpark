# Installing Apache Spark on Linux Ubuntu

## Installing Java

Download OpenJDK 11 or Oracle JDK 11 (It's important that the version is 11 - spark requires 8 or 11)

We'll use [OpenJDK](https://jdk.java.net/archive/)

Download it (e.g. to `~/spark`):

```
wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
```

Unpack it:

```bash
tar xzfv openjdk-11.0.2_linux-x64_bin.tar.gz
```

define `JAVA_HOME` and add it to `PATH`:

```bash
export JAVA_HOME="${HOME}/spark/jdk-11.0.2"
export PATH="${JAVA_HOME}/bin:${PATH}"
```

check that it works:

```bash
java --version
```

Output:

```
openjdk 11.0.2 2019-01-15
OpenJDK Runtime Environment 18.9 (build 11.0.2+9)
OpenJDK 64-Bit Server VM 18.9 (build 11.0.2+9, mixed mode)
```

Remove the archive:

```bash
rm openjdk-11.0.2_linux-x64_bin.tar.gz
```

## Installing Spark

Download Spark. Use 3.3.0 version:

```bash
wget https://dlcdn.apache.org/spark/spark-3.3.0/spark-3.3.0-bin-hadoop3.tgz
```

Unpack:

```bash
tar xzfv spark-3.3.0-bin-hadoop3.tgz
```

Remove the archive:

```bash
rm spark-3.3.0-bin-hadoop3.tgz
```

Add it to `PATH`:

```bash
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
export PYSPARK_PYTHON=/usr/bin/python3
```

### Testing Spark

Execute `spark-shell` and run the following:

```scala
val data = 1 to 10000
val distData = sc.parallelize(data)
distData.filter(_ < 10).collect()
```
### Screenshots
![spark-cli](https://user-images.githubusercontent.com/85284506/206483164-2cf65aa1-9b2e-47f5-a19c-a016188fbae7.jpg)
![spark-shell](https://user-images.githubusercontent.com/85284506/206483175-2463c1f0-3e52-476a-a0cf-06761663af8f.jpg)
## PySpark

### Integrating PySpark with Jupyter Notebook
The only requirement to get the Jupyter Notebook reference PySpark is to add the following environmental variables in your .bashrc or .zshrc file, which points PySpark to Jupyter.

```bash
export PYSPARK_DRIVER_PYTHON='jupyter'
export PYSPARK_DRIVER_PYTHON_OPTS='notebook --no-browser --port=8889'
```
The PYSPARK_DRIVER_PYTHON points to Jupiter, while the PYSPARK_DRIVER_PYTHON_OPTS defines the options to be used when starting the notebook. In this case, it indicates the no-browser option and the port 8889 for the web interface.

Now, we can directly launch a Jupyter Notebook instance by running the pyspark command in the terminal.

`$ pyspark`

![pyspark](https://user-images.githubusercontent.com/85284506/206484629-57b13b6e-84e8-4d46-a6cf-e26d8c93c061.jpg)

To install findspark just type:

`$ pip install findspark`

And then on Jupyter Notebook to initialize PySpark, run:

```python
import findspark
findspark.init()
import pyspark
sc = SparkContext.getOrCreate();
```

To print the Spark Version, run:

```python
spark = SparkSession.builder \
    .master("local[*]") \
    .appName('myapp') \
    .getOrCreate()
    
def main():
    print(f'Spark Version:, {spark.version}')
    
if __name__ == '__main__':
    main()
```
![spark vesion](https://user-images.githubusercontent.com/85284506/206486380-c078386a-97da-474f-a670-423b35136e54.jpg)
