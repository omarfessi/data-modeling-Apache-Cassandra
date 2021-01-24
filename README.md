# Data-modeling-ApacheCassandra 
## Project Overview
This one is the 2nd work within my Data Engineering training projects - please feel free to check [data-modeling-Postgres](https://github.com/omarfessi/data-modeling-Postgres) first for more consistency. In this project, as I did in the first one I'll model user activity data for a music streaming app called Sparkify. I am particulary interested in understanding what songs users are listening to, and there is no easy way to query the data to generate the results since the data resides in a directory of CSV files on user activity on the app.
Here the job is to create an ETL pipeline using Python and build an Apache Cassandra database which can create queries on song data to answer the questions. 

## Project Template
The project template includes one `data-modeling.ipynb` Jupyter Notebook file in which:
- I process the csv files in `event_data` data folder to create the final csv file to be used in the Apache Cassandra database (ETL-part of the work).
- I model the data tables keeping in mind the queries I need to run.(Modeling part of the work )
- I load the data into tables.

## Project outcomes:
The project is a demonstration of how the NoSql data modeling is different from the SQL data modeling in the previous project, focusing on the basics of NoSql database design, denormalization, primary keys,partition keys, clustering columns and WHERE clauses.
### Denormalization in Apache Cassandra
The denormalization in Apache Cassandra is absolutely critical. The biggest take away when doing data modeling in Apache Cassandra is to think about your `queries` first. There are `no joins ` in Apache Cassandra.
Here where the difference between relational data modeling and non-relational data modeling is. The normalized data table must go through the process of `denormalization` to fit in the Apache Cassandra data model. 
In modeling with non-relational database one top priority to consider is `what queries I need to run`, based on that the modeling must be. So to recap :
- There are no joins, Only one query on one table at a time.
- Denormalization must be done for fast reads.
- Apache Cassandra has been optimized for fast writes.
- Think queries first.
- One table per query: Okay with redundant data but noway to miss up with latency.

### CQL: Cassandra Query Language
CQL is the way to interact with the database and is very similar to SQL, except JOINS, GROUP BY or subqueries are not supported.
In the notebook I will be using a Python driver for cassandra. please refer to this [youtube link](https://www.youtube.com/watch?v=XyrDoak3YnI) to properly install cassandra. Once you finish installation pip install cassandra-drive and finally import it in you notebook.
### PRIMARY KEY 
- The `PRIMARY KEY` is how each row can be uniquely identified and how data is distributed across the nodes.
- The first element of the `PRIMARY KEY` is the `PARTITION KEY` which will determine the distribution.
- The `PRIMARY KEY` is made up of either just the `PARTITION KEY`-which can single or multiple or with the addition of `CLUSTERING COLUMNS`.
- The `PARTITION KEY`'s row value will be hashed (turned into a number) and stored on the node in the system that holds that range of values.
- The `CLUSTERING COLUMN` will determine the sort within a partition, and will sort the data in `ASC` order. More than one clustering column can be added or none.
- The Clustering columns wol sort in order of how they were added to the primary key
- => ``` PRIMARY KEY ((Partition Keys),(Clustering Columns))``` <= 
- We can use as many clustering columns as we would like. But we cannot use the clustering columns out of order in the `SELECT` statement. you may choose to omit using a clustering column in the `SELECT` statement. That's Okay.

## Conclusion
I think the notebook is well documented and structered so it would be easy to understand.
What I like more about this project is that inspite of the it's simplicity and small code, it break down complicated concepts of NoSQL with Apache Cassandra against SQL modeling. Please feel free to get in touch for any type of feedback and questions.

