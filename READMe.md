
# Workshop: Connecting Autonomous Transaction Processing with OIC

![](screenshots/general/2.png)

## Introduction

This lab will teach you how to make an integration with Oracle’s ATP database, using the Oracle Integration Cloud, OIC. The integration will allow a web page to query information in the ATP database and write new information to a table.

## Prequisites
	1. OIC instance 
	2. ATP instance
		- with a Cloud Wallet
	3. Visual Builder Cloud Service, VBCS, app
      - the file to import is in the folder with this lab, it is a zip file called "ATPWorkshop.zip"
	4. Generic REST adapter

For this lab, your instructors will have the above items procured for you.

## Lab 100: Introduction to OIC

[Introduction to Oracle Integration Cloud](https://github.com/KseniiaRyuma/HCM_to_EBS_integration/blob/master/oic100.md)

This lab walks through how to spin up an OIC instance and other basics. It also goes through another use case. 

### Notes for instructors

### **STEP 1**: These tables need to be created within the ATP instance

Copy the commands below and run them in SQL Developer

```
CREATE TABLE Market (
   id NUMBER GENERATED ALWAYS as IDENTITY(START with 1 INCREMENT by 1),
   name VARCHAR2(255),
   client VARCHAR2(255),
   zipcode VARCHAR2(255),
   salesrepname VARCHAR2(255),
   salesrepemail VARCHAR2(255)
);
```
```
CREATE TABLE Opportunity (
   id NUMBER GENERATED ALWAYS as IDENTITY(START with 1 INCREMENT by 1),
   name VARCHAR2(255),
   client VARCHAR2(255),
   region VARCHAR2(255),
   country VARCHAR2(255),
   state VARCHAR2(255),
   city VARCHAR2(255),
   Address VARCHAR2(255),
   zipcode VARCHAR2(255),
   timeentered VARCHAR2(255)
);
```

### **STEP 2**: The Market table is going to need one value inserted, with a zipcode of 12345. 

```
INSERT INTO MARKET (name, client, zipcode, salesrepname, salesrepemail) VALUES (
'Market A', 'Client A', '12345', 'Robert Spaulding', 'robert.spaulding@website.com');
```

### **STEP 3**: The database will need the following stored procedure created: 
```
create or replace PROCEDURE GET_MARKET
(
   p_zipcode IN VARCHAR2,
   p_clientName OUT VARCHAR2,
   p_marketName OUT VARCHAR2,
   p_salesRepName OUT VARCHAR2,
   p_salesRepEmail OUT VARCHAR2
)
AS
BEGIN
   SELECT name, client, salesRepName, salesRepEmail INTO p_marketName, p_clientName, p_salesRepName, p_salesRepEmail FROM Market WHERE Market.zipcode = p_zipcode;
END;
```







