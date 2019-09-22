# Part 1 - Setup the Lake Formation users and the Glue Crawler role


For this lab, we will create a number of IAM users to be able to demonstrate different levels of access when they use Lake Formation and the related services like Athena.  In addition, we will use the Glue Crawler in this lab, so we will create a role that provides the permissions that the crawler will need.


## Create the Lake Formation Administrator user

First, we will create a user who will be our Lake Formation administrator.  For this lab, she will have the overall acount AdministratorAccess policy.  If you wanted to use a smaller set of permissions, you can refer to the [Lake Formation documentation](https://docs.aws.amazon.com/lake-formation/latest/dg/permissions-reference.html#persona-dl-admin) for specifcs.


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

Once your user is created, you should see a screen like this:

![screen](images/iam5.png)



## Create two query users

Next, we will create two new users ("UserFlights" and "UserAll") to run queries.  In a later section of the lab, we will grant each user different Lake Formation permissions and demonstrate their different levels of access.


* Click the "Add user" button 


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

To read more about creating Lake Formation query users and what the above policy does, go [here](https://docs.aws.amazon.com/lake-formation/latest/dg/tut-create-lf-user.html)


![screen](images/iam11.png)

* Click "Review policy" button at the bottom of the Create policy page.

* Name the policy "DatalakeUserBasic" and click "Create policy"

![screen](images/iam12.png)

* You should see that the policy has been created.  

![screen](images/iam13.png)

* Now go back to the previous browser tab where you were creating the 2 query users.

![screen](images/iam14.png)

* Clear out the search field and type in "Datalake".  Then click on the Refresh button to the right of the "Create policy" button.  A picture of the Refresh button is shown below:

![screen](images/iam15.png)

* Check the box in front of "DatalakeUserBasic".  Then click "Next: Tags"

![screen](images/iam16.png)

* Click "Next: Review"

* Review the information and click "Create users"

![screen](images/iam17.png)

## Create a role for use by Glue Crawler

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


Once the role is created, you should a screen like this:

![screen](images/iamglue3.png)


## Congratulations.

You have setup an IAM user to be the Lake Formation administrator.  And you have created two IAM users to be used as query users- we will grant them differing Lake Formation privileges in a later part of the lab. Finally, we created a role that the Glue Crawler can use.

Proceed onto [Part 2](Part2.md)
