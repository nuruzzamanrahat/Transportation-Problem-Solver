Project: Interactive Transportation Problem Solver

Live Demo & Usage

► View Live Demo

Project Overview

This project is an interactive web application that solves the classic Transportation Problem from Operations Research. Given a set of suppliers (sources) with limited capacities, a set of customers (destinations) with specific demands, and the cost to ship one unit from each source to each destination, this tool finds the shipping plan that minimizes the total transportation cost.

This implementation is a direct application of two key optimization algorithms from your syllabus:

Phase 1: Vogel's Approximation Method (VAM) - A sophisticated heuristic used to find a high-quality Initial Basic Feasible Solution (IBFS).

Phase 2: Modified Distribution (MODI) / UV Method - An iterative optimization algorithm (based on the principles of the Simplex dual) that checks the IBFS for optimality and improves it until the minimum cost solution is guaranteed.

The Mathematical Model

The goal is to minimize the total cost Z:

$$Z = \sum_{i=1}^{m} \sum_{j=1}^{n} c_{ij} x_{ij}
$$Where:

* `m` = number of sources
* `n` = number of destinations
* `c_ij` = cost of shipping one unit from source `i` to destination `j`
* `x_ij` = number of units to ship from source `i` to destination `j`

Subject to the constraints:

1.  **Supply Constraints:** The total shipped *from* a source cannot exceed its supply.$$

$$\\sum\_{j=1}^{n} x\_{ij} \\le s\_i \\quad \\text{for } i = 1, 2, ..., m

$$
$$(Where `s_i` is the supply at source `i`)


Demand Constraints: The total shipped to a destination must meet its demand.

$$\\ \sum\_{i=1}^{m} x\_{ij} \ge d\_j \quad \text{for } j = 1, 2, ..., n$$

$$$$(Where d_j is the demand at destination j)

Non-negativity: You cannot ship a negative number of items.

$$\\ x\_{ij} \ge 0$$

$$$$

Methodology

Phase 1: Vogel's Approximation Method (VAM)

To find an optimal solution, we must first have a feasible solution. While we could use simple methods like the Northwest Corner Rule, VAM is a much smarter heuristic that often gives a solution very close to the optimal one, saving optimization time.

VAM works as follows:

Calculate Penalties: For each row and column, find the difference between the two lowest costs. This "penalty" represents the cost of not using the cheapest route.

Select Max Penalty: Find the row or column with the highest penalty.

Allocate: In that selected row or column, find the cell with the lowest cost.

Assign Max Flow: Allocate as many units as possible to this cell, limited by the available supply and demand.

Update: Satisfy the supply or demand, and remove the corresponding row or column.

Repeat: Go back to Step 1 and repeat until all supplies and demands are met.

Phase 2: MODI (UV) Method for Optimality

VAM gives a good start, but it doesn't guarantee optimality. The MODI (Modified Distribution) method checks and improves the solution.

Check for Degeneracy: A non-degenerate solution must have exactly m + n - 1 allocated cells (where m = rows, n = columns). This app's implementation has basic handling for this.

Calculate u and v values: Set up a system of equations for all allocated cells based on the formula: c_ij = u_i + v_j. We set u_1 = 0 and solve for all other u and v values.

Calculate Opportunity Costs (d_ij): For all unallocated cells, calculate the opportunity cost: d_ij = c_ij - u_i - v_j.

Check for Optimality:

If all d_ij are greater than or equal to 0, the current solution is optimal.

If any d_ij is negative, the solution can be improved.

Improve the Solution (Iterate):

Select the unallocated cell with the most negative d_ij. This is the new cell to enter the solution.

Form a closed loop (or "stepping-stone path") starting from this cell, alternating between currently allocated cells.

Find the minimum allocation in the "minus" corners of the loop.

Add this minimum value to the "plus" corners and subtract it from the "minus" corners, creating a new, better allocation.

Repeat: Go back to Step 2 and repeat the MODI process until optimality (Step 4) is reached.

How to Use the App

Define Sources: Use the "Add Source" button to create your supply points. Enter their names and supply capacity.

Define Destinations: Use the "Add Destination" button to create your demand points. Enter their names and demand requirements.

Check Balance: The app will show a message if your total supply and demand are not equal. If they are unbalanced, it will automatically add a dummy source or destination with 0 cost to solve the problem, which is the standard procedure.

Define Cost Matrix: Fill in the table with the cost to ship one unit from each source to each destination.

Solve: Click the "Find Optimal Solution" button.

Review Results:

Optimal Solution Found!: This box shows the final, minimum total cost and the optimal shipping plan from the MODI method.

Initial Solution (VAM): This box shows the first solution found by VAM and its (higher) cost, allowing you to see the improvement made by the MODI method.

[Add a screenshot of your running application here!]
