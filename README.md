# Restaurant-Sale-Analysis

🍽️ Restaurant Data Analysis with SQL and User-Defined Functions

Project Overview:-

This project focuses on analyzing restaurant data using SQL, with a particular emphasis on creating and applying user-defined functions (UDFs) to transform, manipulate, and aggregate data. The goal is to extract insights such as top-rated restaurants, cuisine types, and cost analysis while performing advanced calculations like rating categorization and date extraction. The dataset consists of restaurant information, including names, cuisine types, ratings, and average costs.

Dataset:-

Data set contains single table with several columns

Orderid
RestaurantName
RestaurantType
Rating
No#of#rating
AverageCost
OnlineOrder
TableBooking
CuisinesType
Area
LocalAddress
DeliveryTime

Key Features and Tasks:-

1. Creating a User-Defined Function (UDF) for Custom String Transformation:
   
A custom SQL function was developed to append the word "Chicken" into the term "Quick Bites," transforming it into "Quick Chicken Bites."
This function was applied to identify all instances of "Quick Bites" in restaurant names or types and update them accordingly, e.g., "Quick Chicken Bites."

2. Restaurant with the Maximum Number of Ratings:
   
The function was further used to display the restaurant name and cuisine type with the highest number of ratings.

SQL aggregation techniques were applied to determine which restaurant holds the top spot based on customer ratings.


3. Rating Status Categorization:
   
A new column, Rating Status, was created to categorize restaurants based on their ratings:

Excellent: For ratings greater than 4 stars.

Good: For ratings above 3.5 stars but less than 4 stars.

Average: For ratings above 3 stars but less than 3.5 stars.

Bad: For ratings below 3 stars.


This categorization helps quickly gauge the overall quality of restaurants at a glance.

4. Mathematical Functions on Ratings:

The ceil, floor, and abs SQL functions were used to transform the restaurant ratings:

Ceil: Rounds up the rating.

Floor: Rounds down the rating.

Abs: Displays the absolute value of the rating (to handle negative cases, if any).

Additionally, the current date was displayed, and the year, month_name, and day were extracted and presented separately to show how time-based information can be isolated from a timestamp.

5. Cost Analysis Using Rollup:
 
The ROLLUP operator was employed to display the restaurant_type along with the total and average cost per restaurant type.
This analysis offers a deeper understanding of how different types of restaurants compare in terms of pricing.

Technologies Used:-

SQL: For data querying, UDF creation, and data manipulation.

SQLServer/MySQL: Database management system used for handling the restaurant data.

DBMS Tools: Any SQL IDE (e.g., pgAdmin, MySQL Workbench) for executing the queries and interacting with the database.

Sample Queries:-

Custom UDF for "Quick Chicken Bites":

sql
Copy code
CREATE FUNCTION add_chicken(input VARCHAR)
RETURNS VARCHAR
BEGIN
  IF input = 'Quick Bites' THEN
    RETURN 'Quick Chicken Bites';
  ELSE
    RETURN input;
  END IF;
END;


Restaurant with the Maximum Ratings:

sql
Copy code
SELECT restaurant_name, cuisine_type
FROM restaurants
WHERE rating = (SELECT MAX(rating) FROM restaurants);

Rating Status Column:

sql
Copy code
SELECT restaurant_name, 
       rating, 
       CASE
         WHEN rating > 4 THEN 'Excellent'
         WHEN rating > 3.5 AND rating <= 4 THEN 'Good'
         WHEN rating > 3 AND rating <= 3.5 THEN 'Average'
         ELSE 'Bad'
       END AS rating_status
FROM restaurants;

Mathematical Functions on Ratings:

sql
Copy code
SELECT rating, 
       CEIL(rating) AS ceil_value, 
       FLOOR(rating) AS floor_value, 
       ABS(rating) AS absolute_value,
       CURRENT_DATE AS current_date,
       EXTRACT(YEAR FROM CURRENT_DATE) AS year,
       EXTRACT(MONTH FROM CURRENT_DATE) AS month_name,
       EXTRACT(DAY FROM CURRENT_DATE) AS day
FROM restaurants;

Cost Analysis with Rollup:

sql
Copy code
SELECT restaurant_type, AVG(cost) AS avg_cost, SUM(cost) AS total_cost
FROM restaurants
GROUP BY ROLLUP(restaurant_type);

Conclusion:-

This project highlights how SQL functions and advanced queries can be used to perform sophisticated data manipulation and analysis, particularly in the context of restaurant ratings and costs. The use of user-defined functions and rollups demonstrates SQL’s flexibility for transforming and aggregating data to generate meaningful insights.


