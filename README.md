# End to End-to-end customer Churn Analysis using Power BI 📊

<div align="center">
  <img src="https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/332c5e0d-6500-477a-8398-1503488681de" alt="Description" width="900" height="500">
</div>

## The purpose of this project is to provide an end-to-end Business Analysis Solution to minimize Customer Attrition in the Banking Sector

# Table of Contents 🔍
- [Demo-Preview](#Demo-Preview)
- [Business Case](#Business-Case)
- [Data Source](#Data-Source)
- [Data Summary](#Data-Summary)
- [Exploratory Analysis](#Exploratory-Analysis)
- [DAX](#DAX)
- [Dashboarding](#Dashboarding)
- [Conclusion](#Conclusion)

# Demo Preview 📈
Here's a glimpse of the final report.

# Business Case 💼

### Business Case for Customer Churn Analysis in Banking

<b>1. Introduction: </b>
1. In the highly competitive banking industry, retaining customers is crucial for long-term success. Customer churn analysis helps identify patterns and reasons why customers leave, enabling proactive measures to 
   improve retention.

<b>2. Objectives: </b>

1. Identify factors contributing to customer churn.
2. Predict customers at high risk of leaving.
3. Develop strategies to reduce churn and improve customer loyalty.

<b>3. Benefits: </b>

1. Increased Retention: By understanding why customers leave, banks can implement targeted retention strategies, reducing churn rates.
2. Cost Savings: Acquiring new customers is more expensive than retaining existing ones. Reducing churn leads to significant cost savings.
3. Improved Customer Experience: Insights from churn analysis can enhance customer service and product offerings.
4. Revenue Growth: Retaining customers longer increases lifetime value, boosting revenue.

<b>4. Expected Outcomes: </b>
1. A comprehensive understanding of churn drivers
2. A predictive model with high accuracy in identifying at-risk customers.
3. It tailored retention strategies that effectively reduce churn rates.

# Data Gathering 🔠
Please use the following data assets to pull the data related to Bank customers and associated details.

o	ActiveCustomer 

o	Bank_Churn

o	CreditCard

o	CustomerInfo

o	ExitCustomer

o	Gender

o	Geography

# Data Summary 🔠

<b>1. RowNumber—</b> corresponds to the record (row) number and does not affect the output.

<b>2. CustomerId—</b> contains random values and does not affect customers leaving the bank.

</b>3. Surname—</b> A customer's surname has no impact on their decision to leave the bank.

</b>4. CreditScore—</b>can affect customer churn since a customer with a higher credit score is less likely to leave the bank.
<b>Credit score: </b>
•	Excellent: 800–850

•	Very Good: 740–799

•	Good: 670–739

•	Fair: 580–669

•	Poor: 300–579

</b>5. Geography—</b> A customer’s location can affect their decision to leave the bank.

</b>6. Gender—</b> It’s interesting to explore whether gender plays a role in a customer leaving the bank.

</b>7. Age—</b> This is certainly relevant since older customers are less likely to leave their bank than younger ones.

</b>8. Tenure—</b> refers to the number of years that the customer has been a bank client. Normally, older clients are more loyal and less likely to leave a bank.

</b>9. Balance—</b> is also a very good indicator of customer churn, as people with a higher balance in their accounts are less likely to leave the bank than those with lower balances.

<b>10. NumOfProducts—</b>refers to the number of products a customer purchases through the bank. 

<b>11. HasCrCard—</b> denotes whether or not a customer has a credit card. This column is also relevant since people with credit cards are less likely to leave the bank.

•	1 represents credit card holder

•	0 represents non credit card holder

<b>12. IsActiveMember—</b> Active customers are less likely to leave the bank.

•	1 represents Active Member

•	0 represents Inactive Member

<b>13. Estimated Salary—</b> As with balance, people with lower salaries are more likely to leave the bank compared to those with higher salaries.
Exited—whether or not the customer left the bank.

• 0 represents Retain 

• 1 represents Exit

</b>14. Bank DOJ — </b> date when the Customer associated/joined  with the bank.

# Data Modelling 🔍
Data Modelling is creating a relationship between the tables i.e. fact tables and Dimension tables. 

![Screenshot 2024-07-01 215558](https://github.com/itzKshitijaC/Customer-Churn-Analysis/assets/168798073/70a0ea5c-043a-4f1f-b51e-695a5cff7534)


# Data Analysis Expressions (DAX) ⚡

1. DateMaster Table

        Datemaster = CALENDAR(FIRSTDATE(Bank_Churn[Bank DOJ]),LASTDATE(Bank_Churn[Bank DOJ]))

2. Create a Year column from the "DateMaster" table

        year = YEAR(Datemaster[Date])

3. Create a Month column from the "DateMaster" table

        Month = MONTH(Datemaster[Date])

4. Create a Month Name column from the "DateMaster" table

        Month Name = FORMAT(Datemaster[Date], "MMM")

5. Create a measure to calculate active customers

        Active Customers = CALCULATE(COUNT(Bank_Churn[CustomerId]), ActiveCustomer[ActiveCategory]="Active Member")

6. Create a measure to calculate total customers

        Total Customers = CALCULATE(COUNT(Bank_Churn[CustomerId]))

7. Create a measure to calculate inactive customers

        Inactive Customers = [Total Customers]-[Active Customers]

8. Create a measure to calculate the number of Credit Card holders

        Credit Card Holders = CALCULATE(COUNT(Bank_Churn[CustomerId]),CreditCard[Category]="credit card holder")

9. Create a measure to calculate the number of Non-Credit Card holders

        Non Credit Card Holders = CALCULATE(COUNT(Bank_Churn[CustomerId]),CreditCard[Category]="non credit card holder")

10. Create a measure to calculate the number of Exit customers

        Exit Customers = CALCULATE([Total Customers], ExitCustomer[ExitCategory]="Exit")

11. Create a measure to calculate the number of Retain Customers

        Retain Customers = CALCULATE([Total Customers], ExitCustomer[ExitCategory]="Retain")

12. Define the Credit type based on the Credit score

        credit type = SWITCH(true(), Bank_Churn[CreditScore]>=800 && Bank_Churn[CreditScore]<=850, "Excellent",
        Bank_Churn[CreditScore]>=740 && Bank_Churn[CreditScore]<=799, "very good", 
        Bank_Churn[CreditScore]>=670 && Bank_Churn[CreditScore]<=739, "good",
        Bank_Churn[CreditScore]>=580 && Bank_Churn[CreditScore]<=669, "Fair",
        Bank_Churn[CreditScore]>=300 && Bank_Churn[CreditScore]<=579, "Poor")

13. Formula to calculate the Previous month's exit customers

        previous month exit customers = CALCULATE([Exit Customers], PREVIOUSMONTH(Datemaster[Date]))

14. 
