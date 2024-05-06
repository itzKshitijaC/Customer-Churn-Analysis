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

       CREATE DATABASE customer_churn;

2. Select a Database

       USE customer_churn;

3. Select the Records from the table
-- After importing dataset into the database, select the records from the table

       SELECT * FROM churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/bebb428d-23cd-40dd-99ea-3b86139d1949">
</div>

4. Count of Total Number of Records
   
       SELECT COUNT(*) FROM churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/b42a9cdc-7b83-4ca5-bc0b-7a1bb0101853">
</div>

5. Description of Table
   
       DESCRIBE churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/0d4e5262-1b5a-422a-9935-209bf704f075">
</div>

6. Drop Columns
-- Drop Unnecessary Columns as they are of no use 

        ALTER TABLE churn DROP COLUMN RowNumber, DROP COLUMN Surname, DROP COLUMN EstimatedSalary;

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

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/95c561f2-03ae-4a7c-a525-7825232ce921">
</div>

8. Drop Column "Point_Earned"

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

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/f57f31c9-a8ce-401b-ba32-bcff448651ca">
</div>

10. Replacing values in columns. In the "AvailabilityOfCard" column, 0 is replaced with "Not_Available" and 1 is replaced with "Available". In the "Activity_Status" column, 1 is replaced with "Active" and 0 is replaced with "Dormant". In "Churn_Status" column, 1 is replaced with "Churned" and 0 is replaced with "Not_Churned".

         -- Replacing values in a "AvailabilityOfCard" column. 0 is replaced with "Not_Available" and 1 is replaced with "Available"

          SET sql_safe_updates = 0;
          UPDATE churn
          SET AvailabilityOfCard = replace(AvailabilityOfCard, "0", "Not_Available");

          UPDATE churn
          SET AvailabilityOfCard = replace(AvailabilityOfCard, "1", "Available");


          -- Replacing values in a "Activity_Status" column. 1 is replaced with "Active" and 0 is replaced with "Dormant"
          SET sql_safe_updates = 0;
          UPDATE churn
          SET Activity_Status = replace(Activity_Status, "0", "Dormant");

          UPDATE churn
          SET Activity_Status = replace(Activity_Status, "1", "Active");


          -- Replacing values in a "Churn_Status" column. 1 is replaced with "Churned" and 0 is replaced with "Not Churned"
          SET sql_safe_updates = 0;
          UPDATE churn
          SET Churn_Status = replace(Churn_Status, "0", "Not_Churned");

          UPDATE churn
          SET Churn_Status = replace(Churn_Status, "1", "Churned");


          -- Replacing values in a "Churn_Status" column. 1 is replaced with "Churned" and 0 is replaced with "Not Churned"
          SET sql_safe_updates = 0;
          UPDATE churn
          SET Complain_Status = replace(Complain_Status, "0", "No_Complain_Raised");

          UPDATE churn
          SET Complain_Status = replace(Complain_Status, "1", "Complain_Raised");

11. Getting records where AvailabilityOfCard = "Available"

         select * from churn where AvailabilityOfCard = "Available";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/0cadc4a7-e8fa-4b05-b888-a531a2406dfc">
</div>


12. Getting records where AvailabilityOfCard = "Not_Available"

         select * from churn where AvailabilityOfCard = "Not_Available";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/a1ac5cce-6341-40db-9718-ccfe532d3fb4">
</div>


13. Getting records where Activity_Status = "Active"

         SELECT * FROM churn WHERE Activity_Status = "Active";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/f8cd6dae-72cf-4b15-8f68-f62058a0f9e9">
</div>

14. Getting records where Activity_Status = "Dormant"

         SELECT * FROM churn WHERE Activity_Status = "Dormant";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/e0a9f1cb-8a20-4565-8348-a0146571ab72">
</div>

15. Getting records where Churn_Status = "Not_Churned"

         SELECT * FROM churn WHERE Churn_Status = "Not_Churned";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/9954ca23-d457-4b27-a9ff-73b0e24fc646">
</div>


16.  Getting records where Churn_Status = "Churned"

         SELECT * FROM churn WHERE Churn_Status = "Churned";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/25451d5f-fee5-4283-9a85-17f4766647c6">
</div>

17. 









