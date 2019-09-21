# Lake Formation Security Demonstration

## Setup the initial users

### Create the Lake Formation Administrator user

* Navigate to the IAM Console

![screen](images/iam1.png)

* Click on Users on the left hand column

* Then click the Add user button.

* Enter "LFadmin" for User name.  Check the "AWS Management Console access" box.  Enter a custom password that you will remember.  And uncheck the "User must create a new password" box.  Then click "Next: Permissions"

![screen](images/iam2.png)

* Click the "Attach existing policies directly" button.  Then check the box for "AdministratorAccess".  Then click "Next: Tags"

![screen](images/iam3.png)

* Click "Next: Review"

* Review the information and click "Create user"

![screen](images/iam4.png)

* Copy the sign-in url (https://######.signin.aws.amazon.com/console) and save it in a notepad or text editor for later.  Click "Close"

![screen](images/iam5.png)

### Create two query users

* Click the "Add user" button 


This is based on the instructions [here](https://docs.aws.amazon.com/lake-formation/latest/dg/tut-create-lf-user.html)

* Enter "UserFlights" for the User name.  Then click "Add another user"

![screen](images/iam6.png)

* Enter "UserAll" for the 2nd User name.

![screen](images/iam7.png)


* Check the "AWS Management Console access" box.  Enter a custom password that you will remember.  And uncheck the "User must create a new password" box.  Then click "Next: Permissions"

![screen](images/iam8.png)

* Click the "Attach existing policies directly" button.  Then enter the search term "Athena".  Then check the box for "AmazonAthenaFullAccess".  


![screen](images/iam9.png)

* Click the "Create policy" button.  A new browser tab will open.

![screen](images/iam10.png)

* In the "Create policy" page, click on the JSON tab.  Paste the following into the text area (overwriting the previous contents):


```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lakeformation:GetDataAccess",
                "glue:GetTable",
                "glue:GetTables",
                "glue:SearchTables",
                "glue:GetDatabase",
                "glue:GetDatabases",
                "glue:GetPartitions"
            ],
            "Resource": "*"
        }
    ]
}

```

![screen](images/iam11.png)

* Click "Review policy" button at the bottom of the Create policy page.

* Name the policy "DatalakeUserBasic" and click "Create policy"

![screen](images/iam12.png)

* You should see that the policy has been created.  

![screen](images/iam13.png)

* Now go back to the previous browser tab where you were creating the 2 query users.

![screen](images/iam14.png)

* Clear out the search field and type in "Datalake".  Then click on the refresh button 

![screen](images/iam15.png)

* Check the box in front of "DatalakeUserBasic".  Then click "Next: Tags"

![screen](images/iam16.png)

* Click "Next: Review"

* Review the information and click "Create users"

![screen](images/iam17.png)

### Create a role for use by Glue Crawler

* On the left hand column, click "Roles".  Then click "Create role" button.

* Click on Glue in the list of services that will use this role.  Then click "Next: Permissions"

![screen](images/iamglue1.png)

* In the filter field, type s3 and then check the box for "AmazonS3ReadOnlyAccess".

![screen](images/iamglue33.png)

* Now add Glue permissions, by typing glue and then checking the box for "AWSGlueServiceRole".

![screen](images/iamglue34.png)

* Click "Next: Tags"

* Click "Next: Review"

* Name the role "GlueCrawlerRole" and click "Create role"

![screen](images/iamglue2.png)

![screen](images/iamglue3.png)

## Login as the LFadmin user and setup Lake Formation

### Login as LFadmin user

* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "LFadmin" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/iam20.png)

* Navigate to the Lake Formation Console.

![screen](images/lf1.png)

* Click "Add administrators" button

Note: if you have previously setup Lake Formation in your account, you may see a different initial screen.

![screen](images/lf2.png)

* In the drop-down list for "IAM users and roles", choose the "LFadmin" user.

![screen](images/lf3.png)

* Click "Save"

![screen](images/lf4.png)

### Configure the account to use Lake Formation Security permissions

* On the left-hand column, click on "Settings"

![screen](images/lf5.png)

* Uncheck the 2 checkboxes.  Then click "Save"

![screen](images/lf6.png)

### Register S3 locations with Lake Formation

* Click on "Dashboard" on the left hand column

![screen](images/lf8.png)

* Click on "Register location" button.  In the Amazon S3 Path, enter this value:

```
s3://us-east-1.elasticmapreduce.samples/flights/parquet/
```

* Then click "Register location" button.

![screen](images/lf9.png)

![screen](images/lf10.png)

* On the Data lake locations page, click "Register location" to add a second location.  In the Amazon S3 Path, enter this value:

```
s3://amazon-reviews-pds/parquet/
```

* Then click "Register location" button.

![screen](images/lf11.png)

![screen](images/lf12.png)

### Create databases

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

### Grant privileges on the databases to Glue Crawler

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

## Create tables by crawling our S3 locations

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

### Add another crawler for the Reviews database

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

* Wait for both crawlers to finish running.

![screen](images/lf35.png)

Notice that each crawler has added 1 table.

* Click on Tables on the left hand column of the Glue console.  

![screen](images/lf36.png)

These are the 2 tables that the crawlers created.

## Access the tables

### Try accessing the tables as the UserFlights

UserFlights has not been granted any access yet in Lake Formation, so we don't expect UserFlights to be able to query these tables.

* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "UserFlights" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/use1.png)

* Navigate to the Athena Console.

![screen](images/use2.png)

* Click Get Started

* Close the tutorial window

* In the Database drop-down, notice that UserFlights does not see the Flights or Reviews databases

![screen](images/use3.png)

### Grant permissions to our users


* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "LFadmin" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/iam20.png)

* Navigate to the Lake Formation Console.

![screen](images/lf1.png)

* On the left-hand column of the Lake Formation Console, click "Dashboard".  On the Dashboard page, click the "Grant permissions" button.

![screen](images/use4.png)

* With the "IAM users and roles" drop-down, choose "UserFlights".

![screen](images/use5.png)

* With the Database drop-down, choose "Flights"

![screen](images/use6.png)

* With the Table drop-down, choose "flights_parquet"

![screen](images/use7.png)

* For table permissions, choose "Select".  Then click the Grant button

![screen](images/use8.png)

![screen](images/use9.png)

### Grant permissions for UserAll

* Click the "Grant" button on the Data permissions page

![screen](images/use4.png)

* With the "IAM users and roles" drop-down, choose "UserAll".

![screen](images/use10.png)

* With the Database drop-down, choose "Reviews"

![screen](images/use11.png)

* With the Table drop-down, choose "reviews_parquet"

![screen](images/use12.png)

* For table permissions, choose "Select".  Then click the Grant button

![screen](images/use8.png)

#### Now do the same for the Flights database & table for UserAll

* Click the "Grant" button on the Data permissions page

![screen](images/use4.png)

* With the "IAM users and roles" drop-down, choose "UserAll".

![screen](images/use10.png)


* With the Database drop-down, choose "Flights"

![screen](images/use6.png)

* With the Table drop-down, choose "flights_parquet"

![screen](images/use7.png)

* For table permissions, choose "Select".  Then click the Grant button

![screen](images/use8.png)

### Try accessing the tables as the UserFlights

UserFlights has now been granted access to just the flights table (but not the reviews table).

* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "UserFlights" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/use1.png)

* Navigate to the Athena Console.

![screen](images/use2.png)

* Click Get Started

* Notice that you now see the Flights database and the flights_parquet table in the navigator on the left.

![screen](images/use13.png)

* In the query editor, enter this query

```
select count(*) from flights_parquet;

```

* Click "Run query"

![screen](images/use14.png)



### Try accessing the tables as the UserAll

UserAll has now been granted access to both tables.

* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "UserAll" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/use15.png)

* Navigate to the Athena Console.

![screen](images/use2.png)

* Click Get Started if needed

* Notice that you now see both the Flights and Reviews databases in the navigator on the left.

![screen](images/use16.png)

* In the query editor, enter this query

```
select count(*) from reviews.reviews_parquet;

```

* Click "Run query"

![screen](images/use17.png)

