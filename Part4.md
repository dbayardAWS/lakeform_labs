# Part 4 - Create tables by crawling our S3 locations

In this part, we use the Glue Crawler to look at our two datasets and create table definitions for them in our data catalog.

You can read more about Glue Crawlers [here](https://docs.aws.amazon.com/glue/latest/dg/components-overview.html#crawling-intro).


## Create a crawler for the Flights data

* On the left-hand column of the Lake Formation console, click on "Crawlers"

![screen](images/lf23.png)

* If this is your first time using Glue in this account, click the "Get started" button.

* Click the "Add tables using a crawler" button

* Enter "flights_crawl" for the Crawler name and click "Next"

![screen](images/lf24.png)

* Leave the source type as "Data stores" and click "Next" again

* Enter this value in the "Include path" field:

```
s3://us-east-1.elasticmapreduce.samples/flights/parquet/
```

![screen](images/lf25.png)

* Click Next

* Leave the radio button as "No" and click "Next" 

* Change the radio button to "Choose an existing IAM role".  Select the "GlueCrawlerRole".  Then click "Next"

![screen](images/lf28.png)

* Leave the frequency to "Run on demand" and click "Next"

* Pick flights for the database using the drop-down.  Enter "flights_" as the prefix for the tables.  Click Next


![screen](images/lf29.png)

* Click Finish

* Then click the "Run it now link" (see below)

![screen](images/lf30.png)



## Create another crawler for the Product Reviews dataset

While the crawler is running for the Flights dataset, let's create another crawler for the Reviews dataset.


* Click the "Add crawler" button.

* Enter "reviews_crawl" for the Crawler name and click "Next"

![screen](images/lf31.png)

* Leave the source type as "Data stores" and click "Next" again

* Enter this value in the "Include path" field:

```
s3://amazon-reviews-pds/parquet/
```

![screen](images/lf32.png)

* Click Next

* Leave the radio button as "No" and click "Next" 

* Change the radio button to "Choose an existing IAM role".  Select the "GlueCrawlerRole".  Then click "Next"

![screen](images/lf28.png)

* Leave the frequency to "Run on demand" and click "Next"

* Pick reviews for the database using the drop-down.  Enter "reviews_" as the prefix for the tables.  Click Next


![screen](images/lf33.png)

* Click Finish

* Then click the "Run it now link" (see below)

![screen](images/lf34.png)

* Wait for both crawlers to finish running.  You should see both crawlers have a Status of "Ready".

![screen](images/lf35.png)

Notice that each crawler has added 1 table.

* Click on Tables on the left hand column of the Glue console.  

![screen](images/lf36.png)

These are the two tables that the crawlers created.  You can click on the table names if you would like explore further.



## Congratulations.

You have used Glue Crawlers to discover and define two new tables.  Now, we are ready to experiment with Lake Formation's security permissions.

Proceed onto [Part 5](Part5.md)
