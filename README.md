# SQL-Projects

Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table = 10,000 
ii. Business table = 10,000
iii. Category table = 10,000
iv. Checkin table = 10,000
v. elite_years table = 10,000
vi. friend table = 10,000
vii. hours table = 10,000
viii. photo table = 10,000 
ix. review table = 10,000 
x. tip table = 10,000 
xi. user table = 10,000 
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10,000
ii. Hours = 1,562
iii. Category = 2,643
iv. Attribute = 1,115
v. Review = id (10,000), business_id (8,090), user_id (9,581)
vi. Checkin = 493
vii. Photo = id (10,000), business_id (6,493)
viii. Tip = user_id (537), business_id (3,979)
ix. User = 10,000
x. Friend = 11
xi. Elite_years = 2,780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer:
	
	
	SQL code used to arrive at answer:

SELECT COUNT(*)
FROM user
WHERE id IS NULL OR name IS NULL OR review_count IS NULL OR 
yelping_since IS NULL OR useful IS NULL OR funny IS NULL OR 
cool IS NULL OR fans IS NULL OR average_stars IS NULL OR 
compliment_hot IS NULL OR compliment_more IS NULL OR compliment_profile IS NULL OR 
compliment_cute IS NULL OR compliment_list IS NULL OR compliment_note IS NULL OR 
compliment_plain IS NULL OR compliment_cool IS NULL OR compliment_funny IS NULL OR 
compliment_writer IS NULL OR compliment_photos IS NULL
	
	

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min:1		max:5		avg:3.71
		
	
	ii. Table: Business, Column: Stars
	
		min:	1	max:	5	avg: 3.65
		
	
	iii. Table: Tip, Column: Likes
	
		min:0		max:	2	avg:.014
		
	
	iv. Table: Checkin, Column: Count
	
		min:	1	max:	53	avg:1.94
		
	
	v. Table: User, Column: Review_count
	
		min:	0	max:200		avg:24.3
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	
SELECT city, SUM(review_count) AS count_reviews
FROM business
GROUP BY city
ORDER BY count_reviews DESC	

	Copy and Paste the Result Below:
	
+-----------------+---------------+
| city            | count_reviews |
+-----------------+---------------+
| Las Vegas       |         82854 |
| Phoenix         |         34503 |
| Toronto         |         24113 |
| Scottsdale      |         20614 |
| Charlotte       |         12523 |
| Henderson       |         10871 |
| Tempe           |         10504 |
| Pittsburgh      |          9798 |
| Montréal        |          9448 |
| Chandler        |          8112 |
| Mesa            |          6875 |
| Gilbert         |          6380 |
| Cleveland       |          5593 |
| Madison         |          5265 |
| Glendale        |          4406 |
| Mississauga     |          3814 |
| Edinburgh       |          2792 |
| Peoria          |          2624 |
| North Las Vegas |          2438 |
| Markham         |          2352 |
| Champaign       |          2029 |
| Stuttgart       |          1849 |
| Surprise        |          1520 |
| Lakewood        |          1465 |
| Goodyear        |          1155 |
+-----------------+---------------+
	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:

SELECT stars,
SUM(review_count) AS count
FROM business
WHERE city == 'Avon'
GROUP BY stars

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):

+-------+-------+
| stars | count |
+-------+-------+
|   1.5 |    10 |
|   2.5 |     6 |
|   3.5 |    88 |
|   4.0 |    21 |
|   4.5 |    31 |
|   5.0 |     3 |
+-------+-------+

ii. Beachwood

SQL code used to arrive at answer:

SELECT stars,
SUM(review_count) AS count
FROM business
WHERE city == 'Beachwood'
GROUP BY stars

Copy and Paste the Resulting Table Below (2 columns â€“ star rating and count):
		
+-------+-------+
| stars | count |
+-------+-------+
|   2.0 |     8 |
|   2.5 |     3 |
|   3.0 |    11 |
|   3.5 |     6 |
|   4.0 |    69 |
|   4.5 |    17 |
|   5.0 |    23 |
+-------+-------+

7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:

SELECT id, name, review_count
FROM user
ORDER BY review_count DESC
LIMIT 3	
		
	Copy and Paste the Result Below:
		
+------------------------+--------+--------------+
| id                     | name   | review_count |
+------------------------+--------+--------------+
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald |         2000 |
| -3s52C4zL_DHRK0ULG6qtg | Sara   |         1629 |
| -8lbUNlXVSoXqaRRiHiSNg | Yuri   |         1339 |
+------------------------+--------+--------------+

8. Does posing more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:
	
Not necessaritly, there are many people will fewer reviews that have more fans than people with more reviews posted.
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: Love

	
	SQL code used to arrive at answer:

SELECT COUNT(*)								
FROM review							
WHERE text LIKE "%love%"						
= 1780	

SELECT COUNT(*)								
FROM review							
WHERE text LIKE "%hate%"						
= 232
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	
SELECT id, name, fans
FROM user
ORDER BY fans DESC
	
	Copy and Paste the Result Below:

+------------------------+-----------+------+
| id                     | name      | fans |
+------------------------+-----------+------+
| -9I98YbNQnLdAmcYfb324Q | Amy       |  503 |
| -8EnCioUmDygAbsYZmTeRQ | Mimi      |  497 |
| --2vR0DIsmQ6WfcSzKWigw | Harald    |  311 |
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |  253 |
| -0IiMAZI2SsQ7VmyzJjokQ | Christine |  173 |
| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |  159 |
| -9bbDysuiWeo2VShFJJtcw | Cat       |  133 |
| -FZBTkAZEXoP7CYvRV2ZwQ | William   |  126 |
| -9da1xk7zgnnfO1uTVYGkA | Fran      |  124 |
| -lh59ko3dxChBSZ9U7LfUw | Lissa     |  120 |
+------------------------+-----------+------+
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?

Yes, they do.

ii. Do the two groups you chose to analyze have a different number of reviews?
         
Yes, they do.
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.

No, there are only two Food places in Toronto in the data set. While the better reviewed restaurant has less hours, there isn't enough data to form a conclusion.

SQL code used for analysis:

SELECT B.name, B.review_count, H.hours,
postal_code, 
CASE
	WHEN hours LIKE 'Mon%' THEN 1
	WHEN hours LIKE 'Tues%' THEN 2
	WHEN hours LIKE 'Wed%' THEN 3
	WHEN hours LIKE 'Thurs%' THEN 4
	WHEN hours LIKE 'Fri%' THEN 5
	WHEN hours LIKE 'Sat%' THEN 6
	WHEN hours LIKE 'Sun%' THEN 7
END AS DAILY,
CASE
	WHEN B.Stars BETWEEN 2 AND 3 THEN '2-3 Star'
	WHEN B.Stars BETWEEN 4 AND 5 THEN '4-5 Star'
END AS Rating
FROM Business b INNER JOIN Hours H
ON B.ID = H.Business_ID
INNER JOIN Category c ON C.Business_ID = B.ID
WHERE (B.city = 'Toronto') AND (C.Category = 'Food')
GROUP BY Rating
ORDER BY Rating ASC		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1: Open businesses have higher review counts (31.76 vs 23.20)
         
         
ii. Difference 2: Open business have higher ratings (3.68 vs 3.52), though it's not much different.
         
         
         
SQL code used for analysis:

SELECT COUNT(DISTINCT(id)), AVG(Review_Count), SUM(Review_Count),AVG(Stars), is_open
FROM Business
GROUP BY is_open	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         
Review by category of food, if 'food' category has different reviews than 'soul food'
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
                           
I would like to see if more specific keywords offer a higher overall review because reviewers and other customers have a better idea of the type of food the business has, boosting 
overall satisfaction of customers.
                  
iii. Output of your finished dataset:
         
+------------+---------------+---------------------+
| category   |  AVG(b.Stars) | AVG(b.Review_Count) |
+------------+---------------+---------------------+
| Food       | 3.78260869565 |       77.4347826087 |
| Sandwiches |        3.9375 |              121.75 |
+------------+---------------+---------------------+
         
iv. Provide the SQL code you used to create your final dataset:

SELECT C.Category, AVG(b.Stars), AVG(b.Review_Count)
FROM Business b INNER JOIN Category c on C.Business_ID = B.ID
GROUP BY Category
HAVING C.Category IN ('Food', 'Sandwiches');
