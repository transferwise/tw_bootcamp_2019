# Bootcamp linker

## Context

At TransferWise, we deal with lots of banks and customers. When a customer wants to make an international transfer with TransferWise, they have to do the following:

- set up a transfer request on our website
- fund the transfer via their online bank

The Linker is in charge of matching these incoming customer funds to the transfer request they have set up on our website.

## How does it work?

The Linker compares the bank statement of our banking partner to the transfer request records in our database. If the records on our bank statement matches the records in our database, we have a match. Your job is to create a matching algorithm (see matching rules at the end).

Incoming bank statements (people paying into transferwise bank accounts) look like this:

| id           | first_name | last_name | account_nr                        | amount | currency | comment | 
|--------------|------------|-----------|-----------------------------------|--------|----------|---------| 
| a1TVPS+joiQ= | Beebe      | Aarika    | FR19-2312-9002-35GW-20YN-STX5-095 | 282.0  | CNY      | P663    | 
| dtlhn%8w48wh | Anett      | Smith     | FR19-2312-1238-G345-6BRR-EGE5-373 | 770.0  | CNY      | P440    | 

*_Filename: src/main/resources/ex_bankstatement.csv_*

The transfer request records in our database look like this:

| id           | first_name | last_name | amount | currency | comment | recipient | 
|--------------|------------|-----------|--------|----------|---------|-----------| 
| WlQ5WsLH+fU= | Beebe      | Aarika    | 282.0  | CNY      | P663    | 37        | 
| HRS4e444h6q= | Joe        | Smith     | 770.0  | CNY      | P444    | 426       | 

*_Filename: src/main/resources/ex_transfer.csv_*


## The task

Your task is to read in the two files, creating a resulting file that looks like:

| bank_statement_id |  transfer_id  |  confidence | 
|-------------------|---------------|-------------| 
| a1TVPS+joiQ=      |  WlQ5WsLH+fU= | match       | 
| dtlhn%8w48wh      |  HRS4e444h6q= | proposed    | 

## We require the following rules for calculating the confidence field

 - If all records are identical = "**match**"
 - If all records have only letter case differences (case-insensitive match) = "**match**"
 - If 1 record is different (like title, comment) = "**high**"
 - If 2 records are different = "**proposed**"
 - If none of the above match = "**none**"

## Submitting your solution and source files

- Download this template
- Implement your solution in any language (we prefer Java if possible)
- Share your source code and the solution file as `links.csv` within a zip file. **Please make sure you save it as a valid CSV file!** :slightly_smiling_face:
- Upload the zip using the upload button you should see at the end of the test
 
‼️ THE DATA IN THIS REPOSITORY IS FAKE AND GENERATED FOR THE EXERCISE NOT ACTUALL CUSTOMER DATA‼️
