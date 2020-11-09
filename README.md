# Pewlett-Hackard-Analysis

Through using the data we were trying to solve the total number of employees per title who were retiring and the employees who are eligible to participate in a mentorship program. The reason for this analysis is to help provide solutions for the big number of upcoming retiring employees while trying to find employees elegible for a mentorship program to hopefully move them up in the company. 

To get the number of retiring employees, we merged two tables to recieve the employee information in order to see how many employees were retiring: 

" -- Create new table for deliverable_one

SELECT ri.emp_no, ri.first_name, ri.last_name, ti.title, s.salary, s.from_date

INTO deliverable_one

FROM retirement_info AS ri

INNER JOIN salaries AS s

ON (ri.emp_no = s.emp_no)

INNER JOIN titles AS ti

ON (ri.emp_no = ti.emp_no)

SELECT * FROM deliverable_one "

We then had to partition the data to clean it and eliminate doubles. 

    ("-- Partition the data to show only most recent title per employee

    SELECT first_name,
    last_name,
    title,
    salary,
    emp_no

    INTO deliverable_one_part

    FROM

    (SELECT first_name,
          last_name,
          title,
       salary,
       emp_no, 
       ROW_NUMBER() OVER
       (PARTITION BY (emp_no)
       ORDER BY from_date DESC) rn
       FROM deliverable_one as del) 
    tmp WHERE rn = 1
    ORDER BY emp_no; ") 

From there we set our sights on the mentorship data. We basically did the same process but added the birth dates of the eligble employees. We also had to partition this data due to having doubles in the first data table. 

In conclusion, although the number of retiring employees is a bit high, especially in the senior positions, the mentorship program should set the employees on the right path to slowly transition into the new positions. The limitations we ran into was lack of assertive information of the employee actually deciding whether or not he wanted to retire. We didn't know if the employee had decided to retire early or later, we were assuming based off of their age. My recommendation would be do a poll on the employees that are "coming of age" to see if they're planning to retire. 
