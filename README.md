# Project: Interactive Transportation Problem Solver

### 🔗 Live Demo & Usage
> **View Live Demo:** 
*(https://nuruzzamanrahat.github.io/Transportation-Prroblem-Solver/)*

## Project Overview

This project is an **interactive web application** that solves the **classic Transportation Problem** from *Operations Research*.  

Given:
- A set of **suppliers (sources)** with limited supply capacities.
- A set of **customers (destinations)** with specific demand requirements.
- The **cost matrix** representing the cost to ship one unit from each source to each destination.

The tool finds the **optimal shipping plan** that **minimizes total transportation cost**.

### Optimization Algorithms Used

This project directly implements two key algorithms :

#### **Phase 1:** Vogel’s Approximation Method (VAM)
A heuristic algorithm that finds a **high-quality Initial Basic Feasible Solution (IBFS)**.

#### **Phase 2:** Modified Distribution (MODI / UV Method)
An iterative optimization algorithm that tests and **improves the IBFS** to ensure **global optimality**.

---

## 🧮 The Mathematical Model

We aim to **minimize the total cost** \( Z \):

\[
Z = \sum_{i=1}^{m} \sum_{j=1}^{n} c_{ij} x_{ij}
\]

Where:
- \( m \) = number of sources  
- \( n \) = number of destinations  
- \( c_{ij} \) = cost of shipping one unit from source *i* to destination *j*  
- \( x_{ij} \) = quantity shipped from source *i* to destination *j*  

### Subject to Constraints:

1. **Supply Constraints**  
   Total shipped *from* each source ≤ its supply  
   \[
   \sum_{j=1}^{n} x_{ij} \le s_i \quad \forall i = 1, 2, …, m
   \]

2. **Demand Constraints**  
   Total shipped *to* each destination ≥ its demand  
   \[
   \sum_{i=1}^{m} x_{ij} \ge d_j \quad \forall j = 1, 2, …, n
   \]

3. **Non-negativity**  
   \[
   x_{ij} \ge 0
   \]

---

##  Methodology

###  **Phase 1: Vogel’s Approximation Method (VAM)**

To begin optimization, we need a feasible initial solution.  
VAM is a **smart heuristic** that provides an excellent starting solution — often close to the optimal one.

**Steps of VAM:**
1. **Calculate Penalties:**  
   For each row and column, find the difference between the two smallest costs.  
   This represents the penalty for not using the cheapest route.
2. **Select Maximum Penalty:**  
   Choose the row or column with the highest penalty.
3. **Allocate:**  
   In that selected row/column, find the cell with the lowest cost.
4. **Assign Maximum Units:**  
   Allocate as many units as possible, limited by available supply and demand.
5. **Update:**  
   Adjust supply/demand and remove satisfied rows or columns.
6. **Repeat** until all supply and demand are met.

---

###  **Phase 2: Modified Distribution Method (MODI / UV Method)**

VAM provides a feasible starting solution. MODI ensures **optimality** by improving it iteratively.

**Steps of MODI:**

1. **Check for Degeneracy:**  
   A non-degenerate solution must have exactly \( m + n - 1 \) allocated cells.

2. **Calculate \( u_i \) and \( v_j \):**  
   For all allocated cells, solve:  
   \[
   c_{ij} = u_i + v_j
   \]  
   Start with \( u_1 = 0 \) and compute all other \( u \) and \( v \) values.

3. **Compute Opportunity Costs \( d_{ij} \):**  
   For unallocated cells:  
   \[
   d_{ij} = c_{ij} - u_i - v_j
   \]

4. **Check for Optimality:**  
   - If all \( d_{ij} \ge 0 \): current solution is **optimal**.  
   - If any \( d_{ij} < 0 \): the solution can be **improved**.

5. **Improve the Solution:**  
   - Select the cell with the **most negative \( d_{ij} \)**.  
   - Form a **closed loop** (stepping-stone path) of allocated cells.  
   - Identify “+” and “–” corners along the loop.  
   - Adjust allocations: add to “+” cells, subtract from “–” cells using the smallest “–” value.

6. **Repeat Steps 2–5** until optimality is reached.

---

## How to Use the App

1. **Define Sources:**  
   Click “Add Source” to create supply points and specify their capacities.

2. **Define Destinations:**  
   Click “Add Destination” to create demand points and specify their requirements.

3. **Check Balance:**  
   - The app automatically detects if total supply ≠ total demand.  
   - If unbalanced, it automatically adds a **dummy source/destination** with **0 cost**, ensuring a balanced problem.

4. **Define Cost Matrix:**  
   Enter the cost per unit from each source to each destination.

5. **Solve:**  
   Click **“Find Optimal Solution”** to compute:
   - The **Initial (VAM) Solution**
   - The **Optimal (MODI) Solution**

6. **Review Results:**  
   -  **Optimal Solution Found!**  
     Shows the minimum transportation cost and shipment plan.  
   -  **Initial Solution (VAM):**  
     Shows the first feasible plan and cost before optimization.

---

## 📸 Example Output

> *Add a screenshot of your running web app here.*

![App Screenshot Placeholder](assets/screenshot-placeholder.png)

---

## 📂 Project Structure

