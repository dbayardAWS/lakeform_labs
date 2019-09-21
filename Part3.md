# Part 3 - Create databases


## Create databases in Lake Formation

* On the left hand column, click "Dashboard"


![screen](images/lf13.png)


* Click the Create database button

![screen](images/lf14.png)

* Enter "flights" for the Name

* For the Location, enter this value:

```
s3://us-east-1.elasticmapreduce.samples/flights/parquet/
```

![screen](images/lf15.png)

* Click the Create database button

![screen](images/lf16.png)

* On the Databases page, click "Create database button" to create a 2nd database

* Enter "reviews" for the Name

* For the Location, enter this value:

```
s3://amazon-reviews-pds/parquet/
```

![screen](images/lf17.png)



## Grant privileges on the databases to Glue Crawler

* On the left hand column, click "Dashboard"


![screen](images/lf13.png)


* Click the Grant permissions button

![screen](images/lf18.png)

* Use the "IAM users and roles" drop-down, and scroll-down and choose the "GlueCrawlerRole".

![screen](images/lf19.png)

* Use the "Database" drop-down and select the flights database.  Then do the same for the review database.

![screen](images/lf20.png)

* Check the box in front of "All" in the Database permissions section.  Then click "Grant"

![screen](images/lf21.png)

![screen](images/lf22.png)



## Congratulations.

You have created 2 databases in Lake Formation and granted the Glue Crawler permissions to add tables to them.  Next we will use the Glue Crawler to add some tables.

Proceed onto [Part 4](Part4.md)
