# Pewlett-Hackard-Analysis

## Purpose
The purpose of this analysis was to review employee data from Pewlett-Hackard in order to determine the following:
 1. The titles held by employees who are at retirement age.
 2. The current titles of employees at retirement age.
 3. How many employees per title are at retirement age.
 4. The number of employees who are eligible for a mentorship program.

## Results
Throughout this analysis, we created a databases to hold all of our information, pulled data from different tables, and created new tables using joins. We began by determining the total number of employees retiring and the number of employees retiring by department. We quickly realized that in order to utilize this information, we needed to drill down further into the data.

We started the process by determining all of the titles held by employees who are at retirement age. That information is held in the retirement_titles table in PostgreSQL, and has been exported into a .csv file here:

[retirement_titles](retirement_titles.csv)

Looking at the list of titles below, we can see that there are duplicate employee numbers. 

![Image](..%5C..%5C..%5C..%5C..%5CDupes.png)

These duplicate titles are due to the fact that employees have been promoted throughout their time at Pewlett-Hackard. Since we want to determine the roles that will need to be filled as these employees retire, it is necessary to remove duplicate employee numbers and get the current titles of all employees who are at retirement age. We did this with the following SQL query:

    SELECT DISTINCT ON (rt.emp_no) rt.emp_no,
            rt.first_name,
            rt.last_name,
            rt.title
    INTO unique_titles
    FROM retirement_titles AS rt
    WHERE rt.to_date = '9999-01-01'
    ORDER BY rt.emp_no, rt.to_date DESC;

The unique titles for each employee at retirement age can be seen in this .csv file:
[unique_titles](unique_titles.csv)

Next, we needed to determine how many employees with each title are retiring soon. This information can be viewed in this .csv file:
[retiring_titles](retiring_titles.csv)

Finally, we determined who is eligible for the proposed mentorship program by joining three different tables in order to produce a new table that includes all current employees who were born between January 1, 1965 and December 31, 1965. That information can be viewed in this .csv file:
[mentorship_eligibility](mentorhsip_eligibility.csv)

## Summary
Ultimately, our analysis boils down to the following:
    Q: How many roles will need to be filled as the "silver tsunami" begins to make an impact?
        A: There is a very high number of employees born between 1952 and 1955 who will be retiring soon, assuming a retirement age of 65 years old. The number is 72,458. 
    Q: Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
        A: At this time, there are 1,549 employees eligible for the mentorship program (born in 1965). This means that there are enough retiring employees to step into a mentorship role and mentor these employees who are not quite at retirement age themselves.