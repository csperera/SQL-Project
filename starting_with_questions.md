Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SQL Queries:
SELECT city,country, SUM(totaltransactionrevenue) FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city, country
ORDER BY SUM(totaltransactionrevenue)DESC;

Answer:
not available in demo dataset	United States	6092560000
San Francisco	United States	1564320000
Sunnyvale	United States	992230000
Atlanta	United States	854440000
Palo Alto	United States	608000000


**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
SELECT city,country, AVG(transactions) FROM all_sessions
WHERE transactions IS NOT NULL
GROUP BY city, country
ORDER BY AVG(transactions);

Answer: If there is an order, it's for 1.00000000000 of the product. 

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
SELECT city,country, SUM(totaltransactionrevenue),v2productcategory FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city, country, v2productcategory
ORDER BY SUM(totaltransactionrevenue)DESC;

Answer:
Yes! The Nest/Nest-USA product category seems to be the number one seller in the majority of US cities

**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
SELECT city,country, totaltransactionrevenue,v2productname FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city, country, v2productname,totaltransactionrevenue
ORDER BY totaltransactionrevenue, v2productname, city, country;


Answer:
Yes! Nest Protect Smoke, Nest Learning Thermostat, Nest Outdoor Security Camera and Nest Indoor Security Camera are very popular.

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
SELECT city,country, totaltransactionrevenue FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city, country, totaltransactionrevenue
ORDER BY totaltransactionrevenue DESC;

Answer: yes, the majority of the revenue is from the United States, with the only foreign cities being Tel Aviv-Israel, Sydney-Australia, Toronto-Canada
and Zurich-Switzerland







