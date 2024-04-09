# L4G Program - Employee Salary Analysis

# Overview:
# This L4G program analyzes employee salary data stored in a file and performs the following tasks:
# 1. Calculates the average salary of employees.
# 2. Identifies high earners whose salary exceeds the average.
# 3. Recommends promotions for employees whose salary is below 80% of the average.

# Files:
# - employee_salary_analysis.l4g: The main L4G program file that performs the analysis.

# Usage:
# 1. Ensure that the L4G interpreter is installed on your system.
# 2. Place the employee_salary_analysis.l4g file in the desired directory.
# 3. Ensure that the employee data file (EMPLOYEE) is available in the appropriate location.
# 4. Run the program using the L4G interpreter.

# Instructions:
# 1. Open a terminal or command prompt.
# 2. Navigate to the directory containing the employee_salary_analysis.l4g file.
# 3. Run the program by executing the following command:
# ```
# l4g employee_salary_analysis.l4g
# ```
# 4. Follow the on-screen instructions to view the analysis results.

# Sample Output:
# ```
# Average Salary: 50000
# High Earners:
# John Doe: 60000
# Jane Smith: 55000
# Promotion recommended for Michael Johnson
# ```

# Notes:
# - This program assumes that the employee data is stored in a file named EMPLOYEE. Please ensure that the file exists and is properly formatted.
# - Adjustments may be required to the file paths and data formats based on your specific environment and requirements.
# - Feel free to modify the program to suit your needs or extend its functionality as necessary.

# Define variables
DEFINE VARIABLE TotalSalary INTEGER INIT 0.
DEFINE VARIABLE NumEmployees INTEGER INIT 0.
DEFINE VARIABLE AVERAGE_SALARY DECIMAL INIT 0.

# Open file and read data
READ([F:EMPLOYEE]Employee_Record)

# Calculate total salary and count number of employees
WHILE FOUND([F:EMPLOYEE])
    TotalSalary := TotalSalary + Employee_Record.Salary
    NumEmployees := NumEmployees + 1
    READ([F:EMPLOYEE]Employee_Record)
ENDWHILE

# Calculate average salary
IF NumEmployees > 0 THEN
    AVERAGE_SALARY := TotalSalary / NumEmployees
ELSE
    AVERAGE_SALARY := 0

# Display average salary
DISPLAY "Average Salary: " + AVERAGE_SALARY

# Reset file pointer
READ([F:EMPLOYEE]Employee_Record)

# Display high earners
DISPLAY "High Earners:"
WHILE FOUND([F:EMPLOYEE])
    IF Employee_Record.Salary > AVERAGE_SALARY THEN
        DISPLAY Employee_Record.Name + ": " + Employee_Record.Salary
    ENDIF
    READ([F:EMPLOYEE]Employee_Record)
ENDWHILE

# Check for promotions
READ([F:EMPLOYEE]Employee_Record)
WHILE FOUND([F:EMPLOYEE])
    IF Employee_Record.Salary < (AVERAGE_SALARY * 0.8) THEN
        DISPLAY "Promotion recommended for " + Employee_Record.Name
    ENDIF
    READ([F:EMPLOYEE]Employee_Record)
ENDWHILE
