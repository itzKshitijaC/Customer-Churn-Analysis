# End to end Customer Churn analysis using MySQL and Power BI 📊

# Objective 🎯
To identify the factors contributing to churn.

# Dataset 🔤🔤
[Download Dataset from here](https://www.kaggle.com/datasets/radheshyamkollipara/bank-customer-churn)

# Data Summary 🔤

### Our dataset comprises 18 attributes. Let's comprehensively examine each one in detail.

<b>1. RowNumber: </b> corresponds to the record (row) number and has no effect on the output.

<b>2. CustomerId: </b>contains random values and has no effect on customer leaving the bank.

<b>3. Surname: </b>the surname of a customer has no impact on their decision to leave the bank.

<b>4. CreditScore: </b>can have an effect on customer churn, since a customer with a higher credit score is less likely to leave the bank.

<b>5. Geography: </b>a customer’s location can affect their decision to leave the bank.

<b>6. Gender: </b>it’s interesting to explore whether gender plays a role in a customer leaving the bank.

<b>7. Age: </b>this is certainly relevant, since older customers are less likely to leave their bank than younger ones.

<b>8. Tenure: </b>refers to the number of years that the customer has been a client of the bank. Normally, older clients are more loyal and less likely to leave a bank.

<b>9. Balance: </b>also a very good indicator of customer churn, as people with a higher balance in their accounts are less likely to leave the bank compared to those with lower balances.

<b>10. NumOfProducts: </b>refers to the number of products that a customer has purchased through the bank.

<b>11. HasCrCard: </b>denotes whether or not a customer has a credit card. This column is also relevant, since people with a credit card are less likely to leave the bank.

<b>12. IsActiveMember: </b>active customers are less likely to leave the bank.

<b>13. EstimatedSalary: </b>as with balance, people with lower salaries are more likely to leave the bank compared to those with higher salaries.

<b>14. Exited: </b>whether or not the customer left the bank.

<b>15. Complain: </b>customer has complaint or not.

<b>16. Satisfaction Score: </b>Score provided by the customer for their complaint resolution.

<b>17. Card Type: </b>type of card hold by the customer.

<b>18. Points Earned: </b>the points earned by the customer for using credit card.

# Methodology 🚂
This project involves conducting an End-to-End Customer Churn Analysis utilizing MySQL and Power BI. The churn dataset within the banking domain is cleaned and subjected to basic analysis via MySQL. Subsequently, the refined dataset is exported to Power BI for the creation of an interactive Dashboard.

# Tools Used 🔨
<b> 1. To Clean and Analyze data: </b> MySQL Workbench

<b> 2. To Create an interactive Dashboard: </b> Power BI

# Data Cleaning and Exploratory Analysis using MySQL 👩🏻‍💻
1. Create a Database

       CREATE DATABASE churn;

2. Select the Database

       use churn;

3. After importing dataset into the database, select the records from the table

       SELECT * FROM churn;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/20babb29-e9ab-44fb-837f-13bf6130ee5f">
</div>
   
4. Count of total number of records

       SELECT COUNT(*) FROM churn;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/b67e7ac0-ca3d-4d87-9704-ab9d817fda7a">
</div>


5. Description of Table

       DESCRIBE churn;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/95b570c5-eb1e-47e7-9db1-96f4a426782e">
</div>

6. Drop Unnecessary Columns as they are of no use 

       ALTER TABLE churn DROP COLUMN RowNumber, DROP COLUMN Surname, DROP COLUMN EstimatedSalary;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/cfc6acc4-6b91-4a49-a9e1-3a3f4211d955">
</div>


7. Rename Columns

       -- HasCrCard
       ALTER TABLE churn
       RENAME COLUMN HasCrCard to AvailabilityOfcard;

       -- IsActiveMember
       ALTER TABLE churn
       RENAME COLUMN IsActiveMember to Activity_Status;

       -- Exited
       ALTER TABLE churn
       RENAME COLUMN Exited to Churn_Status;

       -- Complain
       ALTER TABLE churn
       RENAME COLUMN Complain to Complain_Status;

       -- Satisfaction Score
       ALTER TABLE churn
       RENAME COLUMN `Satisfaction Score` to Satisfaction_Score;

       -- Card Type
       ALTER TABLE churn
       RENAME COLUMN `Card Type` to Card_Type;

       -- Point Earned
       ALTER TABLE churn
       RENAME COLUMN `Point Earned` to Point_Earned;

8. Drop "Point_Earned" Column

       -- Drop "Point_Earned" Table
       ALTER TABLE churn DROP COLUMN Point_Earned;

9. Changing the data type of columns "AvailabilityOfCard", "Activity_Status", "Churn_Status" and "Complain_Status" from int to text

       -- AvailabilityOfCard
       ALTER TABLE churn
       MODIFY COLUMN AvailabilityOfCard text;

       -- Activity_Status
       ALTER TABLE churn
       MODIFY COLUMN Activity_Status text;

       -- Churn_Status
       ALTER TABLE churn
       MODIFY COLUMN Churn_Status text;

       -- Complain_Status
       ALTER TABLE churn
       MODIFY COLUMN Complain_Status text;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/285de2de-d872-4bfd-8895-0b500e7d9305">
</div>

10. Replacing values in columns. In the "AvailabilityOfCard" column, 0 is replaced with "Not_Available" and 1 is replaced with "Available". In the "Activity_Status" column, 1 is replaced with "Active" and 0 is replaced with "Dormant". In "Churn_Status" column, 1 is replaced with "Churned" and 0 is replaced with "Not_Churned".

        -- Replacing values in a "AvailabilityOfCard" column. 0 is replaced with "Not_Available" and 1 is replaced with "Available"
        SET sql_safe_updates = 0;
        UPDATE churn 
        SET AvailabilityOfCard = 'Available'
        WHERE AvailabilityOfCard = 1;

        UPDATE churn 
        SET AvailabilityOfCard = 'Not_Available'
        WHERE AvailabilityOfCard = 0;

        -- Replacing values in a "Activity_Status" column. 1 is replaced with "Active" and 0 is replaced with "Dormant"
        SET sql_safe_updates = 0;
        UPDATE churn
        SET Activity_Status = 'Active'
        WHERE Activity_Status = 1;

        UPDATE churn
        SET Activity_Status = 'Dormant'
        WHERE Activity_Status = 0;

        -- Replacing values in a "Churn_Status" column. 1 is replaced with "Churned" and 0 is replaced with "Not Churned"
        SET sql_safe_updates = 0;
        UPDATE churn
        SET Churn_Status = "Churned"
        WHERE Churn_Status = 1;

        UPDATE churn
        SET Churn_Status = "Not_Churned"
        WHERE Churn_Status = 0;

        -- Replacing values in a "Churn_Status" column. 1 is replaced with "Churned" and 0 is replaced with "Not Churned"
        SET sql_safe_updates = 0;
        UPDATE churn
        SET Complain_Status = "Complain_Raised"
        WHERE Complain_Status = 1;

        UPDATE churn
        SET Complain_Status = "No_Complain_Raised"
        WHERE Complain_Status = 0;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/251a7e64-ada3-4743-bf2c-f6018ecfda7a">
</div>


11. Create a new column named "Age_Range" to categorize age values into groups.

        ALTER TABLE churn ADD COLUMN Age_bins VARCHAR(20);
        UPDATE churn
        SET Age_bins = 
        CASE 
        WHEN Age < 20 THEN '[Under 20]'
        WHEN Age BETWEEN 20 AND 39 THEN '[20-39]'
        WHEN Age BETWEEN 40 AND 59 THEN '[40-59]'
        WHEN Age BETWEEN 60 AND 79 THEN '[60-79]'
        WHEN Age >= 80 THEN "[80 and above]"
        END ;
    
<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/92acdccd-d143-48a3-8b45-d8ca3071bb06">
</div>


12. Get Distinct CreditScores

        SELECT distinct CreditScore from churn order by CreditScore desc;

13. Add a new column "Credit_type" to label CreditScores

        ALTER TABLE churn ADD COLUMN Credit_Type VARCHAR(20);
        UPDATE churn
        SET Credit_Type = 
        CASE
        WHEN CreditScore < 450 THEN 'Poor'
        WHEN CreditScore BETWEEN 450 AND 549 THEN 'Fair'
        WHEN CreditScore BETWEEN 550 AND 649 THEN 'Good'
        WHEN CreditScore BETWEEN 650 AND 749 THEN 'Very Good'
        WHEN CreditScore BETWEEN 750 AND 851 THEN 'Excellent'
        END;
    
<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/35d3fa45-7abc-4086-8bd1-d86010478c6d">
</div>

14. Change the data type of "Balance" Column

        ALTER TABLE churn
        MODIFY COLUMN Balance int;

15. Add a new column "Balance_Range"

        ALTER TABLE churn ADD COLUMN Balance_Range VARCHAR(20);
        UPDATE churn
        SET Balance_Range = 
        CASE
        WHEN Balance = 0 THEN '0'
        WHEN Balance BETWEEN 1000 AND 10000 THEN '1k-10k'
        WHEN Balance BETWEEN 10000 AND 100000 THEN '10k-100k'
        WHEN Balance BETWEEN 100000 AND 200000 THEN '100k-200k'
        WHEN Balance > 200000 THEN '>200k'
        END;

<div align='center'">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/cf00a18b-9ba4-4525-92a6-20022e280cb3">
</div>

16. 


