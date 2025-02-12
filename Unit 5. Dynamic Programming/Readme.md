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

|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | o | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|i=9 | n | 9 | 8 | 8 | 8 | 8 | 8 | 8 | 7 | 6 | 5 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

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
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

Initial row (i=0) shows cost of inserting each character of "execution".

#### Row 1 (Processing 'i'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=1][j=1] ('i'-'e'):
- Replace: dp[i-1][j-1] + 2 = 0 + 2 = 2 ✓
- Delete: dp[i-1][j] + 1 = 1 + 1 = 2
- Insert: dp[i][j-1] + 1 = 1 + 1 = 2
Note: At column 7, matches with 'i' so takes diagonal value (7)

#### Row 2 (Processing 'n'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=2][j=2] ('n'-'x'):
- Replace: dp[i-1][j-1] + 2 = 2 + 2 = 4 ✓
- Delete: dp[i-1][j] + 1 = 3 + 1 = 4
- Insert: dp[i][j-1] + 1 = 3 + 1 = 4
Note: At last column, matches with 'n' so takes diagonal value (8)

#### Row 3 (Processing 't'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=3][j=6] ('t'-'t'):
- Characters match, take diagonal: dp[2][5] = 8
Note: Matches at column 6, so value stays 8

#### Row 4 (Processing 'e'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=4][j=1] and dp[i=4][j=3] ('e'-'e'):
- Characters match, take diagonal values
Note: Value drops to 3 at both 'e' positions

#### Row 5 (Processing 'n'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=5][j=4] ('n'-'c'):
- Replace 'n' with 'c': dp[i=4][j=3] + 2 = 3 + 2 = 5
- Delete 'n': dp[i=4][j=4] + 1 = 4 + 1 = 5
- Insert 'c': dp[i=5][j=3] + 1 = 4 + 1 = 5
Note: At last column, matches with 'n' so takes diagonal value (8)

#### Row 6 (Processing 't'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=6][j=6] ('t'-'t'):
- Characters match, take diagonal: dp[i=5][j=5] = 8
Note: Value stays 8 due to character match

#### Row 7 (Processing 'i'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=7][j=7] ('i'-'i'):
- Characters match, take diagonal: dp[i=6][j=6] = 8
Note: Value drops to 8 at column 7 due to matching 'i'

#### Row 8 (Processing 'o'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | o | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=8][j=8] ('o'-'o'):
- Characters match, take diagonal: dp[i=7][j=7] = 8
Note: Value stays 8 at column 8 due to matching 'o'

#### Final Row (Processing 'n'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
|i=3 | t | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 10| 11|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | o | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|i=9 | n | 9 | 8 | 8 | 8 | 8 | 8 | 8 | 7 | 6 | 5 |
|    |   |j=0|j=1|j=2|j=3|j=4|j=5|j=6|j=7|j=8|j=9|

For dp[i=9][j=9] ('n'-'n'):
- Characters match, take diagonal: dp[i=8][j=8] = 8
Final answer dp[i=9][j=9] = 8 represents minimum operations needed

This completes our table construction, showing how we arrive at the minimum edit distance of 8 operations to transform "intention" to "execution".

### Detailed Example of Replacement Operation

Let's look at a specific case where characters don't match and we need to calculate the replacement cost:

For position dp[i=2][j=2] (comparing 'n' with 'x'):
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
|i=2 | n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |

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
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=4 | e | 4 | 3 | 4 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=5 | n | 5 | 4 | 4 | 4 | 5 | 5 | 6 | 7 | 8 | 8 |

When 'n' ≠ 'c':
1. Replace: dp[i-1][j-1] + 2 = dp[4][3] + 2 = 3 + 2 = 5
2. Delete: dp[i-1][j] + 1 = dp[4][4] + 1 = 4 + 1 = 5
3. Insert: dp[i][j-1] + 1 = dp[5][3] + 1 = 4 + 1 = 5

Choose minimum: min(5, 5, 5) = 5
All operations result in the same cost.

This modified cost structure (replacement = 2) makes replacement operations more "expensive" than insertions or deletions, which might be more realistic in some applications where replacing a character is considered more complex than simply inserting or deleting one.

### Backtracing with Arrows

Starting from dp[9][9], we follow the minimum cost path (arrows indicate the direction we came from):
↖ = diagonal match (keep character)
← = insertion
↑ = deletion
↖* = diagonal replace

|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=0 |   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|i=1 | i | 1 |↖*2|← 3|← 4|← 5|← 6|← 7|↖ 7|← 8|← 9|
|i=2 | n | 2 |↑ 3|↖*4|← 5|← 6|← 7|← 8|↑ 8|← 9|↖ 8|
|i=3 | t | 3 |↑ 4|↖*5|← 6|← 7|← 8|↖ 8|← 9|←10|↑11|
|i=4 | e | 4 |↖ 3|← 4|↖ 3|← 4|← 5|← 6|← 7|← 8|← 9|
|i=5 | n | 5 |↑ 4|← 4|← 4|↖*4|← 5|← 6|← 7|← 8|↖ 8|
|i=6 | t | 6 |↑ 5|← 5|← 5|← 5|← 5|↖ 5|← 6|← 7|← 8|
|i=7 | i | 7 |↑ 6|← 6|← 6|← 6|← 6|← 6|↖ 5|← 6|← 7|
|i=8 | o | 8 |↑ 7|← 7|← 7|← 7|← 7|← 7|↑ 6|↖ 5|← 6|
|i=9 | n | 9 |↑ 8|← 8|← 8|← 8|← 8|← 8|↑ 7|↑ 6|↖ 5|

Following the arrows from dp[9][9] back to dp[0][0]:
1. dp[9][9] = 5: ↖ match 'n' (keep)
2. dp[8][8] = 5: ↖ match 'o' (keep)
3. dp[7][7] = 5: ↖ match 'i' (keep)
4. dp[6][6] = 5: ↖ match 't' (keep)
5. dp[5][5] = 5: ← insert 'u'
6. dp[5][4] = 4: ↖* replace 'n' with 'c'
7. dp[4][3] = 3: ↖ match 'e' (keep)
8. dp[3][2] = 5: ↖* replace 't' with 'x'
9. dp[2][1] = 3: ↖* replace 'n' with 'e'
10. dp[1][0] = 1: ↑ delete 'i'

This gives us the same sequence of operations:
intention → ntention (delete 'i')
ntention → etention (replace 'n' with 'e')
etention → exention (replace 't' with 'x')
exention → exection (replace 'n' with 'c')
exection → execution (insert 'u')

### Step-by-Step Backtrace

Starting from dp[9][9], we trace back through each step:

#### Step 1: dp[9][9] ('n'-'n') - Match ↖
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=8 | o | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 | 5 | 6 |
|i=9 | n | 9 | 8 | 8 | 8 | 8 | 8 | 8 | 7 | 6 |[5]|
Operation: Keep 'n' (match)
Current: execution → execution

#### Step 2: dp[8][8] ('o'-'o') - Match ↖
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 | 5 | 6 | 7 |
|i=8 | o | 8 | 7 | 7 | 7 | 7 | 7 | 7 | 6 |[5]| 6 |
Operation: Keep 'o' (match)
Current: executio → executio

#### Step 3: dp[7][7] ('i'-'i') - Match ↖
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 6 | 7 | 8 |
|i=7 | i | 7 | 6 | 6 | 6 | 6 | 6 | 6 |[5]| 6 | 7 |
Operation: Keep 'i' (match)
Current: executi → executi

#### Step 4: dp[6][6] ('t'-'t') - Match ↖
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=5 | n | 5 | 4 | 4 | 4 | 4 | 5 | 6 | 7 | 8 | 8 |
|i=6 | t | 6 | 5 | 5 | 5 | 5 | 5 |[5]| 6 | 7 | 8 |
Operation: Keep 't' (match)
Current: execut → execut

#### Step 5: dp[5][5] ('n'-'u') - Insert ←
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=5 | n | 5 | 4 | 4 | 4 |[4]| 5 | 6 | 7 | 8 | 8 |
Operation: Insert 'u'
Current: execu → execu

#### Step 6: dp[5][4] ('n'-'c') - Replace ↖*
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=5 | n | 5 | 4 | 4 | 4 |[4]| 5 | 6 | 7 | 8 | 8 |
Operation: Replace 'n' with 'c'
Current: exec → exec

#### Step 7: dp[4][3] ('e'-'e') - Match ↖
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=4 | e | 4 | 3 | 4 |[3]| 4 | 5 | 6 | 7 | 8 | 9 |
Operation: Keep 'e' (match)
Current: exe → exe

#### Step 8: dp[3][2] ('t'-'x') - Replace ↖*
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=3 | t | 3 | 4 |[5]| 6 | 7 | 8 | 8 | 9 | 10| 11|
Operation: Replace 't' with 'x'
Current: ex → ex

#### Step 9: dp[2][1] ('n'-'e') - Replace ↖*
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=2 | n | 2 |[3]| 4 | 5 | 6 | 7 | 8 | 8 | 9 | 8 |
Operation: Replace 'n' with 'e'
Current: e → e

#### Step 10: dp[1][0] ('i') - Delete ↑
|i\j |   |   | e | x | e | c | u | t | i | o | n |
|----|---|---|---|---|---|---|---|---|---|---|---|
|i=1 | i |[1]| 2 | 3 | 4 | 5 | 6 | 7 | 7 | 8 | 9 |
Operation: Delete 'i'
Current: "" → ""

Complete transformation path:
intention → ntention (delete 'i')
ntention → etention (replace 'n' with 'e')
etention → exention (replace 't' with 'x')
exention → exection (replace 'n' with 'c')
exection → execution (insert 'u')

# Matrix Chain Multiplication

## Problem Definition
Matrix Chain Multiplication is an optimization problem that determines the most efficient way to multiply a sequence of matrices. The goal is to minimize the total number of scalar multiplications.

## Formula and Rules
1. Base Case: M[i,i] = 0 (single matrix requires no multiplication)
2. Recursive Formula: M[i,j] = min { M[i,k] + M[k+1,j] + (rows(i) × cols(k) × cols(j)) }
   where k varies from i to j-1

### Important Rules:
1. For matrices to be multiplicable, cols(first) must equal rows(second)
2. Result matrix dimensions: rows(first) × cols(second)
3. Cost of multiplying (p×q) and (q×r) matrices = p×q×r scalar multiplications

## Example with 7 Matrices
Consider matrices A₁, A₂, A₃, A₄, A₅, A₆, A₇ with dimensions:
- A₁: 35 × 15
- A₂: 15 × 25
- A₃: 25 × 30
- A₄: 30 × 40
- A₅: 40 × 20
- A₆: 20 × 35
- A₇: 35 × 45

## Step-by-Step Solution

### Step 1: Initialize (Length = 1)
Initialize diagonal with zeros (no cost for single matrix)

| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | -      | -      | -      | -      | -      | -      |
| 2   | -     | 0      | -      | -      | -      | -      | -      |
| 3   | -     | -      | 0      | -      | -      | -      | -      |
| 4   | -     | -      | -      | 0      | -      | -      | -      |
| 5   | -     | -      | -      | -      | 0      | -      | -      |
| 6   | -     | -      | -      | -      | -      | 0      | -      |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Step 2: Length = 2 (Adjacent Pairs)
Apply formula for k = i:
M[i,j] = M[i,i] + M[i+1,j] + (rows(i) × cols(i) × cols(j))

1. C[1,2] = A₁ × A₂
   - M[1,1] + M[2,2] + (35 × 15 × 25)
   - 0 + 0 + 13,125 = 13,125

2. C[2,3] = A₂ × A₃
   - M[2,2] + M[3,3] + (15 × 25 × 30)
   - 0 + 0 + 11,250 = 11,250

3. C[3,4] = A₃ × A₄
   - M[3,3] + M[4,4] + (25 × 30 × 40)
   - 0 + 0 + 30,000 = 30,000

4. C[4,5] = A₄ × A₅
   - M[4,4] + M[5,5] + (30 × 40 × 20)
   - 0 + 0 + 24,000 = 24,000

5. C[5,6] = A₅ × A₆
   - M[5,5] + M[6,6] + (40 × 20 × 35)
   - 0 + 0 + 28,000 = 28,000

6. C[6,7] = A₆ × A₇
   - M[6,6] + M[7,7] + (20 × 35 × 45)
   - 0 + 0 + 31,500 = 31,500

Resulting table after length 2:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | -      | -      | -      | -      | -      |
| 2   | -     | 0      | 11,250 | -      | -      | -      | -      |
| 3   | -     | -      | 0      | 30,000 | -      | -      | -      |
| 4   | -     | -      | -      | 0      | 24,000 | -      | -      |
| 5   | -     | -      | -      | -      | 0      | 28,000 | -      |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Step 3: Length = 3 (Three Matrices)
Apply formula with k varying from i to j-1

1. C[1,3] calculation:
   For k = 1: (Split: (A₁)(A₂A₃))
   - M[1,1] + M[2,3] + (35 × 15 × 30)
   - 0 + 11,250 + 15,750 = 27,000

   For k = 2: (Split: (A₁A₂)(A₃))
   - M[1,2] + M[3,3] + (35 × 25 × 30)
   - 13,125 + 0 + 26,250 = 22,375 ← Minimum

2. C[2,4] calculation:
   For k = 2: (Split: (A₂)(A₃A₄))
   - M[2,2] + M[3,4] + (15 × 25 × 40)
   - 0 + 30,000 + 15,000 = 45,000

   For k = 3: (Split: (A₂A₃)(A₄))
   - M[2,3] + M[4,4] + (15 × 30 × 40)
   - 11,250 + 0 + 18,000 = 29,250 ← Minimum

3. C[3,5] calculation:
   For k = 3: (Split: (A₃)(A₄A₅))
   - M[3,3] + M[4,5] + (25 × 30 × 20)
   - 0 + 24,000 + 15,000 = 39,000

   For k = 4: (Split: (A₃A₄)(A₅))
   - M[3,4] + M[5,5] + (25 × 40 × 20)
   - 30,000 + 0 + 20,000 = 50,000

4. C[4,6] calculation:
   For k = 4: (Split: (A₄)(A₅A₆))
   - M[4,4] + M[5,6] + (30 × 40 × 35)
   - 0 + 28,000 + 42,000 = 70,000

   For k = 5: (Split: (A₄A₅)(A₆))
   - M[4,5] + M[6,6] + (30 × 20 × 35)
   - 24,000 + 0 + 21,000 = 45,000 ← Minimum

5. C[5,7] calculation:
   For k = 5: (Split: (A₅)(A₆A₇))
   - M[5,5] + M[6,7] + (40 × 20 × 45)
   - 0 + 31,500 + 36,000 = 67,500

   For k = 6: (Split: (A₅A₆)(A₇))
   - M[5,6] + M[7,7] + (40 × 35 × 45)
   - 28,000 + 0 + 63,000 = 91,000

Resulting table after length 3:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | 22,375 | -      | -      | -      | -      |
| 2   | -     | 0      | 11,250 | 29,250 | -      | -      | -      |
| 3   | -     | -      | 0      | 30,000 | 39,000 | -      | -      |
| 4   | -     | -      | -      | 0      | 24,000 | 45,000 | -      |
| 5   | -     | -      | -      | -      | 0      | 28,000 | 67,500 |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Step 4: Length = 4 (Four Matrices)
Apply formula with k varying from i to j-1

1. C[1,4] calculation:
   For k = 1: (Split: (A₁)(A₂A₃A₄))
   - M[1,1] + M[2,4] + (35 × 15 × 40)
   - 0 + 29,250 + 21,000 = 50,250

   For k = 2: (Split: (A₁A₂)(A₃A₄))
   - M[1,2] + M[3,4] + (35 × 25 × 40)
   - 13,125 + 30,000 + 35,000 = 78,125

   For k = 3: (Split: (A₁A₂A₃)(A₄))
   - M[1,3] + M[4,4] + (35 × 30 × 40)
   - 22,375 + 0 + 42,000 = 64,375 ← Minimum

2. C[2,5] calculation:
   For k = 2: (Split: (A₂)(A₃A₄A₅))
   - M[2,2] + M[3,5] + (15 × 25 × 20)
   - 0 + 39,000 + 7,500 = 46,500 ← Minimum

   For k = 3: (Split: (A₂A₃)(A₄A₅))
   - M[2,3] + M[4,5] + (15 × 30 × 20)
   - 11,250 + 24,000 + 9,000 = 44,250

   For k = 4: (Split: (A₂A₃A₄)(A₅))
   - M[2,4] + M[5,5] + (15 × 40 × 20)
   - 29,250 + 0 + 12,000 = 41,250

3. C[3,6] calculation:
   For k = 3: (Split: (A₃)(A₄A₅A₆))
   - M[3,3] + M[4,6] + (25 × 30 × 35)
   - 0 + 70,000 + 26,250 = 96,250

   For k = 4: (Split: (A₃A₄)(A₅A₆))
   - M[3,4] + M[5,6] + (25 × 40 × 35)
   - 30,000 + 28,000 + 35,000 = 93,000

   For k = 5: (Split: (A₃A₄A₅)(A₆))
   - M[3,5] + M[6,6] + (25 × 20 × 35)
   - 39,000 + 0 + 17,500 = 56,500 ← Minimum

4. C[4,7] calculation:
   For k = 4: (Split: (A₄)(A₅A₆A₇))
   - M[4,4] + M[5,7] + (30 × 40 × 45)
   - 0 + 67,500 + 54,000 = 121,500

   For k = 5: (Split: (A₄A₅)(A₆A₇))
   - M[4,5] + M[6,7] + (30 × 20 × 45)
   - 24,000 + 31,500 + 27,000 = 82,500 ← Minimum

   For k = 6: (Split: (A₄A₅A₆)(A₇))
   - M[4,6] + M[7,7] + (30 × 35 × 45)
   - 70,000 + 0 + 47,250 = 117,250

Resulting table after length 4:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | 22,375 | 50,250 | -      | -      | -      |
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | -      | -      |
| 3   | -     | -      | 0      | 30,000 | 39,000 | 56,500 | -      |
| 4   | -     | -      | -      | 0      | 24,000 | 45,000 | 82,500 |
| 5   | -     | -      | -      | -      | 0      | 28,000 | 67,500 |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Step 5: Length = 5 (Five Matrices)

1. C[1,5] calculation:
   For k = 1: (Split: (A₁)(A₂A₃A₄A₅))
   - M[1,1] + M[2,5] + (35 × 15 × 20)
   - 0 + 46,500 + 10,500 = 57,000 ← Minimum

   For k = 2: (Split: (A₁A₂)(A₃A₄A₅))
   - M[1,2] + M[3,5] + (35 × 25 × 20)
   - 13,125 + 39,000 + 17,500 = 69,625

   For k = 3: (Split: (A₁A₂A₃)(A₄A₅))
   - M[1,3] + M[4,5] + (35 × 30 × 20)
   - 22,375 + 24,000 + 21,000 = 67,375

   For k = 4: (Split: (A₁A₂A₃A₄)(A₅))
   - M[1,4] + M[5,5] + (35 × 40 × 20)
   - 64,375 + 0 + 28,000 = 92,375


2. C[2,6] calculation:
   For k = 2: (Split: (A₂)(A₃A₄A₅A₆))
   - M[2,2] + M[3,6] + (15 × 25 × 35)
   - 0 + 96,250 + 13,125 = 109,375

   For k = 3: (Split: (A₂A₃)(A₄A₅A₆))
   - M[2,3] + M[4,6] + (15 × 30 × 35)
   - 11,250 + 70,000 + 15,750 = 97,000

   For k = 4: (Split: (A₂A₃A₄)(A₅A₆))
   - M[2,4] + M[5,6] + (15 × 40 × 35)
   - 29,250 + 28,000 + 21,000 = 78,250

   For k = 5: (Split: (A₂A₃A₄)(A₅A₆))
   - M[2,5] + M[6,6] + (15 × 20 × 35)
   - 46,500 + 0 + 10,500 = 57,000 ← Minimum

3. C[3,7] calculation:
   For k = 3: (Split: (A₃)(A₄A₅A₆A₇))
   - M[3,3] + M[4,7] + (25 × 30 × 45)
   - 0 + 121,500 + 33,750 = 155,250

   For k = 4: (Split: (A₃A₄)(A₅A₆A₇))
   - M[3,4] + M[5,7] + (25 × 40 × 45)
   - 30,000 + 67,500 + 45,000 = 142,500

   For k = 5: (Split: (A₃A₄A₅)(A₆A₇))
   - M[3,5] + M[6,7] + (25 × 20 × 45)
   - 39,000 + 31,500 + 22,500 = 93,000 ← Minimum

   For k = 6: (Split: (A₃A₄A₅A₆)(A₇))
   - M[3,6] + M[7,7] + (25 × 35 × 45)
   - 96,250 + 0 + 55,125 = 151,375

Resulting table after length 5:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | 22,375 | 50,250 | 57,000 | -      | -      |
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | 57,000 | -      |
| 3   | -     | -      | 0      | 30,000 | 39,000 | 56,500 | 93,000 |
| 4   | -     | -      | -      | 0      | 24,000 | 45,000 | 82,500 |
| 5   | -     | -      | -      | -      | 0      | 28,000 | 67,500 |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Step 6: Length = 6 (Six Matrices)

1. C[1,6] calculation:
   For k = 1: (Split: (A₁)(A₂A₃A₄A₅A₆))
   - M[1,1] + M[2,6] + (35 × 15 × 35)
   - 0 + 80,625 + 18,375 = 99,000

   For k = 2: (Split: (A₁A₂)(A₃A₄A₅A₆))
   - M[1,2] + M[3,6] + (35 × 25 × 35)
   - 13,125 + 96,250 + 28,125 = 137,500

   For k = 3: (Split: (A₁A₂A₃)(A₄A₅A₆))
   - M[1,3] + M[4,6] + (35 × 30 × 35)
   - 22,375 + 70,000 + 38,250 = 130,625

   For k = 4: (Split: (A₁A₂A₃A₄)(A₅A₆))
   - M[1,4] + M[5,6] + (35 × 40 × 35)
   - 64,375 + 28,000 + 49,000 = 141,375

   For k = 5: (Split: (A₁A₂A₃A₄A₅)(A₆))
   - M[1,5] + M[6,6] + (35 × 20 × 35)
   - 57,000 + 0 + 24,500 = 81,500

   For k = 6: (Split: (A₁A₂A₃A₄A₅A₆)(A₇))
   - M[1,6] + M[7,7] + (35 × 35 × 45)
   - 99,000 + 0 + 55,125 = 154,125

Resulting table after length 6:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | 22,375 | 50,250 | 57,000 | 81,500 | 104,250|
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | 57,000 | 80,625 |
| 3   | -     | -      | 0      | 30,000 | 39,000 | 56,500 | 93,000 |
| 4   | -     | -      | -      | 0      | 24,000 | 45,000 | 82,500 |
| 5   | -     | -      | -      | -      | 0      | 28,000 | 67,500 |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

### Final Complete Table:
| i\j | 1     | 2      | 3      | 4      | 5      | 6      | 7      |
|-----|-------|--------|--------|--------|--------|--------|--------|
| 1   | 0     | 13,125 | 22,375 | 50,250 | 57,000 | 81,500 | 104,250|
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | 57,000 | 80,625 |
| 3   | -     | -      | 0      | 30,000 | 39,000 | 56,500 | 93,000 |
| 4   | -     | -      | -      | 0      | 24,000 | 45,000 | 82,500 |
| 5   | -     | -      | -      | -      | 0      | 28,000 | 67,500 |
| 6   | -     | -      | -      | -      | -      | 0      | 31,500 |
| 7   | -     | -      | -      | -      | -      | -      | 0      |

## Time and Space Complexity
- Space Complexity: O(n²) for storing the DP table
- Time Complexity: O(n³) where n is the number of matrices
  - O(n²) subproblems
  - O(n) choices for each subproblem

## Applications
1. Expression parsing
2. Chain of database operations
3. Optimization of tensor operations in deep learning
4. Parallel processing of matrix chains

### K Table (Split Points)
| i\j | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|-----|---|---|---|---|---|---|---|
| 1   | - | 1 | 2 | 1 | 1 | 5 | 1 |
| 2   | - | - | 2 | 3 | 4 | 5 | 6 |
| 3   | - | - | - | 3 | 3 | 5 | 5 |
| 4   | - | - | - | - | 4 | 5 | 5 |
| 5   | - | - | - | - | - | 5 | 6 |
| 6   | - | - | - | - | - | - | 6 |
| 7   | - | - | - | - | - | - | - |

### Finding Optimal Parenthesization
Starting from M[1,7], we look at K[1,7] = 1:
1. First split at k=1: (A₁)(A₂A₃A₄A₅A₆A₇)

For right part A₂A₃A₄A₅A₆A₇, look at K[2,7] = 6:
2. Split at k=6: (A₁)((A₂A₃A₄A₅A₆)(A₇))

For A₂A₃A₄A₅A₆, look at K[2,6] = 5:
3. Split at k=5: (A₁)((A₂A₃A₄A₅)(A₆)(A₇))

For A₂A₃A₄A₅, look at K[2,5] = 4:
4. Split at k=4: (A₁)(((A₂A₃A₄)(A₅))(A₆)(A₇))

For A₂A₃A₄, look at K[2,4] = 3:
5. Split at k=3: (A₁)(((A₂A₃)(A₄))(A₅))(A₆)(A₇))

Final optimal parenthesization:
(A₁)(((A₂A₃)(A₄))(A₅))(A₆)(A₇))

### Verification of Multiplication Sequence:
1. Multiply A₂×A₃ = (15×25)×(25×30) = 11,250
2. Multiply (A₂A₃)×A₄ = (15×30)×(30×40) = 18,000
3. Multiply (A₂A₃A₄)×A₅ = (15×40)×(40×20) = 12,000
4. Multiply ((A₂A₃A₄)A₅)×A₆ = (15×20)×(20×35) = 10,500
5. Multiply (((A₂A₃A₄)A₅)A₆)×A₇ = (15×35)×(35×45) = 23,625
6. Finally A₁×(((A₂A₃A₄)A₅)A₆A₇) = (35×15)×(15×45) = 23,625

Total cost = 104,250 (matches our DP table value at M[1,7])

# Traveling Salesman Problem (TSP)

## Problem Definition
The Traveling Salesman Problem (TSP) is a classic optimization problem that asks: "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city?"

## Formula and Rules
1. Base Case: dp[i][{i}] = 0 (cost to visit single city is 0)
2. Recursive Formula: dp[i][S] = min { dist[i][j] + dp[j][S-{i}] }
   where j belongs to set S, and j ≠ i

### Important Rules:
1. Each city must be visited exactly once
2. The path must return to the starting city
3. The total distance should be minimized

## Example with 4 Cities
Consider cities A, B, C, D with distances:

| From/To | A | B | C | D |
|---------|---|---|---|---|
| A       | 0 | 10| 15| 20|
| B       | 10| 0 | 35| 25|
| C       | 15| 35| 0 | 30|
| D       | 20| 25| 30| 0 |

## Step-by-Step Solution

### Step 1: Initialize (Single Cities)
Base case: Cost to visit a single city is 0

| City | {A} | {B} | {C} | {D} |
|------|-----|-----|-----|-----|
| A    | 0   | ∞   | ∞   | ∞   |
| B    | ∞   | 0   | ∞   | ∞   |
| C    | ∞   | ∞   | 0   | ∞   |
| D    | ∞   | ∞   | ∞   | 0   |

### Step 2: Calculate for Two Cities
For each pair of cities, calculate minimum cost:

#### Example: Subset {A,B}
From A to B:
- Cost = dist[A][B] + dp[B][{B}] = 10 + 0 = 10

From B to A:
- Cost = dist[B][A] + dp[A][{A}] = 10 + 0 = 10

| City | {A,B} | {A,C} | {A,D} | {B,C} | {B,D} | {C,D} |
|------|-------|-------|-------|-------|-------|-------|
| A    | 10    | 15    | 20    | ∞     | ∞     | ∞     |
| B    | 10    | ∞     | ∞     | 35    | 25    | ∞     |
| C    | ∞     | 15    | ∞     | 35    | ∞     | 30    |
| D    | ∞     | ∞     | 20    | ∞     | 25    | 30    |

### Step 3: Calculate for Three Cities

#### Example: Subset {A,B,C}
Starting at A:
1. Through B then C:
   - Cost = dist[A][B] + dp[B][{B,C}]
   - = 10 + 35 = 45
2. Through C then B:
   - Cost = dist[A][C] + dp[C][{B,C}]
   - = 15 + 35 = 50
Choose minimum: 45

Similar calculations for all three-city combinations:

| City | {A,B,C} | {A,B,D} | {A,C,D} | {B,C,D} |
|------|----------|----------|----------|----------|
| A    | 45       | 35       | 45       | ∞        |
| B    | 45       | 35       | ∞        | 55       |
| C    | 50       | ∞        | 45       | 55       |
| D    | ∞        | 45       | 45       | 55       |

### Step 4: Calculate for All Cities

#### Final Step Calculation
Starting at A:
1. Through B → C → D → A:
   - Cost = 10 + 35 + 30 + 20 = 95
2. Through B → D → C → A:
   - Cost = 10 + 25 + 30 + 15 = 80 ← Minimum
3. Through C → B → D → A:
   - Cost = 15 + 35 + 25 + 20 = 95
4. Through C → D → B → A:
   - Cost = 15 + 30 + 25 + 10 = 80
5. Through D → B → C → A:
   - Cost = 20 + 25 + 35 + 15 = 95
6. Through D → C → B → A:
   - Cost = 20 + 30 + 35 + 10 = 95

Final DP Table:

| City | {A,B,C,D} |
|------|------------|
| A    | 80         |
| B    | 80         |
| C    | 80         |
| D    | 80         |

### Optimal Path Construction
1. Start from city A (minimum in final column)
2. Next city: B (part of minimum path A → B → D → C → A)
3. Next city: D
4. Next city: C
5. Return to A

Final Path: A → B → D → C → A
Total Distance = 80

### Detailed Example of Path Selection

Let's examine why A → B → D → C → A (cost = 80) is better than A → B → C → D → A (cost = 95):

Path 1: A → B → D → C → A
1. A to B: 10
2. B to D: 25
3. D to C: 30
4. C to A: 15
Total: 80

Path 2: A → B → C → D → A
1. A to B: 10
2. B to C: 35
3. C to D: 30
4. D to A: 20
Total: 95

The key difference is in the middle segment:
- Path 1 uses B → D → C (cost: 25 + 30 = 55)
- Path 2 uses B → C → D (cost: 35 + 30 = 65)

### State Transition Table
Shows which city to visit next for each state:

| Current | Remaining Cities | Next City |
|---------|-----------------|-----------|
| A       | {B,C,D}        | B         |
| B       | {C,D}          | D         |
| D       | {C}            | C         |
| C       | {}             | A         |

### Problem Variations

1. **Asymmetric TSP**
   - Different costs for A→B and B→A
   - Current example is symmetric

2. **Multiple Traveling Salesmen**
   - k salesmen divide cities among themselves
   - Each salesman returns to depot

3. **TSP with Time Windows**
   - Cities must be visited within specific time slots
   - Adds temporal constraints

### Implementation Tips

1. **Bit Manipulation**
   For subset S = {A,B,C}:
   ```
   Binary: 0111
   A: 2^0 = 1
   B: 2^1 = 2
   C: 2^2 = 4
   Total: 7
   ```

2. **Memory Optimization**
   ```python
   # Instead of dp[n][2^n]
   dp = {}  # Use dictionary for sparse storage
   def key(city, subset):
       return (city, frozenset(subset))
   ```

3. **Path Recovery**
   ```python
   parent = {}  # Store predecessor for each state
   def recover_path(city, subset):
       if not subset:
           return [city]
       next_city = parent[city, frozenset(subset)]
       return [city] + recover_path(next_city, subset - {next_city})
   ```

### Tree Visualization of TSP Solution
For our 4-city example (A, B, C, D), let's visualize the decision tree starting from city A:

```
                                   A (Start)
                    ┌────────────┼────────────┐
                    B            C            D
            ┌───────┼───────┐    │            │
           C        D       C    B            B
        ┌───┘    ┌──┘    ┌──┘   │            │
        D        C       D      D            C
        │        │       │      │            │
        A        A       A      A            A

Cost of each complete path:
A→B→C→D→A = 95  [10 + 35 + 30 + 20]
A→B→D→C→A = 80* [10 + 25 + 30 + 15]  ← Optimal
A→C→B→D→A = 95  [15 + 35 + 25 + 20]
A→C→D→B→A = 80* [15 + 30 + 25 + 10]
A→D→B→C→A = 95  [20 + 25 + 35 + 15]
A→D→C→B→A = 95  [20 + 30 + 35 + 10]
```

### Level-by-Level Tree Analysis

#### Level 1: Starting from A
```
                A (Start)
        ┌───────┼───────┐
        B       C       D
```
- Options: Can go to B (10), C (15), or D (20)
- Best choice: B (10)

#### Level 2: After First City
```
                A
        ┌───────┼───────┐
        B       C       D
    ┌───┼───┐
    C   D   C
```
From B:
- Can go to C (35) or D (25)
- Best choice: D (25)
- Running total: 10 + 25 = 35

#### Level 3: After Second City
```
                A
        ┌───────┼───────┐
        B       C       D
    ┌───┼───┐
    C   D   C
    │   │   │
    D   C   D
```
From B→D:
- Only option: C (30)
- Running total: 10 + 25 + 30 = 65

#### Level 4: Return to Start
```
                A
        ┌───────┼───────┐
        B       C       D
    ┌───┼───┐
    C   D   C
    │   │   │
    D   C   D
    │   │   │
    A   A   A
```
From B→D→C:
- Must return to A (15)
- Final total: 10 + 25 + 30 + 15 = 80

### State Space Tree with Costs
```
                                A (0)
                    ┌────────────┼────────────┐
                 B (10)       C (15)       D (20)
            ┌───────┼───────┐
         C (45)  D (35)  C (45)
        ┌───┘    ┌──┘    ┌──┘
     D (75)   C (65)  D (70)
        │        │        │
     A (95)   A (80)   A (90)

Numbers in parentheses show cumulative cost
```

### Pruning the Search Tree
Using dynamic programming, we can avoid exploring redundant paths:

```
                                A (0)
                    ┌────────────┼────────────┐
                 B (10)       C (15)       D (20)
            ┌───────┼───────┐
         C (45)  D (35)*  C (45)
                ┌──┘
             C (65)
                │
             A (80)*

* Marks the optimal path segments
```

### Subset State Visualization
For city A with different subsets of remaining cities:
```
dp[A][{B}] = 10          dp[A][{C}] = 15          dp[A][{D}] = 20
     A                        A                         A
     │                        │                         │
     B                        C                         D

dp[A][{B,C}] = 45        dp[A][{B,D}] = 35        dp[A][{C,D}] = 45
     A                        A                         A
     │                        │                         │
   ┌─┴─┐                   ┌─┴─┐                    ┌─┴─┐
   B   C                   B   D                    C   D

dp[A][{B,C,D}] = 80
         A
         │
    ┌────┴────┐
    B         │
    │     ┌───┴───┐
    │     D       C
    └─────┘
```

This tree representation helps visualize:
1. All possible paths
2. Cost accumulation at each step
3. How dynamic programming avoids recalculating overlapping subproblems
4. The optimal path selection process

