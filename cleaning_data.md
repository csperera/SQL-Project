What issues will you address by cleaning the data?

It should be noted that simply getting the .csv data into Postgresql was very difficult, and required figuring a workaround to the server conflict.
Ultimately we created a C:/temp folder, used the COPY command and managed to get the data ported into Postgresql after much difficulty.

Typically data cleaning involves:

1.Remove Unwanted or Irrelevent Observations - which we did by running an assertion "sumcheck" on all columns which appeared to be NULL

2.Ensure Accurate Datatypes - Each column was checked, and certain datatypes were changed using ALTER TABLE shown below

3.Address Missing Values - This cannot be done with certainty here, so we did not do this

4.Fixing Typos - All of the column names were changes from camel-case to all lowercase because of the issues with pgadmin4.

I believe in not skewing the data too much by "over-cleaning" so I ran data assertion checks on all columns which might be NULL values from top to bottom, hence offering no additive value to the analysis.  The following columns were NULL from top to bottom and deleted: 

Sumcheck – productrefundtamount – NULL - deleted

Sumcheck – itemquantity – NULL - deleted

Sumcheck – itemrevenue – NULL - deleted

Queries:
Below, provide the SQL queries you used to clean your data.

SELECT SUM(timeonsite) AS sumcheck FROM analytics;

ALTER TABLE analytics
ALTER COLUMN timeonsite TYPE INT 
USING timeonsite::integer;

ALTER TABLE all_sessions DROP COLUMN itemquantity;

ALTER TABLE all_sessions RENAME COLUMN old_column_name TO new_column_name; <-- THIS WAS USED 17 TIMES


