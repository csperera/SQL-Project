Question 1: find the total number of unique visitors (fullVisitorID)

SQL Queries:

SELECT DISTINCT fullvisitorid from all_sessions; 

Answer: There are 14223 unique visitors

Question 2: find all duplicate visits

SQL Queries:

SELECT visitid, COUNT(visitid)
FROM all_sessions
GROUP BY visitid
HAVING COUNT(visitid) > 1;

Answer: 

553 visitid's have been counted twice, so it's highly likely that total visits have been overestimated by this amount

Question 3: find the total number of unique visitors by referring sites

SQL Queries:

SELECT DISTINCT fullvisitorid from all_sessions
WHERE channelgrouping = 'Referral'; 

Answer:

There are 2,419 unique visitors from "Referral" sites. 

Question 4: find each unique product viewed by each visitor

SQL Queries:

SELECT DISTINCT fullvisitorid, v2productname from all_sessions;

Answer:

There are 15115 unique visits viewing a unique product

Question 5: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries: 
SELECT DISTINCT fullvisitorid from all_sessions
WHERE totaltransactionrevenue IS NOT NULL;

Answer:
There are 80 unique visitors who purchase something 
Divided by   14,223 unique visitors, so only 0.5624% of visitors buy something! 
