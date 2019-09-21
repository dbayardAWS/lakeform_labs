# Part 6 - Grant permissions to our users


## Use the Lake Formation administrator to grant permissions

* Use the username drop-down at the top of the AWS console page and choose "Sign Out".

![screen](images/iam18.png)

* Click the "Sign In to the Console" button

![screen](images/iam19.png)

* Enter "LFadmin" for the IAM user name.  Enter the Password you used when creating the users for the Password.  Click "Sign In"

![screen](images/iam20.png)

* Navigate to the Lake Formation Console.

![screen](images/lf1.png)



## Grant permissions for the Flights table to UserFlights

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



## Grant permissions for UserAll to the Reviews table

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



### Now do the same for the Flights table for UserAll

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




## Congratulations.

You have used granted Lake Formation security permissions to UserFlights and UserAll.  UserFlights only has permissions on the Flights table.  UserAll has permissions on both the Flights and Reviews tables.  Next, let's verify their access.

Proceed onto [Part 7](Part7.md)

