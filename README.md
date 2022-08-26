# Pewlett-Hackard-Analysis

# Overview
After creating a database for Pewlett-Hackard employee information an analysis was performed to gain insight of the upcoming wave of retirements that will be happening at the company. The number of employees retiring, their respective departments, and potential eligibility for a mentorship program were derived from the database and summarized for management. 

### Software
- pgAdmin 4 version 6.8

## Results
Results: Provide a bulleted list with four major points from the two analysis deliverables. Use images as support where needed.
- The first query returned a table with the number of employees that will be eligible for retirement by their current job title. A total of 72,458 employees belonging to seven distinct job title groups. 
-The title with the highest number of potential retirees was Senior Engineer with 25,916 and the lowest being Manager with only 2.<br><br>
![Screen Shot 2022-08-25 at 7 14 22 PM](https://user-images.githubusercontent.com/106560606/186798386-f703ef09-dbfb-4308-8248-d1b3a6d3979e.png) <br>

- The second query returned a table with employees that are eligible for the mentorship program. These employees have a birth date between January 1, 1965 and December 31, 1965.
- A total of only 1549 employees across varying job titles were found to be eligible for the program given these search parameters. <br><br>
![Screen Shot 2022-08-25 at 7 15 26 PM](https://user-images.githubusercontent.com/106560606/186798557-e4722a66-2f5d-4974-98ca-2f6f223d6740.png)
<br>

## Summary
This analysis shows that there will be 72,458 employees from 7 distinct job title groups eligible for retirement from Pewlett-Hackard. Given the current parameters for mentorship eligibility, only 1549 of the retirement eligible employees would be able to participate in the mentorship program. This creates a massive need for more mentor eligible employees (70,909). 

### Suggestions
Changing the age parameters to determine mentorship eligibility could be useful in finding more employees to participate. The current parameter is only for a birth date in the year 1965. If that were changed to 1964 to 1966, the need for mentors could be much closer to being met. However, given retirement age requirements and changing legislation, a definite timeframe or birthdates cannot be suggested at this point. Using the following SQL code snippet the dates can be easily adjusted in the query and reused with the new parameters for birth dates on the Pewlett-Hackard employee database. Simply replace this code
````sql
'1965-01-01' AND '1965-12-31'
````
in the following code block with new birthdates.
````sql
-- Create mentorship eligibility table
SELECT DISTINCT ON (e.emp_no) e.emp_no,
	e.first_name,
	e.last_name,
	e.birth_date,
	de.from_date,
	de.to_date,
	ti.title
INTO mentorship_eligibility
FROM employees AS e
INNER JOIN dept_emp AS de
ON (e.emp_no = de.emp_no)
INNER JOIN titles AS ti
ON (e.emp_no = ti.emp_no)
WHERE (de.to_date = '9999-01-01')
	AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no;
```` 
<br>
A table grouping the mentorship eligible employees by job title will assist in knowing which areas are possibly staffed with enough eligible mentors. With the current parameters for birthdate in place this table shows six distinct job titles with eligible mentors. Some of the job titles needed do not have any eligible mentors. <br><br>


![Screen Shot 2022-08-25 at 8 36 50 PM](https://user-images.githubusercontent.com/106560606/186798477-0d70e63c-cfd6-4820-8266-bf7792f4a6d5.png)
