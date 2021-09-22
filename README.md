# Pewlett-Hackard-Analysis

## Overview of the Analysis

### Purpose of Analysis
Many employees are retiring soon at Pewlett-Hackard, so there will be thousands of job openings coming in the next few years. We are building an employee database in SQL to analyze and prepare for the upcoming silver tsunami. 
The major questions we are looking into are:

   - Who is retiring soon?
    
   - How many positions need to be filled?
    
   - Offer retirement packages for people meeting cetain criteria.
    

### Overview of the Challenge
Along with answering the above questions, we are asked to collect more information to,
    - Determine number of retiring employees per title
    - Identify employees who are eligible to participate in a mentorship program

## Resources
Software: PG Admin4 Version 5.6, Postgress Database, VS Code 1.60 (to write SQL queries and access .csv data files).

## Results

Number of Retiring Employees by Title:

To determine the number of employees by title, we are joining employees table and titles table, and filter for employees with birthday between 1952 and 1955. 

1. We notice that the employee names are repeating with different titles. As the employee receives promotion, their title changes and we are capturing all the titles. To get the accurate number of retiring employees by title, we need to consider the latest title for an employee and ignore the past titles.
    - To correct it, we are using DISTINCT ON on the employee number and picking up the latest title based on to_date in titles table.
    
            -- Use Dictinct with Orderby to get unique titles
            SELECT DISTINCT ON (emp_no) emp_no ,
                    first_name,
                    last_name,
                    title
            INTO unique_titles
            FROM retirement_titles
            ORDER BY emp_no, to_date DESC;

2. Another interesting fact we are observing when we group number of employees by title is that  more than 60% of people retiring is part of the senior management team (that is Senior Engineer and Senior Staff). 

    ![](https://github.com/Nikhila999/Pewlett-Hackard-Analysis/blob/main/Images/Retiring_Employess_by_Title.png)

Employees Eligible for Mentorship Program:

To determine the employees who qualify for mentorship program, we are joining employees table, titles table and department employee table and filtering the records for current employees born in 1965.

3. There are 1549 employees eligible for mentorship program from 9 departments.

4. As the number of employees retiring soon are more than 90k and most of them are from management team, it is very important for Pewlett-Hackard to retain some of the employees to train the next generation employees for the organization to run efficiently and effortlessly. The silver tsunami along with mentorship analysis gives more details for the executives to make decisions on how many employess to train and in which departments.


## Summary

1. How many roles will need to be filled as the "silver tsunami" begins to make an impact?
    - There are 90,398 employees begin to retire in next few years.

            SELECT COUNT(first_name)
            FROM employees
            WHERE birth_date BETWEEN '1952-01-01' AND '1955-12-31';

2. Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
    - There are 1549 employees eligible for mentorship program and they are from all the 9 departments, which suggests that qualified mentors would be able to train the employees in all the departments. So, from image below, we see that there are eligible mentors from all departments.
    
    ![](https://github.com/Nikhila999/Pewlett-Hackard-Analysis/blob/main/Images/mentors_by_departments.png)

3. Of all the people retiring soon (upcoming silver tsunami), 3 departments (Development, Sales and Production) are contributing more than 65% to it.

    ![](https://github.com/Nikhila999/Pewlett-Hackard-Analysis/blob/main/Images/retiree_by_department.png)

4. Out of 90,398 employees retiring in next few years, there are 36,258 women and 54,140 men.

    ![](https://github.com/Nikhila999/Pewlett-Hackard-Analysis/blob/main/Images/retirees_by_gender.png)
