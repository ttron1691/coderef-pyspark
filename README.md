# coderef-pyspark
# Imports
```Python
from pyspark.sql import SparkSession

import pyspark.sql.functions as F
import pyspark.sql.types as T
```
# PySpark Session
A PySpark session is considered as an entry point for interacting with Spark. The basic process to create a Spark session is given as follows
```Python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("appName").getOrCreate()
```
# PySpark DataFrame
We can create a PySpark data frame using the createDataFrame method as follows
```Python
SparkSession.createDataFrame(data, 
                             schema=None, 
                             samplingRatio=None, 
                             verifySchema=True)
```
## Create Data frame
```Python
import pyspark.sql.functions as F
import pyspark.sql.types as T

columns = ["first_name", "last_name", "salary"]
data = [("John", "Smith", 60000),
        ("Andrew", "White", 80000)]

df_spark = spark.createDataFrame(data=data, schema=columns)
```
We can also create a PySpark data frame from a given Pandas data frame
```Python
import pyspark.sql.functions as F
import pyspark.sql.types as T

import pandas as pd

df_pandas = pd.DataFrame(data={"id": [1, 2],
                               "name": ["John Smith", "Andrew White"]})

df_spark = spark.createDataFrame(df_pandas)
```
## Collect rows
We can collect the rows of a data frame by using the collect method
```Python
df = spark.createDataFrame(data=[(14, "Tom"), (23, "Alice"), (16, "Bob")], 
                           schema=["age", "name"])
df.collect()
```
This evalues to
```
[Row(age=2, name='Alice', age2=4), Row(age=5, name='Bob', age2=7)]
```
## Columns
We can add a new column to a given PySpark data frame as follows
```Python
DataFrame.withColumn(colName, 
                     col)
```
We give some examples in the following
```Python
# Add new column with constant value
df_spark_col = df_spark.withColumn("new_column", F.lit("value"))
# Add new column by performing aggregation with respect to existing column
df2 = df.withColumn('age_add_two', df.age + 2)
```

# Input and Output
## Input
### CSV
The general function for reading CSV files in PySpark is given as follows
```Python
DataFrameReader.csv(path, 
                    schema=None, 
                    sep=None, 
                    encoding=None, 
                    quote=None, 
                    escape=None, 
                    comment=None, 
                    header=None, 
                    inferSchema=None, 
                    ignoreLeadingWhiteSpace=None, 
                    ignoreTrailingWhiteSpace=None, 
                    nullValue=None, 
                    nanValue=None, 
                    positiveInf=None, 
                    negativeInf=None,
                    dateFormat=None, 
                    timestampFormat=None, 
                    maxColumns=None, 
                    maxCharsPerColumn=None, 
                    maxMalformedLogPerPartition=None, 
                    mode=None, 
                    columnNameOfCorruptRecord=None, 
                    multiLine=None, 
                    charToEscapeQuoteEscaping=None, 
                    samplingRatio=None, 
                    enforceSchema=None, 
                    emptyValue=None, 
                    locale=None, 
                    lineSep=None, 
                    pathGlobFilter=None, 
                    recursiveFileLookup=None, 
                    modifiedBefore=None, 
                    modifiedAfter=None, 
                    unescapedQuoteHandling=None)
```
Reading a CSV file can be done via
```Python
df = spark.read.csv("/path/to/file/data.csv")
```
Alternatively, we can proceed in the following way
```Python
df = spark.read.format("csv").load("/path/to/file/data.csv")
```
There are several options for reading csv files
```Python
# Parameter to set delimiter
df2 = spark.read.option("delimiter", ",").csv(path)
# Parameter to set header
df3 = spark.read.option("delimiter", ";").option("header", True).csv(path)
# Parameter for multiple options
df4 = spark.read.options(delimiter=";", header=True).csv(path)
```
In addition, within PySpark we can read multiple CSV files by using the following method
```Python
df5 = spark.read.csv("path1,path2,path3")
df6 = spark.read.format("csv").load("/path/to/files/*.csv")
```
### Parquet
### Snowflake
## Output
### CSV
### Parquet
### Snowflake

```Python
a
```
