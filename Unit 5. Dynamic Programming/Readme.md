# Unit 5: Dynamic Programming

## Introduction
Dynamic Programming is the most powerful design technique used to solve optimization problems. It is particularly effective when sub-problems are dependent, such as when they share the same sub-problems.

## Key Features

### 1. Optimal Substructure
- If an optimal solution contains optimal sub-solutions, then a problem shows optimal substructure.

### 2. Overlapping Sub-problems
- When a recursive algorithm would visit the same sub-problems repeatedly, then a problem has overlapping sub-problems.

## Dynamic Programming vs. Greedy Method

| Dynamic Programming | Greedy Method |
|-------------------|----------------|
| Used to obtain the optimal solution, which is guaranteed | Also used to obtain the optimal solution, but has no guarantee |
| Requires DP table for memorization and increases memory complexity | Does not require DP table for memorization as it never revises previous choices |
| Less efficient as compared to greedy approach | More efficient as compared to dynamic approach |
| In each step, choices may depend on the solutions to sub-problems | Makes whatever choice seems best at the moment and then solves the sub-problems arising after the choice is made |

## Divide and Conquer vs. Dynamic Programming

| Divide and Conquer Method | Dynamic Programming |
|--------------------------|-------------------|
| It is recursive | It is non-recursive |
| It does more work on sub-problems and hence has more time consumption | It solves sub-problems only once and then stores in the table |
| It is a top-down approach | It is a bottom-up approach |
| Sub-problems are independent of each other | Sub-problems are interdependent |

### Examples
- Divide and Conquer: Merge Sort & Binary Search
- Dynamic Programming: Matrix Multiplication

## Elements of Dynamic Programming Approach

There are three key elements that characterize a dynamic programming algorithm:

1. **Substructure**: Decompose the given problem into smaller sub-problems. Express the solution of the original problem in terms of the solution for smaller problems.

2. **Table Structure**: After solving sub-problems, store the results to the sub-problems in a table.

3. **Bottom-up Computation**: Using table, combine the solution of smaller sub-problems to solve larger sub-problems and eventually arrives at a solution to complete problem.

## Examples
- Dynamic Programming Example: Knapsack problem (0-1)
- Greedy Method Example: Fractional Knapsack

## Concept Implementation
Dynamic Programming is particularly useful when:
1. The problem can be broken down into smaller sub-problems
2. The solution to the problem depends on solutions to its sub-problems
3. The same sub-problems are encountered multiple times when solving the larger problem

## Minimum Edit Distance Problem

The Minimum Edit Distance (or Levenshtein Distance) is a classic dynamic programming problem that finds the minimum number of operations required to transform one string into another.

### Problem Statement
Given two strings str1 and str2, find the minimum number of operations required to convert str1 into str2. The allowed operations are:
1. Insert a character
2. Delete a character
3. Replace a character

### Example

Input:  str1 = "intention", str2 = "execution"
Output: 5
Explanation: 
intention → inention (remove 't')
inention → enention (replace 'i' with 'e')
enention → exention (replace 'n' with 'x')
exention → exection (replace 'n' with 'c')
exection → execution (insert 'u')

### Solution Approach
For strings "intention" and "execution", we create a DP table where:
- Rows represent characters of "intention" (m = 9)
- Columns represent characters of "execution" (n = 9)

The DP table will be filled using the following logic:
- If characters match: dp[i][j] = dp[i-1][j-1]
- If characters don't match: dp[i][j] = min(
    dp[i-1][j] + 1,      // deletion
    dp[i][j-1] + 1,      // insertion
    dp[i-1][j-1] + 2     // replacement (costs 2)
)

For example, when comparing 'n' with 'x':
1. Deletion: Remove 'n' (cost 1)
2. Insertion: Insert 'x' (cost 1)
3. Replacement: Replace 'n' with 'x' (cost 2)

This makes replacement more expensive than insertion or deletion, which is often more realistic since replacing involves both removing one character and adding another.

### Implementation Steps
1. Initialize first row and column
2. For each cell (i,j):
   - If characters match: Copy diagonal value
   - If characters don't match: Take minimum of:
     * Deletion (cost 1)
     * Insertion (cost 1)
     * Replacement (cost 2)
3. Final answer will be in dp[m][n]

The final value dp[9][9] = 5 represents the minimum number of operations needed.

### DP Table Visualization
Here's the dynamic programming table for converting "intention" to "execution":

|   |   | e | x | e | c | u | t | i | o | n |
|---|---|---|---|---|---|---|---|---|---|---|
|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
| n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
| t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
| e | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11|
| n | 5 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 10|
| t | 6 | 5 | 6 | 7 | 8 | 9 | 8 | 9 | 10| 11|
| i | 7 | 6 | 7 | 8 | 9 | 10| 9 | 8 | 9 | 10|
| o | 8 | 7 | 8 | 9 | 10| 11| 10| 9 | 8 | 9 |
| n | 9 | 8 | 9 | 10| 11| 12| 11| 10| 9 | 8 |

Note: The values are higher now because replacement costs 2 instead of 1.

Key observations in the updated table:
1. When characters match (like 'e' with 'e'), we take diagonal value
2. When characters don't match, we take min of:
   - Deletion (top cell + 1)
   - Insertion (left cell + 1)
   - Replacement (diagonal cell + 2)
3. The final value (8) represents the minimum operations needed with replacement cost of 2

### Row-by-Row Construction with Indices

#### Row 0 (Empty String to "execution"):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

Initial row (i=0) shows cost of inserting each character of "execution".

#### Row 1 (Processing 'i'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=1][j=1] ('i'-'e'):
- Replace: dp[i-1][j-1] + 2 = 0 + 2 = 2 ✓
- Delete: dp[i-1][j] + 1 = 1 + 1 = 2
- Insert: dp[i][j-1] + 1 = 1 + 1 = 2
Note: At column 7, matches with 'i' so takes diagonal value (7)

#### Row 2 (Processing 'n'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=2][j=2] ('n'-'x'):
- Replace: dp[i-1][j-1] + 2 = 2 + 2 = 4 ✓
- Delete: dp[i-1][j] + 1 = 3 + 1 = 4
- Insert: dp[i][j-1] + 1 = 3 + 1 = 4
Note: At last column, matches with 'n' so takes diagonal value (8)

#### Row 3 (Processing 't'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=3][j=6] ('t'-'t'):
- Characters match, take diagonal: dp[2][5] = 8
Note: Matches at column 6, so value stays 8

#### Row 4 (Processing 'e'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=4][j=1] and dp[i=4][j=3] ('e'-'e'):
- Characters match, take diagonal values
Note: Value drops to 3 at both 'e' positions

#### Row 5 (Processing 'n'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=5][j=4] ('n'-'c'):
- Replace 'n' with 'c': dp[i=4][j=3] + 2 = 3 + 2 = 5
- Delete 'n': dp[i=4][j=4] + 1 = 4 + 1 = 5
- Insert 'c': dp[i=5][j=3] + 1 = 4 + 1 = 5
Note: At last column, matches with 'n' so takes diagonal value (8)

#### Row 6 (Processing 't'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=6][j=6] ('t'-'t'):
- Characters match, take diagonal: dp[i=5][j=5] = 8
Note: Value stays 8 due to character match

#### Row 7 (Processing 'i'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=7][j=7] ('i'-'i'):
- Characters match, take diagonal: dp[i=6][j=6] = 8
Note: Value drops to 8 at column 7 due to matching 'i'

#### Row 8 (Processing 'o'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=8][j=8] ('o'-'o'):
- Characters match, take diagonal: dp[i=7][j=7] = 8
Note: Value stays 8 at column 8 due to matching 'o'

#### Final Row (Processing 'n'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|i=9 | 9 | 8 | 8 | 8 | 8 | 8 | 8 | 7 | 6 | 5 |
|    |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=9][j=9] ('n'-'n'):
- Characters match, take diagonal: dp[i=8][j=8] = 8
Final answer dp[i=9][j=9] = 8 represents minimum operations needed

This completes our table construction, showing how we arrive at the minimum edit distance of 8 operations to transform "intention" to "execution".

### Detailed Example of Replacement Operation

Let's look at a specific case where characters don't match and we need to calculate the replacement cost:

For position dp[i=2][j=2] (comparing 'n' with 'x'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=0 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |

When 'n' ≠ 'x', we calculate:
1. Replace operation: dp[i-1][j-1] + 2
   - Take diagonal value (dp[1][1] = 2)
   - Add 2 for replacement cost
   - Total = 2 + 2 = 4

2. Delete operation: dp[i-1][j] + 1
   - Take value from above (dp[1][2] = 3)
   - Add 1 for deletion cost
   - Total = 3 + 1 = 4

3. Insert operation: dp[i][j-1] + 1
   - Take value from left (dp[2][1] = 3)
   - Add 1 for insertion cost
   - Total = 3 + 1 = 4

Choose minimum: min(4, 4, 4) = 4
All operations have the same cost in this case.

Another example for dp[i=5][j=4] (comparing 'n' with 'c'):
|i\j |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|
|i=4 | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | 5 | 4 | 4 | 4 | 5 | 5 | 6 | 7 | 8 | 8 |

When 'n' ≠ 'c':
1. Replace: dp[i-1][j-1] + 2 = dp[4][3] + 2 = 3 + 2 = 5
2. Delete: dp[i-1][j] + 1 = dp[4][4] + 1 = 4 + 1 = 5
3. Insert: dp[i][j-1] + 1 = dp[5][3] + 1 = 4 + 1 = 5

Choose minimum: min(5, 5, 5) = 5
All operations result in the same cost.

This modified cost structure (replacement = 2) makes replacement operations more "expensive" than insertions or deletions, which might be more realistic in some applications where replacing a character is considered more complex than simply inserting or deleting one.

