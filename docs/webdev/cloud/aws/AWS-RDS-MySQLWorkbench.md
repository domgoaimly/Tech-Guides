## Connect to my Amazon RDS for MySQL instance by using MySQL Workbench

1. Download and install MySQL & MySQL Workbench.
   - [Windows](https://www.youtube.com/watch?v=wjTdEPvolzk)
   - [Mac](https://www.youtube.com/watch?v=DVVVSlGDpuw)
   - [Brew Install](https://www.youtube.com/watch?v=1K4m6m5y9Oo)

## Setup for public accessible RDS

_The staging database is public_

2. Open MySQL Workbench, and then choose the ⊕ sign beside MySQL Connections to set up a new connection.
<img width="1205" alt="mysqlconnection" src="https://user-images.githubusercontent.com/111775505/198582412-3bdb57a4-8283-4082-adc3-89eecb3047fd.png">

3. In the Setup New Connection dialog box, enter a name for your connection.
4. In the Parameters section, enter these details:
   - Host name: Enter the RDS endpoint
   - Port: Enter the Port number
   - Username: Enter the primary user

## Setup for private accessible RDS

_The production database is private_

2. Open MySQL Workbench, and then choose the ⊕ sign beside MySQL Connections to set up a new connection.
<img width="1164" alt="Screen Shot 2022-11-12 at 3 50 03 PM" src="https://user-images.githubusercontent.com/111775505/201496040-cdf2778d-82e6-4016-8d92-84dc7b3d990c.png">

3. In the Setup New Connection dialog box, enter a name for your connection.
4. In the Parameters section, enter these details:
   - SSH Hostname: Enter the Hostname (View the hostname in the image)
   - SSH Username: Enter ec2-user as the user name
   - SSH Password: 
     - Login to AWS console
     - Click S3 bucket
     - Find bucket name [keyexchance](https://s3.console.aws.amazon.com/s3/buckets/keyexchance?region=us-east-2)
     - Within the bucket click the download 
     - After the file is downloaded point your SSH Key File to that file
   - Host name: Enter the RDS endpoint
   - Port: Enter the Port number
   - Username: Enter the primary user

Note: You can get these details from the Amazon RDS console. From the Databases section, choose Instances, and then select the instance that you are connecting to. From the Connectivity and Security tab, choose Configuration. The primary user is listed here.

5. Choose Test Connection.
6. In the pop-up window that appears, enter the password for the DB instance, and then choose OK.
7. After testing your connection, from the Setup new connection dialog box, choose OK to save the connection.
Note: If you receive an error when you test the connection, check that you configured the network correctly or the information you entered.

## Common MySQL Workbench Use & MySQL Commands

### MySQL Workbench 

1. In the left hand corner under SCHEMAS you will see databases. Double click the 'mydb' database to select it. Once selected it will open up to show you the tables.
2. Tables are where all of the data is held. For simplicity you do not need to open the drop down of the columns inside of the table. 
   - The first button is the i (or information button). This button will given you information on the data types used in that specific column, primary keys, and general data info about the column.<br/> <img width="195" alt="Screen Shot 2022-10-28 at 7 11 54 AM" src="https://user-images.githubusercontent.com/111775505/198584117-1a559306-a6d6-47e6-8a26-76a4b954a805.png">
   - The second button is an auto generated command. This button will generate all of the data for this column. <br/><img width="196" alt="Screen Shot 2022-10-28 at 7 15 54 AM" src="https://user-images.githubusercontent.com/111775505/198584831-d89ef8ce-2b44-4f63-a4d3-cc2840b1cfca.png">

### MySQL Commands
Find a particular event inside of a column. It is used to extract only those records that fulfill a specified condition.

Samples: 

`SELECT * FROM mydb.Event
WHERE Id = 15;`

`SELECT * FROM mydb.Products
WHERE Price BETWEEN 10 AND 12;`

`SELECT * FROM mydb.Organization
WHERE City IN ('New York');`

`SELECT * FROM mydb.Organization
WHERE Country='US' AND City='Boston';`

`SELECT * FROM mydb.Organization
WHERE City='Houston' OR City='Austin';`

`SELECT * FROM mydb.Organization
WHERE NOT Country='Germany' AND NOT Country='USA';`

`SELECT * FROM mydb.Organization
WHERE Country='USA' AND (City='Cleveland' OR City='Dallas');`

`SELECT * FROM mydb.Event
ORDER BY StartDateTime;`

`SELECT * FROM mydb.Order
WHERE CompletedCheckoutDatetime IS NOT NULL;`
