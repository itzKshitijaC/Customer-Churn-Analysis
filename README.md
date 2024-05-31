# Cleaning | Exploratory Analysis | Report building

# Objective 🎯
To identify the factors contributing to churn.

# Dataset 🔤
[Download Dataset from here](https://www.kaggle.com/datasets/radheshyamkollipara/bank-customer-churn)

# Data Summary 🔍

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

# Tools Used 🔨
<b> 1. To Clean and Analyze data: </b> MySQL Workbench

# Data Cleaning and Exploratory Analysis using MySQL 👩🏻‍💻

1. Create a Database

       CREATE DATABASE customer_churn;

2. Select a Database

       USE customer_churn;

3. Select the Records from the table

After importing dataset into the database, select the records from the table

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
   
Drop Unnecessary Columns as they are of no use 

        ALTER TABLE churn DROP COLUMN RowNumber, DROP COLUMN Surname, DROP COLUMN EstimatedSalary;

8. Rename Columns

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

17. Getting records where Complain_Status = "No_Complain_Raised"

              SELECT * FROM churn WHERE Complain_Status = "No_Complain_Raised";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/51b20af1-8405-42b4-8028-35d6ba0f1c59">
</div>

18. Getting records where Complain_Status = "Complain_Raised"

              SELECT * FROM churn WHERE Complain_Status = "Complain_Raised";

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/1e9f6873-a0bc-416a-b976-dd91e4e21e93">
</div>

19. Create a new column named "Age_grps" to categorize age values into groups.

        SET sql_safe_updates = 0;
        ALTER TABLE churn ADD COLUMN Age_grps VARCHAR(20);
        UPDATE churn
        SET Age_grps = 
        CASE 
        WHEN Age < 20 THEN '[Under 20]'
        WHEN Age BETWEEN 20 AND 39 THEN '[20-39]'
        WHEN Age BETWEEN 40 AND 59 THEN '[40-59]'
        WHEN Age BETWEEN 60 AND 79 THEN '[60-79]'
        WHEN Age >= 80 THEN "[80 and above]"
        END ;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/bcce6ecf-2a9c-415b-a028-bbc3f99d5657">
</div>

20. Get Distinct CreditScores

              SELECT distinct CreditScore from churn order by CreditScore desc;

21.  Add a new column "Credit_type" to label CreditScores

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
     
<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/8908e9ce-ad75-43e2-914a-ec205965168c">
</div>

22. Change the data type of "Balance" Column

              ALTER TABLE churn
              MODIFY COLUMN Balance int;
    
24. Add a new column "Balance_Range"
    
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

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/20202291-92f5-4d73-b92b-107e0be38ea8">
</div>

25. Getting Distinct Geography

              SELECT DISTINCT Geography from churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/eed144d1-0792-4cde-b75f-ca88acc91f24">
</div>

26. Calculating Total Customers

              SELECT COUNT(CustomerId)  AS Total_Customers FROM churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/47d60c55-8aac-4ed7-962a-fa6279775c49">
</div>

27. Calculating Active Customers

      SELECT COUNT(*) AS ActiveCustomers FROM churn WHERE Activity_Status = 'Active';

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/edc7eb7a-a3e5-458c-8658-6ee89f5f4785">
</div>

28. Calculating Inactive Customers

              SELECT COUNT(*) AS InactiveCustomers FROM churn WHERE Activity_Status = 'Dormant';

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/f1b6e112-5eb9-4401-866f-bc763112b924">
</div>

29. Calculating the total number churned customers

              SELECT COUNT(*) AS ChurnedCustomers FROM churn WHERE Churn_Status = 'Churned';
    
<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/efcced1c-12d9-4e94-b650-a12ccc19d64e">
</div>

31. Calculating the total number retained customers

              SELECT COUNT(*) AS RetainedCustomers FROM churn WHERE Churn_Status = 'Not_Churned';

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/56883bbc-a8da-479c-8d30-6eee06f0555c">
</div>

32. Calculating the total number of customers who raised complaints

              SELECT COUNT(*) AS ComplainRaised FROM churn WHERE Complain_Status = 'Complain_Raised';

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/dca3fc62-3d50-477b-8dc1-1aedf2a7e26d">
</div>

33. Calculating the total number of customers who do not raised complaints

              SELECT COUNT(*) AS NoComplainRaised FROM churn WHERE Complain_Status = 'No_Complain_Raised';

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/105369e9-042e-4a7e-adb8-efc19ebc6cc1">
</div>

34. What are the different Card Types?

              SELECT DISTINCT Card_Type AS CardType FROM churn;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/9b6aab2a-41c1-42c3-8f84-8f9c57dafcdb">
</div>

35. Gender wise Customer Churn Status

              SELECT Gender, Count(Gender) AS ChurnNumber
              FROM churn WHERE Churn_Status = 'Churned'
              Group by Gender;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/f4624a18-9433-4abc-829a-2db3eff2ac2b">
</div>

36. Which Age Group customers are more likely to churn?

              SELECT Age_grps, Count(Age_grps) AS AgeGrpsChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group by Age_grps;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/300d4f6d-aa3c-42c3-88bb-068b3aaec281">
</div>

37. In which Balance Range are customers more prone to churn?

              SELECT Balance_Range, Count(Balance_Range) AS BalanceChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Balance_Range;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/48b68f98-32cb-4ff2-ad45-2b8fc40e56bd">
</div>

38.  Which credit type of customers most likely to churn with?

              SELECT Credit_Type, Count(Credit_Type) AS CreditTypeChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Credit_Type
              ORDER BY CreditTypeChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/40985ed2-5530-4d47-9da7-7f5ba58393df">
</div>

39. Customers with which Card type are more likely to churn?

              SELECT Card_Type, Count(Card_Type) AS CardTypeChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Card_Type
              ORDER BY CardTypeChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/fab9baee-9a4f-4e38-af8c-a2d66708f9db">
</div>

40. Are customers who frequently raise complaints more prone to churning?

              SELECT Complain_Status, Count(Complain_Status) AS ComplainStatusChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Complain_Status
              ORDER BY ComplainStatusChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/c72adccc-044e-4857-a240-b7261c7f43c5">
</div>


41. Are customers with a Dormant Activity Status more prone to churning?

              SELECT Activity_Status, Count(Activity_Status) AS ActivityStatusChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Activity_Status
              ORDER BY ActivityStatusChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/faf3402d-ee7b-4011-a0b0-6b395c04ff6c">
</div>

42.  Are customers without Credit Cards more prone to churning?

              SELECT AvailabilityOfCard, Count(AvailabilityOfCard) AS AvailCardChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY AvailabilityOfCard
              ORDER BY AvailCardChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/27cb085e-5ab3-4a35-8e6f-a5e693719530">
</div>

43. Do customers who purchase the minimum number of products tend to churn more frequently?

              SELECT NumOfProducts, Count(NumOfProducts) AS NumOfProductsChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY NumOfProducts
              ORDER BY NumOfProductsChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/03212357-e33d-4432-a004-bbd180e7b5dd">
</div>

44. Are customers with minimum tenure more likely to churn?

              SELECT Tenure, Count(Tenure) AS TenureChurnNum
              FROM churn
              WHERE Churn_Status = 'Churned'
              Group BY Tenure
              ORDER BY TenureChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/edca3882-fe51-43a9-8a7f-ff6c1b85e462">
</div>

45. Which location's customers experienced higher churn rates?

              SELECT Geography,
              Count(Geography) AS GeographyChurnNum
              FROM churn WHERE Churn_Status = 'Churned'
              Group BY Geography
              ORDER BY GeographyChurnNum
              DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/d951ae6a-6e5a-4579-bd0a-43de6e33484b">
</div>

46. Which gender raised more complaints, male or female, and which gender exhibited a higher churn rate?

              SELECT Gender, Count(Gender) AS GenderComplainChurn
              FROM churn
              WHERE Complain_Status = 'Complain_Raised' AND Churn_Status = 'Churned'
              Group By Gender
              Order by GenderComplainChurn DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/118c38d4-d69e-4de2-9c81-49536756a80b">
</div>

47. Geography wise higher churn Status of Gender

              SELECT Geography,Gender,
              Count(Geography) AS GeographyGenderChurn
              FROM churn
              WHERE Churn_Status = 'Churned'
              Group by Geography
              Order By GeographyGenderChurn DESC;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/cc21dbaf-e58f-42d3-bca7-fc73633338b0">
</div>

48. Which geographical region has a larger customer base?

              SELECT Geography,
              COUNT(CustomerId) AS TotalCustomers
              from churn
              group by Geography
              order by TotalCustomers;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/9cc344fc-4265-47cb-a4d4-83b76c62d61a">
</div>

49. How does a Gender distribution of Churned Customers vary across Geographical ragions?

              SELECT Geography, Gender, Count(*) as ChurnedCount
              FROM churn
              WHERE Churn_Status = 'Churned'
              GROUP BY Geography, Gender
              ORDER BY Geography;

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/12e1d60f-b480-4c55-b419-4d2fd0a92ab9">
</div>

50. What is the Age Distribution of churned Customers in different Geographical regions?

              SELECT Geography, Age_grps, Gender, COUNT(*) as count
              FROM churn
              WHERE Churn_Status = 'Churned'
              GROUP BY Geography,Age_grps, Gender
              ORDER BY Geography,Age_grps, Gender

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/3bc74a72-81d7-4680-bdff-c628ee596a64">
</div>

# Report Building using PowerBI

# Key Findings ✨

- The total number of customers is 10,000.

- Among the total customers, 5,151 are active, while the rest are inactive.

- Out of 10,000 customers, 2,038 churned, constituting a churn rate of 20.38%.

- Customers in the age group 40-59 are more likely to churn, followed by those in the age range 20-39.

- Surprisingly, customers with a balance range of 100k-200k were found to have the highest churn rate.

- Customers with a credit score in the range of 550 – 649, categorized as "Good" credit type, are the most prone to churning, followed by those with "Very Good" and "Excellent" credit types.

- Customers with Diamond card type are more likely to churn, followed by Platinum and Silver.

- Customers with Dormant status are more prone to churning.

- Surprisingly, customers with credit cards contributed the most to the churn rate.

- Customers who purchased the minimum number of products exhibited the highest churn rate.

- Observation suggests that tenure has no correlation with churn rate; even customers with 9 years of tenure contributed exceptionally high to the churn rate.

- The highest churn rate was observed in Germany, followed by France and Spain.

- Female customers raised the most complaints, resulting in a higher churn rate compared to male customers.
