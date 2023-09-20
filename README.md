# Project1
 
# Nurse Scheduling Linear Program

## Variables:

1. **x[i, j, k]**: A binary variable that determines whether nurse i is assigned to patient j on day k.
2. **w[i, k]**: A binary variable that indicates whether nurse i is working on day k.
3. **l[i, m, k]**: A binary variable that indicates whether nurse i is at location m on day k.
4. **t[i, j, n, k]**: A binary variable that indicates whether nurse i is performing task n for patient j on day k.

## Objective Function:

The objective function is designed to maximize the total adherence to medication and physical therapy schedules across all patients and days. It computes this by summing up the adherence percentages for each patient on each day (if that day is present in the respective adherence dataframes) and assigning tasks to nurses in a way that maximizes this total adherence.

## Constraints:

1. **Maximum Working Days per Week**: Each nurse can work a maximum of 4 days in a week.
2. **Task Assignment**: Each task for a patient on a specific day is assigned to exactly one nurse.
3. **Maximum Working Hours per Day**: Each nurse can work a maximum of 10 hours per day.
4. **Task Completion**: Each mandatory task for a patient must be completed each day (excluding tasks with adherence).
5. **Skillset Matching**: Nurses are assigned tasks that match their skillsets.

## Data Loading and Processing:

The data (locations, nurses, patients, task execution times, medication adherence, physical therapy adherence, and distance matrix) are loaded dynamically from an Excel file and processed to extract necessary information and format them appropriately for use in the linear program.

