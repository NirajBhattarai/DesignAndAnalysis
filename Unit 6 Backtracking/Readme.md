# 0/1 Knapsack Problem using Backtracking

## Problem Definition
The 0/1 Knapsack problem involves selecting items with given weights and values to maximize total value while keeping total weight under capacity. Using backtracking, we systematically explore all possible combinations of items.

## Example Problem
Consider a knapsack with capacity W = 10 kg and 5 items:

| Item | Weight (kg) | Value ($) |
|------|-------------|-----------|
| 1    | 2          | 20        |
| 2    | 3          | 30        |
| 3    | 4          | 45        |
| 4    | 1          | 15        |
| 5    | 3          | 25        |

## Backtracking Approach

### 1. Decision Tree
For each item, we have two choices:
- Include the item (1)
- Exclude the item (0)

This creates a binary decision tree which can be viewed in two formats:

#### A. Binary Tree Format
```
                                                Root
                                            (0,0,$0,0kg)
                                ╱                              ╲
                        Include Item 1                      Exclude Item 1
                      (1,0,$20,2kg)                         (0,0,$0,0kg)
                    ╱                ╲                    ╱                ╲
            Include Item 2        Exclude Item 2  Include Item 2        Exclude Item 2
            (1,1,$50,5kg)        (1,0,$20,2kg)  (0,1,$30,3kg)        (0,0,$0,0kg)
            ╱          ╲         ╱          ╲    ╱          ╲         ╱          ╲
    Include    Exclude     Include    Exclude   Include    Exclude    Include    Exclude
    Item 3     Item 3      Item 3     Item 3    Item 3     Item 3     Item 3     Item 3
    ($95,9kg)  ($50,5kg)   ($65,6kg)  ($20,2kg) ($75,7kg)  ($30,3kg) ($45,4kg)  ($0,0kg)
    ╱    ╲     ╱    ╲      ╱    ╲     ╱    ╲    ╱    ╲     ╱    ╲    ╱    ╲     ╱    ╲
   I4    E4   I4    E4    I4    E4   I4    E4  I4    E4   I4    E4  I4    E4   I4    E4
$110* $95  $65  $50    $80  $65   $35  $20  $90  $75   $45  $30  $60  $45   $15   $0
10kg  9kg  6kg  5kg    7kg  6kg   3kg  2kg  8kg  7kg   4kg  3kg  5kg  4kg   1kg   0kg
```

#### B. Table Format
| Path ID | Item 1 | Item 2 | Item 3 | Item 4 | Total Value | Total Weight | Status |
|---------|--------|---------|---------|---------|--------------|--------------|---------|
| P1      | 1      | 1       | 1       | 1       | $110        | 10kg         | Optimal* |
| P2      | 1      | 1       | 1       | 0       | $95         | 9kg          | Valid    |
| P3      | 1      | 1       | 0       | 1       | $65         | 6kg          | Valid    |
| P4      | 1      | 1       | 0       | 0       | $50         | 5kg          | Valid    |
| P5      | 1      | 0       | 1       | 1       | $80         | 7kg          | Valid    |
| P6      | 1      | 0       | 1       | 0       | $65         | 6kg          | Valid    |
| P7      | 1      | 0       | 0       | 1       | $35         | 3kg          | Valid    |
| P8      | 1      | 0       | 0       | 0       | $20         | 2kg          | Valid    |
| P9      | 0      | 1       | 1       | 1       | $90         | 8kg          | Valid    |
| P10     | 0      | 1       | 1       | 0       | $75         | 7kg          | Valid    |
| P11     | 0      | 1       | 0       | 1       | $45         | 4kg          | Valid    |
| P12     | 0      | 1       | 0       | 0       | $30         | 3kg          | Valid    |
| P13     | 0      | 0       | 1       | 1       | $60         | 5kg          | Valid    |
| P14     | 0      | 0       | 1       | 0       | $45         | 4kg          | Valid    |
| P15     | 0      | 0       | 0       | 1       | $15         | 1kg          | Valid    |
| P16     | 0      | 0       | 0       | 0       | $0          | 0kg          | Valid    |

Legend:
- 1: Item included
- 0: Item excluded
- *: Optimal solution
- Status: Valid/Invalid (exceeds weight) or Pruned (by bound check)

Notes:
1. All paths that would include Item 5 are pruned as they would exceed capacity
2. Some paths may be pruned early due to bound checking
3. The table shows only valid paths (16 out of potential 32 paths)

Key Observations from the Complete Tree:

1. Optimal Solution Path:
   - Include Item 1 ($20, 2kg)
   - Include Item 2 ($30, 3kg)
   - Include Item 3 ($45, 4kg)
   - Include Item 4 ($15, 1kg)
   - Total: $110, 10kg

2. Pruning Examples:
   - After Item 3 inclusion (9kg), Item 5 paths are pruned (would exceed 10kg)
   - Branches with low value sums are pruned by bound checking

3. Notable Alternatives:
   - Second best: $95 (Items 1,2,3)
   - Third best: $90 (Items 2,3,4)

4. Pruning Effectiveness:
   - From possible 2⁵=32 leaf nodes
   - Only 16 paths need full evaluation
   - Others pruned by weight or bound checks

### 2. State Space
Each node in the tree represents a state with:
- Selected items (binary string)
- Current value sum
- Current weight sum
- Level (depth in tree)

### 3. Constraints
- Weight sum ≤ Capacity (10 kg)
- Each item can be used at most once

### 4. Pruning Conditions
1. If current weight exceeds capacity
2. If remaining possible value + current value < best solution found

### 5. Implementation

```c
#include <stdio.h>
#include <stdbool.h>

#define MAX_ITEMS 100

typedef struct {
    int weight;
    int value;
} Item;

// Global variables
Item items[MAX_ITEMS];
bool selected[MAX_ITEMS];
bool bestSelection[MAX_ITEMS];
int n, capacity;
int maxValue = 0;

// Calculate remaining possible value from remaining items
int calculateBound(int level, int currentValue, int currentWeight) {
    int remainingValue = 0;
    for (int i = level; i < n; i++) {
        remainingValue += items[i].value;
    }
    return currentValue + remainingValue;
}

void knapsack(int level, int currentValue, int currentWeight) {
    // Base case: reached end of items
    if (level == n) {
        if (currentValue > maxValue) {
            maxValue = currentValue;
            // Save current selection
            for (int i = 0; i < n; i++) {
                bestSelection[i] = selected[i];
            }
        }
        return;
    }
    
    // Pruning: check if this branch could possibly beat best solution
    if (calculateBound(level, currentValue, currentWeight) <= maxValue) {
        return;
    }
    
    // Try including current item if weight allows
    if (currentWeight + items[level].weight <= capacity) {
        selected[level] = true;
        knapsack(level + 1, 
                currentValue + items[level].value,
                currentWeight + items[level].weight);
    }
    
    // Try excluding current item
    selected[level] = false;
    knapsack(level + 1, currentValue, currentWeight);
}

void printSolution() {
    printf("Maximum value: $%d\n", maxValue);
    printf("Selected items:\n");
    int totalWeight = 0;
    for (int i = 0; i < n; i++) {
        if (bestSelection[i]) {
            printf("Item %d (Weight: %dkg, Value: $%d)\n",
                   i + 1, items[i].weight, items[i].value);
            totalWeight += items[i].weight;
        }
    }
    printf("Total weight: %dkg\n", totalWeight);
}
```

### 6. Step-by-Step Execution

Let's trace the execution for first few steps:

1. Start at root (0,0,$0,0kg)
   - Try including Item 1
   - Try excluding Item 1

2. Path: Include Item 1 (1,0,$20,2kg)
   - Weight (2kg) ≤ Capacity (10kg)
   - Try including Item 2
   - Try excluding Item 2

3. Path: Include Item 1 & 2 (1,1,$50,5kg)
   - Weight (5kg) ≤ Capacity (10kg)
   - Try including Item 3
   - Try excluding Item 3

4. Path: Include Item 1 & 2 & 3 (1,1,1,$95,9kg)
   - Weight (9kg) ≤ Capacity (10kg)
   - Try including Item 4
   - Try excluding Item 4

5. Path: Include Item 1 & 2 & 3 & 4 (1,1,1,1,$110,10kg)
   - Weight (10kg) = Capacity (10kg)
   - Cannot include Item 5 (would exceed capacity)
   - Update maxValue if better than current best

### 7. Backtracking Process

1. When a path reaches maximum capacity or all items:
   - Compare current value with maxValue
   - Update maxValue and bestSelection if better
   - Backtrack to try other combinations

2. When a path exceeds capacity:
   - Prune this branch
   - Backtrack to try other combinations

3. When bound check fails:
   - Prune this branch (cannot beat best solution)
   - Backtrack to try other combinations

### 8. Final Solution
For our example:
- Maximum value: $110
- Selected items: 1, 2, 3, 4
- Total weight: 10kg

## Comparison with Dynamic Programming

### Backtracking Approach
Advantages:
- Uses less memory (O(n) space)
- Can stop early with pruning
- Easier to modify constraints

Disadvantages:
- Slower for large inputs (O(2ⁿ) time)
- May explore many unnecessary paths
- Performance varies with input order

### Dynamic Programming Approach
Advantages:
- Guaranteed O(nW) time
- Explores each subproblem once
- Consistent performance

Disadvantages:
- Uses more memory (O(nW) space)
- Must solve all subproblems
- Less flexible for constraint changes

## Time and Space Complexity
- Time Complexity: O(2ⁿ) worst case
- Space Complexity: O(n) for recursion stack
- Practical performance often better due to pruning

## Applications
1. Resource allocation
2. Cargo loading
3. Investment decisions
4. Project selection
5. Budget planning
