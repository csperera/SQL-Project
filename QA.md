What are your risk areas? Identify and describe them.

When validating data, we can check the following:

1. **Handling Missing Data**: Missing data can lead to incorrect conclusions. SQL provides functions such as `IS NULL` and `IS NOT NULL` to identify and handle missing data.

2. **Data Formatting**: Data comes in various formats, and it's important to standardize it for accurate analysis. For example, we may have date data in different formats that need to be unified.

3. **Identifying and Handling Duplicates**: Duplicate data can affect the accuracy of our insights. SQL's `DISTINCT` keyword is one method of identifying duplicates.

4. **Checking Data Accuracy**: The information might be complete and properly formatted, but still incorrect or unrealistic. This could be dates in the future that are not realistic, negative values where they don't make sense, etc.

5. **Data Transformation**: This process involves changing the data from its original form to a form better suited to the specific needs of our analysis.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. Handling missing data: 

We did an assertion to check if all values in a column were null, if they were (productrefundamount, itemquantity, itemrevenue) the were deleted. 

SELECT SUM('totalTransactionRevenue') AS sumcheck FROM all_sessions;

ALTER TABLE analytics
ALTER COLUMN timeonsite TYPE INT 
USING timeonsite::integer;

2. We changed the data format from VARCHAR to INT for units_sold column. 

ALTER TABLE analytics
ALTER COLUMN units_sold TYPE INT 
USING units_sold::integer;

3. Although we didn't change the data, we are aware that duplicates exist in the visitid column using this query:

SELECT visitid, COUNT(visitid) FROM all_sessions 
GROUP BY visitid 
HAVING COUNT(visitid) > 1;

4. Checking data accuracy: 

The productprice column was obviously wrong, and had to be corrected by dividing by 1000000, so this was done by adding a new column productprice2 and then
updating the new column with the corrected data 

ALTER TABLE all_sessions
ADD productprice2 real;

UPDATE all_sessions
SET productprice2 = productprice/1000000;

5. unitssold needed to be in integer form to perform calculations, so we converted that column from VARCHAR to INT. 

We changed the data format from VARCHAR to INT for units_sold column. 

ALTER TABLE analytics
ALTER COLUMN units_sold TYPE INT 
USING units_sold::integer;

It should be noted that the initial import of the csv files took the most time, because certain import methods with pgadmin did not work,
so significant time was spent figuring out what import methods worked - namely moving the data to a c:\temp drive and using the using the COPY
command and the query window in pgadmin. 







