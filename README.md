# Lake Formation Security Demonstration

This Lab demonstrates the Lake Formation security access control mechanisms.  

AWS Lake Formation uses Amazon Simple Storage Service (Amazon S3) as the underlying storage for data lakes. Instead of complex IAM or Amazon S3 policies, the Lake Formation permission model enables fine-grained access to data stored in data lakes through a simple grant/revoke mechanism. Other AWS services, such as AWS Glue, Amazon Athena, and Redshift Spectrum, honor the Lake Formation permissions for restricting access to databases, tables, and columns. 

You can find out more [here](https://docs.aws.amazon.com/lake-formation/latest/dg/access-control-overview.html).




|Part |Topic |
|---- | ----|
|1 |[Setup the Lake Formation users and the Glue Crawler role](Part1.md) |
|2 |[Setup Lake Formation](Part2.md) |
|3 |[Register S3 locations and Create databases](Part3.md) |
|4 |[Create tables by crawling S3 locations](Part4.md) |
|5 |[Access the tables (without permissions)](Part5.md) |
|6 |[Grant permissions to our users](Part6.md) |
|7 |[Access the tables (with permissions)](Part7.md) |

Note: You need to run each Part in order and complete it before moving to the next Part of the lab

