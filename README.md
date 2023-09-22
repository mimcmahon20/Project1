# Project1
 
# Nurse Scheduling Linear Program

## Key Variables

- `day_dict`: Dictionary mapping days of the week to indices.
- `num_nurses`: Total number of nurses.
- `num_patients`: Total number of patients.
- `num_tasks`: Total number of tasks.
- `num_days`: Number of days in a week (7 days).
- `task_list`: List of tasks.
- `medication_adherence_dict` and `physical_therapy_adherence_dict`: Dictionaries containing adherence data for medication and physical therapy, respectively.

## Decision Variables

- \( x[i, j, k] \): Binary variable. 1 if nurse `i` is assigned to patient `j` on day `k`, 0 otherwise.
- \( w[i, k] \): Binary variable. 1 if nurse `i` is working on day `k`, 0 otherwise.
- \( p[i, m, k] \): Binary variable. 1 if nurse `i` is at location `m` on day `k`, 0 otherwise.
- \( t[i, j, n, k] \): Binary variable. 1 if nurse `i` is performing task `n` for patient `j` on day `k`, 0 otherwise.

## Objective Function

The objective function aims to maximize the total benefit of assigning tasks to nurses. It considers a fixed benefit for each task assignment and also adjusts based on the adherence value for medication and physical therapy tasks.

## Constraints

1. **Weekly Work Hours**: Each nurse can work up to 40 hours in a week.
2. **Mandatory Task Coverage**: Ensure all mandatory tasks for each patient are covered.
3. **Working Day Linking**: Link the assignment of tasks/patients to the working day binary variable.
4. **Max Working Days**: Limit the number of days a nurse can work in a week.
5. **Location Constraint**: Each nurse works in only one location in a given day.
6. **Task Completion**: Ensure each necessary task for each patient is completed each day.
7. **Single Nurse per Task**: Only one nurse is assigned to a specific task for a specific patient on a specific day.
8. **Consecutive Location**: A nurse must work in the same location for consecutive days if they are working on both days.

## Output

The script provides the optimal objective value and a detailed schedule for each nurse, specifying the tasks they are performing for each patient on each day.

## Limitations and Considerations

- This model assumes that the provided data frames (`nurses_df`, `patients_df`, `task_execution_time_df`, `locations_df`) are available in the runtime environment.
- The adherence data for medication and physical therapy are converted to dictionaries for easier access and are used in the objective function to adjust the benefit of task assignments.
- The model currently considers a 7-day week. Adjustments would be needed for different time frames.
