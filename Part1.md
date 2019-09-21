# Part1 - Setup the Lake Formation users and the Glue Crawler role

## Create the Lake Formation Administrator user

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

## Create two query users

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

![screen](images/iamglue3.png)


## Congratulations.

You have setup an IAM user to be the Lake Formation administrator.  And you have created 2 IAM users to be used as query users- we will grant them differing Lake Formation privileges in a later lab. Finally, we created a role that the Glue Crawler can use.

Proceed onto [Part 2](Part2.md)
