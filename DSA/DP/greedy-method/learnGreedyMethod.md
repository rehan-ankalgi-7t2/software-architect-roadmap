# Greedy Method

### **What is the Greedy Method?**
The greedy method solves optimization problems by:
1. Making the best local (immediate) choice at each step.
2. Hoping that these local choices lead to a globally optimal solution.

---

### **Key Characteristics of Greedy Problems**
1. **Greedy Choice Property**:  
   - A globally optimal solution can be arrived at by choosing a local optimum at each step.
2. **Optimal Substructure**:  
   - A problem has optimal substructure if the optimal solution to the problem can be constructed from optimal solutions to its subproblems.

---

### **Steps to Solve a Problem Using Greedy**
1. **Understand the Problem**:
   - Identify if the problem exhibits greedy properties (Greedy Choice + Optimal Substructure).
2. **Define the Objective**:
   - Decide what you're optimizing (e.g., minimize cost, maximize profit).
3. **Make Greedy Choices**:
   - Choose the best immediate option at each step.
4. **Iterate Until Complete**:
   - Keep making greedy choices until the solution is complete.
5. **Validate the Solution**:
   - Ensure that the greedy approach provides the correct result.

---

### **Common Problems Solved Using Greedy**
1. **Activity/Interval Selection**:
   - Select the maximum number of non-overlapping intervals.
2. **Huffman Encoding**:
   - Build an optimal prefix code for data compression.
3. **Minimum Spanning Tree (MST)**:
   - Algorithms like Prim’s and Kruskal’s.
4. **Knapsack Problem (Fractional)**:
   - Choose items to maximize profit while staying within weight limits.
5. **Dijkstra’s Algorithm**:
   - Find the shortest path in a graph.
6. **Job Scheduling**:
   - Maximize profit or minimize time by scheduling jobs optimally.

---

### **Greedy vs Dynamic Programming**
| Feature                   | **Greedy**                                  | **Dynamic Programming**                   |
|---------------------------|---------------------------------------------|-------------------------------------------|
| **Approach**              | Makes local optimal choices.               | Solves subproblems and combines results.  |
| **When to Use**           | When greedy choice leads to global optima. | When subproblems overlap or depend on each other. |
| **Complexity**            | Often \(O(n \log n)\)                      | Often \(O(n^2)\) or higher.               |
| **Examples**              | Activity Selection, MST                    | 0/1 Knapsack, Longest Common Subsequence. |

---

### **Common Techniques in Greedy Problems**
1. **Sorting**:
   - Sort items based on a key (e.g., start time, weight, profit-to-weight ratio).
2. **Priority Queues (Heaps)**:
   - Use heaps to repeatedly extract the smallest/largest element efficiently.
3. **Iterative Selection**:
   - Sequentially make choices, updating the state.

---

### **Common Pitfalls**
1. **Not Always Optimal**:
   - Greedy methods don’t always guarantee an optimal solution. Validate with proof.
2. **Failure to Meet Constraints**:
   - Ensure that greedy choices meet all problem constraints.
3. **Overlooking Dynamic Programming**:
   - Some problems require considering multiple states (e.g., 0/1 Knapsack).

---

### **Cheat Sheet for Problem Solving**
| **Problem Type**                 | **Greedy Strategy**                                                                                     |
|----------------------------------|--------------------------------------------------------------------------------------------------------|
| **Scheduling**                   | Sort by start time, end time, or profit.                                                               |
| **Shortest Path (Positive Weights)** | Use Dijkstra’s Algorithm (choose the node with the smallest tentative distance).                        |
| **Minimum Spanning Tree**        | Use Kruskal’s or Prim’s algorithm (add smallest edge that doesn’t form a cycle).                       |
| **Fractional Knapsack**          | Take items with the highest value-to-weight ratio until capacity is full.                             |
| **Huffman Encoding**             | Merge the two smallest frequencies iteratively.                                                        |
| **Coin Change (Greedy Feasible)**| Pick the largest coin denomination less than or equal to the amount to make change.                   |
| **Maximum Intervals**            | Sort by end time, pick intervals that don’t overlap.                                                   |

---

### **Template for Writing Greedy Code**
```typescript
function greedySolution(data: DataType[]): ResultType {
    // Step 1: Sort data if necessary
    data.sort((a, b) => someKey(a) - someKey(b));

    // Step 2: Initialize variables to track progress
    let result = initializeResult();
    
    // Step 3: Iterate and make greedy choices
    for (let item of data) {
        if (isValid(item, result)) {
            updateResult(item, result);
        }
    }
    
    // Step 4: Return the result
    return result;
}
```

---

This cheat sheet provides a quick summary of how to approach greedy problems and how to decide if they fit a given scenario.
