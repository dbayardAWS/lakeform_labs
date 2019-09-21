# Part 2 - Setup Lake Formation



## Login as LFadmin user

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



## Configure the account to use Lake Formation Security permissions

* On the left-hand column, click on "Settings"

![screen](images/lf5.png)

* Uncheck the 2 checkboxes.  Then click "Save"

![screen](images/lf6.png)



## Register S3 locations with Lake Formation

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



## Congratulations.

You have done the initial setup of Lake Formation and enabled the Lake Formation security privilege system.  And you have registered the 2 S3 locations that we will use later in this lab.

Proceed onto [Part 3](Part3.md)
