# coderef-pyspark
## Data types
```Python
BooleanType                     # Represents boolean values

ByteType                        # Represents 1-byte signed integer numbers, -128 to 127
ShortType                       # Represents 2-byte signed integer numbers, -32768 to 32767
IntegerType                     # Represents 4-byte signed integer numbers, -2147483648 to 2147483647
LongType                        # Represents 8-byte signed integer numbers, -9223372036854775808 to 9223372036854775807

DecimalType                     # Represents arbitrary-precision signed decimal numbers
FloatType                       # Represents 4-byte single-precision floating point numbers
DoubleType                      # Represents 8-byte double-precision floating point numbers

StringType                      # Represents character string values
CharType                        # A variant of VarcharType(length) which is fixed length

DateType                        # Represents values comprising values of fields year, month and day, without a time-zone
TimestampType                   # Timestamp with local time zone(TIMESTAMP_LTZ)
TimestampNTZType                # Timestamp without time zone(TIMESTAMP_NTZ)

StructField(name, dataType)     # 
StructType([fields])            #

```

## Table data types
```Python
pyspark.sql.DataFrame           # Data type for data frame
pyspark.sql.Row                 # Data type for row of data frame
pyspark.sql.Column              # Data type for column of data frame

DataFrameReader                 # Data type for data frame reader
DataFrameWriter                 # Data type for data frame writer             
```

## DataFrame

### Attributes
```Python
df.columns                      # Get column names
df.dtypes                       # 
df.schema
df.write                        # Interface for saving DataFrame into external data sink

```

### Methods
```Python

# Show content
df.show([n])                    # Show content of data frame
df.head(n)                      # Select list including first n rows
df.tail(n)                      # Select list including last n rows
df.first()                      # Returns first row as a Row
df.select(*cols)                # Projects a set of expressions and returns a new DataFrame

# Properties
df.count()                      # Returns to number of rows in data frame
df.printSchema()                # Prints out the schema in the tree format
df.describe()                   # Computes basic statistics for numeric and string columns

# Filtering
df.filter(condition)            # Filter data frame according to condition, e.g. df.filter(df.age > 3)
df.where(condition)             # Filter data frame according to condition

# Add columns
df.withColumn(colName, col)         # Returns a new DataFrame by adding a column
df.withColumnRenamed(colName, col)  # Returns a new DataFrame by renaming existing column 

# Remove columns
df.drop(*cols)                  # Returns a new DataFrame that drops the specified column
df.dropDuplicates([subset])     # Return a new DataFrame with duplicate rows removed
df.drop_duplicates([subset])    # Alias for dropDuplicates()
df.dropna()                     # Returns a new DataFrame omitting rows with null values

# Fill row values
df.fillna(value[, subset])      # Replace null values, alias for na.fill()
df.replace(to_replace)          # Returns a new DataFrame replacing a value with another value

# Joins
df.join(other[, on, how])       # Join with another DataFrame
df.crossJoin(other)             # Returns the cartesian product with another DataFrame

# Repartitioning
df.repartition(numPartitions, *cols)    # Returns a new DataFrame partitioned 

# Export
df.collect()                    # Returns all the records as a list of Row
df.toPandas()                   # Returns data frame as type of pandas.DataFrame
df.toDF(*cols)                  # Returns a new DataFrame with new specified column names
df.toJSON()                     # Converts a DataFrame into a RDD of string
```

## Input
### General
```Python
# General
DataFrameReader.load([path, format, schema])            # Loads data from a data source and returns it as a DataFrame
DataFrameReader.option(key, value)                      # Adds an input option for the underlying data source
DataFrameReader.options(**options)                      # Adds input options for the underlying data source
DataFrameReader.format(source)                          # Specifies the input data source format

# CSV
DataFrameReader.csv(path[, schema, sep, …])             # Loads a CSV file and returns the result as a DataFrame

# JSON
DataFrameReader.json(path[, schema, …])                 # Loads JSON files and returns the results as a DataFrame

# Parquet
DataFrameReader.parquet(*paths, **options)              # Loads Parquet files, returning the result as a DataFrame

# Table
DataFrameReader.table(tableName)                        # Returns the specified table as a DataFrame

# Snowflake (using specific format)
DataFrameReader.format("snowflake")                     # Specifies the format for connection with Snowflake
```

### Examples
```Python
# CSV
df_csv_1 = spark.read.csv(path)
df_csv_2 = spark.read.option("delimiter", ";").csv(path)
df_csv_3 = spark.read.option("delimiter", ";").option("header", True).csv(path)
df_csv_4 = spark.read.options(delimiter=";", header=True).csv(path)

# JSON
df_json_1 = spark.read.json("examples/src/main/resources/people.json")

# Parquet
df_parquet_1 = spark.read.parquet("people.parquet")
df_parquet_2 = spark.read.format("parquet").load("file.parquet")
```

## Output
### General
```Python
# General
DataFrameWriter.save([path, format, mode, …])           # Saves the contents of the DataFrame to a data source
DataFrameWriter.option(key, value)                      # Adds an output option for the underlying data source
DataFrameWriter.options(**options)                      # Adds output options for the underlying data source
DataFrameWriter.format(source)                          # Specifies the underlying output data source
DataFrameWriter.insertInto(tableName[, …])              # Inserts the content of the DataFrame to the specified table
DataFrameWriter.mode(saveMode)                          # Specifies the behavior when data or table already exists

# CSV
DataFrameWriter.csv(path[, mode, …])                    # Saves the content of the DataFrame in CSV format at the specified path

# JSON
DataFrameWriter.json(path[, mode, …])                   # Saves the content of the DataFrame in JSON format

# Parquet
DataFrameWriter.parquet(path[, mode, …])                # Saves the content of the DataFrame in Parquet format at the specified path

# Snowflake (using specific format)
DataFrameWriter.format("snowflake")                     # Specifies the format for connection with Snowflake
```

### Examples
```Python
# CSV
df_csv_1.write.csv("/tmp/spark_output/zipcodes")
df_csv_2.write.option("header", True).csv("/tmp/spark_output/zipcodes")
df_csv_3.write.options(header='True', delimiter=',').csv("/tmp/spark_output/zipcodes")
df_csv_4.write.mode("overwrite").csv("/tmp/spark_output/zipcodes")
df_csv_5.write.format("csv").mode('overwrite').save("/tmp/spark_output/zipcodes")

# JSON
...

# Parquet
df_parquet_1.write.parquet("/tmp/out/people.parquet") 
df_parquet_2.write.mode("append").parquet("path/to/parquet/file")
df_parquet_3.write.mode("overwrite").parquet("path/to/parquet/file")
```

### Row
```Python
a

## References

```

### Column
```Python
a
```

## References
- PySpark API reference: [https://spark.apache.org/docs/latest/api/python/index.html](https://spark.apache.org/docs/latest/api/python/index.html)
