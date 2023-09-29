# Nurse Scheduling Optimization

## Introduction

This project aims to optimize the scheduling of nurses to improve patient adherence to medical tasks while considering various constraints. The scheduling problem is formulated as a mixed-integer linear programming (MILP) problem and is solved using the Gurobi Optimizer.

## Dependencies

- Python
- Gurobi Optimizer
- NumPy

## Problem Formulation

The optimization problem is formulated with the following components:

### Decision Variables
- \( x[i, j, k] \): Binary variable indicating whether nurse \(i\) is assigned to patient \(j\) on day \(k\).
- \( w[i, k] \): Binary variable indicating whether nurse \(i\) is working on day \(k\).
- \( p[i, m, k] \): Binary variable indicating whether nurse \(i\) is at location \(m\) on day \(k\).
- \( t[i, j, n, k] \): Binary variable indicating whether nurse \(i\) is performing task \(n\) for patient \(j\) on day \(k\).
- \( D[i, m, k] \): Binary variable indicating whether nurse \(i\) is at location \(m\) on day \(k\).

### Objective Function
The objective is to maximize the adherence score, calculated as a weighted sum of adherence levels for each task assigned to each patient.

### Constraints
- Each nurse can work up to 10 hours a day.
- Each nurse can work a maximum of 4 days a week.
- Nurses can only be assigned tasks that match their skills.
- Each nurse can only work at one location per day.
- Nurses can only be assigned to a task for a patient if they are at the patient's location.
- Each patient's necessary tasks must be completed.
- Each task for a patient can only be assigned to one nurse per day.
- Nurses can only change their working location a limited number of times per week.

## Usage

1. Prepare the data in the required format. You would need the following dataframes:
   - `nurses_df`: Contains information about each nurse, including their skillset.
   - `patients_df`: Contains information about each patient, including their location and needed tasks.
   - `task_execution_time_df`: Contains information about each task, including execution time.
   - `locations_df`: Contains information about each location.
   - `medication_adherence_df` and `physical_therapy_adherence_df`: Contains adherence information for medication and physical therapy tasks.

2. Run the optimization model by creating an instance of the `Model` class from Gurobi and defining the decision variables, objective function, and constraints as shown in the provided code.

3. Call `model.optimize()` to solve the optimization problem.

4. If the problem is solved optimally, the schedule for each nurse will be printed, showing the tasks assigned to them for each day of the week.

## Conclusion

This nurse scheduling optimization tool helps in efficiently assigning tasks to nurses while considering various constraints, aiming to improve patient adherence to medical tasks.

