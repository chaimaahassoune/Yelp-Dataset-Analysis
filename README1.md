# Part 1: Yelp Dataset Profiling and Understanding

### 1. Total Number of Records for Each Table

- Attribute table = 10000 records
- Business table = 10000 records
- Category table = 10000 records
- Checkin table = 10000 records 
- Elite_years table = 10000 records
- Friend table = 10000 records
- Hours table = 1000 records
- Photo table = 10000 records
- Review table = 10000 records
- Tip table = 10000 records
- User table = 10000 records

### 2. Total Distinct Records by Primary/Foreign Key for Each Table

- Business = 10000
- Hours = 1562
- Category = 2643
- Attribute = 1115
- Review = 10000
- Checkin = 493
- Photo = 10000
- Tip = 537 (user_id)
- User = 10000
- Friend = 11
- Elite_years = 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

### 3. Check for Null Values in Users Table

- **Are there any columns with null values in the Users table?** 
  - Answer: No

SQL code used to arrive at answer:

```sql
SELECT COUNT(*)
FROM user
WHERE id IS NULL OR 
      name IS NULL OR 
      review_count IS NULL OR 
      yelping_since IS NULL OR
      useful IS NULL OR 
      funny IS NULL OR 
      cool IS NULL OR 
      fans IS NULL OR 
      average_stars IS NULL OR 
      compliment_hot IS NULL OR 
      compliment_more IS NULL OR 
      compliment_profile IS NULL OR 
      compliment_cute IS NULL OR 
      compliment_list IS NULL OR 
      compliment_note IS NULL OR 
      compliment_plain IS NULL OR 
      compliment_cool IS NULL OR 
      compliment_funny IS NULL OR 
      compliment_writer IS NULL OR 
compliment_photos IS NULL

### 4. Statistical Summary for Specific Columns

#### Review Table
- **Column: Stars**
  - min: 1   max: 5   avg: 3.7082

#### Business Table
- **Column: Stars**
  - min: 1.0   max: 5.0   avg: 3.6549

#### Tip Table
- **Column: Likes**
  - min: 0   max: 2   avg: 0.0144

#### Checkin Table
- **Column: Count**
  - min: 1   max: 53   avg: 1.9414

#### User Table
- **Column: Review_count**
  - min: 0   max: 2000   avg: 24.2995

### 5. Cities with the Most Reviews

SQL code used to arrive at the answer:
```sql
SELECT city, SUM(Review_count) AS total_Review 
FROM Business 
GROUP BY city 
ORDER BY total_Review DESC

| city            | total_Review |
|-----------------|--------------|
| Las Vegas       | 82854        |
| Phoenix         | 34503        |
| Toronto         | 24113        |
| Scottsdale      | 20614        |
| Charlotte       | 12523        |
| Henderson       | 10871        |
| Tempe           | 10504        |
| Pittsburgh      | 9798         |
| Montréal        | 9448         |
| Chandler        | 8112         |
| Mesa            | 6875         |
| Gilbert         | 6380         |
| Cleveland       | 5593         |
| Madison         | 5265         |
| Glendale        | 4406         |
| Mississauga     | 3814         |
| Edinburgh       | 2792         |
| Peoria          | 2624         |
| North Las Vegas | 2438         |
| Markham         | 2352         |
| Champaign       | 2029         |
| Stuttgart       | 1849         |
| Surprise        | 1520         |
| Lakewood        | 1465         |
| Goodyear        | 1155         |

(Output limit exceeded, 25 of 362 total rows shown)

### 6. Distribution of Star Ratings in Different Cities

#### Avon

SQL code used to arrive at answer:
```sql
SELECT stars, SUM(review_count) AS count 
FROM business 
WHERE city = 'Avon' 
GROUP BY stars

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


#### Beachwood

SQL code used to arrive at answer:

```sql
select stars ,  
SUM (review_count) AS count 
from business 
where city = 'Beachwood'
group by stars

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

### 7. Find the top 3 users based on their total number of reviews:
SQL code used to arrive at answer:
```sql
select Name , review_count
from user 
order by review_count DESC 
LIMIT 3

+--------+--------------+
| name   | review_count |
+--------+--------------+
| Gerald |         2000 |
| Sara   |         1629 |
| Yuri   |         1339 |
+--------+--------------+
### 8. Does posing more reviews correlate with more fans?

The analysis suggests a positive correlation between a user's review activity and the quantity of fans they attract on Yelp.
However, for a more accurate understanding of the relationship, it is essential to consider the time frame or duration over which these reviews were posted.
   ```sql
select fans , review_count , Name , yelping_since
from user 
order by  fans DESC 
'''
+------+--------------+-----------+---------------------+
| fans | review_count | name      | yelping_since       |
+------+--------------+-----------+---------------------+
|  503 |          609 | Amy       | 2007-07-19 00:00:00 |
|  497 |          968 | Mimi      | 2011-03-30 00:00:00 |
|  311 |         1153 | Harald    | 2012-11-27 00:00:00 |
|  253 |         2000 | Gerald    | 2012-12-16 00:00:00 |
|  173 |          930 | Christine | 2009-07-08 00:00:00 |
|  159 |          813 | Lisa      | 2009-10-05 00:00:00 |
|  133 |          377 | Cat       | 2009-02-05 00:00:00 |
|  126 |         1215 | William   | 2015-02-19 00:00:00 |
|  124 |          862 | Fran      | 2012-04-05 00:00:00 |
|  120 |          834 | Lissa     | 2007-08-14 00:00:00 |
|  115 |          861 | Mark      | 2009-05-31 00:00:00 |
|  111 |          408 | Tiffany   | 2008-10-28 00:00:00 |
|  105 |          255 | bernice   | 2007-08-29 00:00:00 |
|  104 |         1039 | Roanna    | 2006-03-28 00:00:00 |
|  101 |          694 | Angela    | 2010-10-01 00:00:00 |
|  101 |         1246 | .Hon      | 2006-07-19 00:00:00 |
|   96 |          307 | Ben       | 2007-03-10 00:00:00 |
|   89 |          584 | Linda     | 2005-08-07 00:00:00 |
|   85 |          842 | Christina | 2012-10-08 00:00:00 |
|   84 |          220 | Jessica   | 2009-01-12 00:00:00 |
|   81 |          408 | Greg      | 2008-02-16 00:00:00 |
|   80 |          178 | Nieves    | 2013-07-08 00:00:00 |
|   78 |          754 | Sui       | 2009-09-07 00:00:00 |
|   76 |         1339 | Yuri      | 2008-01-03 00:00:00 |
|   73 |          161 | Nicole    | 2009-04-30 00:00:00 |
+------+--------------+-----------+---------------------+

### 9. Are there more reviews with the word "love" or with the word "hate" in them?

Answer: love review has 1780 , and hate has 232 . so the reviews are more with the word "love" 

   ```sql
SELECT COUNT(*) AS loveReview
FROM review 
where text like '%love%'

+-------------+
| loveReviews |
+-------------+
|        1780 |
+-------------+

   ```sql
SELECT COUNT(*) AS hateReviews
FROM review 
where text like '%hate%'
'''
	+-------------+
	| hateReviews |
	+-------------+
	|         232 |
	+-------------+

### 10. Find the top 10 users with the most fans:
SQL code used to arrive at answer:
   ```sql
SELECT id,
name,fans
FROM user
ORDER BY fans DESC
LIMIT 10
'''
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

## Part 2: Inferences and Analysis

### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
#### i. Do the two groups you chose to analyze have a different distribution of hours?
the 4-5  stars group have less houre than the 2-3 group stars
#### ii. Do the two groups you chose to analyze have a different number of reviews?
yes they have a deffirent number of review.
####  iii. Are you able to infer anything from the location data provided between these two groups? Explain.
There is a substantial amount of data available, and we cannot adequately explain or draw conclusions solely from the analysis of these two groups 
SQL code used for analysis:

   ```sql
SELECT 
b.city,
b.stars,
c.category,
h.hours,
b.review_count,
CASE
  WHEN hours LIKE "%monday%" THEN 1
  WHEN hours LIKE "%tuesday%" THEN 2
  WHEN hours LIKE "%wednesday%" THEN 3
		WHEN hours LIKE "%thursday%" THEN 4
		WHEN hours LIKE "%friday%" THEN 5
		WHEN hours LIKE "%saturday%" THEN 6
		WHEN hours LIKE "%sunday%" THEN 7
	END AS hourDistribution,
    CASE
        WHEN b.stars BETWEEN 2 AND 3 THEN '2-3 Stars'
        WHEN b.stars BETWEEN 4 AND 5 THEN '4-5 Stars'
    END AS star_category
FROM 
    business b
JOIN 
    category c ON b.id = c.business_id
JOIN 
    hours h ON b.id = h.business_id
WHERE 
    b.city LIKE 'Las%' AND c.category = 'Restaurants'
GROUP BY stars,hourDistribution
ORDER BY hourDistribution,star_category ASC


### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
#### i. Difference 1:
Businesses that remain open typically exhibit a higher average number of reviews compared to those that are closed.
Statistics reveal:

Open businesses: Average review count of 31.757
Closed businesses: Average review count of 23.198

#### i. Difference 2:
Businesses that are open tend to have a higher average star rating compared to businesses that are closed.
here are the statistics:

Open businesses: Average star rating of 3.679
Closed businesses: Average star rating of 3.520

SQL code used for analysis:
   ```sql

SELECT COUNT(DISTINCT(id)),
AVG(review_count),
SUM(review_count),
AVG(stars),
is_open
FROM business
GROUP BY is_open
'''
### 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.
#### i. Indicate the type of analysis you chose to do:
Predicting the overall star rating for a business

#### ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
It's logical to gauge the overall rating based on service quality, although we lack specific information on this aspect. 
However, leveraging the review_count column could be insightful, assuming that businesses providing excellent service tend to garner more reviews.
Furthermore, analyzing the text column in the review table might help determine whether the presence of words like "hate" and "love" in reviews serves as reliable indicators of the overall rating.
Lastly, cross-referencing these hypotheses with the stars column in the business table would be crucial to confirm or refute our assumptions
#### iii. Output of your finished dataset:

+----------------------------------------+--------------+-----------+-------+
| name                                   | review_count | sentiment | stars |
+----------------------------------------+--------------+-----------+-------+
| 4E Kennels                             |           24 | loved     |   5.0 |
| Alfred Angelo Bridal                   |           58 | loved     |   4.0 |
| Angelo's Pizza                         |          377 | loved     |   4.0 |
| AquaKnox                               |          423 | loved     |   4.0 |
| Au 14 Ouest Prince Arthur              |            4 | loved     |   5.0 |
| Au Kouign-Amann                        |          291 | loved     |   4.5 |
| AutoNation Nissan Tempe                |          157 | loved     |   3.0 |
| Avis                                   |            6 | hated     |   2.5 |
| Babe's Cabaret                         |           16 | hated     |   3.0 |
| Balance Hormone Center                 |            9 | loved     |   4.0 |
| Beaver Choice                          |          326 | loved     |   4.0 |
| Benkovitz Seafoods                     |           20 | loved     |   4.5 |
| Boba Tea House                         |          295 | loved     |   4.0 |
| Bootleggers Modern American Smokehouse |          431 | hated     |   4.0 |
| Bootleggers Modern American Smokehouse |          431 | loved     |   4.0 |
| Braddah's Island Style                 |          566 | loved     |   4.0 |
| Budget Rent A Car                      |            7 | hated     |   2.0 |
| Cabo's Cantina and Grill               |           24 | loved     |   3.5 |
| Camp Bow Wow Avondale                  |           79 | loved     |   5.0 |
| Capriotti's Sandwich Shop              |           57 | loved     |   3.0 |
| Cho Sun Ok                             |          195 | loved     |   4.0 |
| D & D Discount Motorcycles             |           11 | loved     |   5.0 |
| Delmonico Steakhouse                   |         1389 | hated     |   4.0 |
| Diablo's Cantina                       |         1084 | loved     |   3.0 |
| Dreamy Draw Recreation Area            |           45 | loved     |   4.0 |
+----------------------------------------+--------------+-----------+-------+

#### iv. Provide the SQL code you used to create your final dataset:

   ```sql

SELECT 
    b.name, b.review_count , 
    CASE 
        WHEN r.text LIKE '%hate%' THEN 'hated'
        WHEN r.text LIKE '%love%' THEN 'loved'
    END AS 'sentiment',
    b.stars
FROM business b INNER JOIN review r 
ON b.id = r.business_id
WHERE sentiment IS NOT NULL
ORDER BY name;
'''