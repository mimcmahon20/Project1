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

### Linear Programming Formulation

**Parameters**:
- \( n \): Number of nurses.
- \( p \): Number of patients.
- \( t \): Number of tasks.
- \( d \): Number of days in the planning horizon.
- \( D_{ij} \): Distance between locations of patient \( i \) and patient \( j \).
- \( T_k \): Time required for task \( k \).
- \( \text{MedAdhere}_{jd} \): Medication adherence rate for patient \( j \) on day \( d \).
- \( \text{PhysTherAdhere}_{jd} \): Physical therapy adherence rate for patient \( j \) on day \( d \).
- \( S_i \): Skill set of nurse \( i \).
- \( N_j \): Needs (tasks) of patient \( j \).

**Decision Variables**:
- \( x_{ijkd} \): 1 if nurse \( i \) performs task \( k \) for patient \( j \) on day \( d \), 0 otherwise.

**Objective Function**:
\[
\text{Maximize } \sum_{i=1}^{n} \sum_{j=1}^{p} \sum_{k=1}^{t} \sum_{d=1}^{d} (x_{ijkd} \times \text{MedAdhere}_{jd} + x_{ijkd} \times \text{PhysTherAdhere}_{jd})
\]

**Constraints**:
1. **Nurse's Working Time**:
\[
\sum_{j=1}^{p} \sum_{k=1}^{t} T_k \times x_{ijkd} + \sum_{j=1}^{p} \sum_{l=1, l\neq j}^{p} D_{jl} \times x_{ijkd} \times x_{ij'kd} \leq 8 \quad \forall i, d
\]
2. **Task Assignment**:
\[
\sum_{i=1}^{n} \sum_{d=1}^{d} x_{ijkd} = 1 \quad \forall j, k
\]
3. **Skills Matching**:
\[
x_{ijkd} \leq 1 \text{ if } k \in S_i \text{ and } k \in N_j \quad \forall i, j, k, d
\]
4. **Patient Adherence**:
\[
x_{ijkd} \leq \text{MedAdhere}_{jd} \text{ and } x_{ijkd} \leq \text{PhysTherAdhere}_{jd} \quad \forall i, j, k, d
\]
