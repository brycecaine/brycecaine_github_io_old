---
title: Insights Building ETL to Redshift
date: 2017-01-21
categories: redshift python etl
comments: true
---

I've spent many hours at work lately developing a process to load data into our new AWS Redshift instance. I'm looking forward to when this ETL process will be ready for production. The plan is to:

- Provide a simple way to add ETL jobs, whether they be overwrites or appends
- Allow for initial and ongoing loads
- Adhere to best practices in loading data into Redshift

### ETL Jobs

The idea behind adding an ETL job will be to add all of the needed SQL statements as independent files, and then a corresponding python dictionary in the ETL script. (Eventually, I'm hoping to replace these dictionaries with database tables and hook a Django app into it.) An ETL job can be designated as an overwrite or an append. For now, overwrites will consist of deleting pertinent data and then appending updated data (similar to [this approach](http://docs.aws.amazon.com/redshift/latest/dg/t_updating-inserting-using-staging-tables-.html#merge-method-replace-existing-rows) in the AWS documentation). Rather than creating staging tables, though, S3 is utilized to stage the data as CSVs.<sup>[1](#footnote1)</sup>

### Initial and Ongoing

Adding a new ETL job consists of developing SQL scripts related to both the initial load as well as ongoing loads. The initial job includes creating the destination table, given the proper create statement, and skips creating it if it already exists. Ongoing jobs will consist of daily, weekly, semi-monthly, etc.

To ensure performance, I am planning on making deep copies of tables that are updated daily or less frequently. Eventually, when I have tables that are updated more frequently, I will utilize the `vacuum` command.

As I continue developing this solution, I will post more on the progress.

---

<a name="footnote1">1</a>: When I was at AWS re:Invent last November, I took occasion to ask an AWS engineer how he would handle periodically updating data in Redshift. He asked how many rows I was talking about, and I responded several thousand. He recommended using S3 to stage CSVs and then the `copy` command to load the data into tables. As I've compared loading data via insert statements versus the `copy` command, I can verify the fact that "the COPY command is many times faster and more efficient than INSERT commands" ([AWS Redshift Tutorial](http://docs.aws.amazon.com/redshift/latest/dg/tutorial-loading-data.html)).
