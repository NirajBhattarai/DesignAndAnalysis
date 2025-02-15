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
| 1   | 0     | 13,125 | 22,375 | 50,250 | 57,000 | -      | -      |
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | 57,000 | -      |
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
| 1   | 0     | 13,125 | 22,375 | 50,250 | 57,000 | 81,500 | 104,250|
| 2   | -     | 0      | 11,250 | 29,250 | 41,250 | 57,000 | 80,625 |
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


### Generating K Table (Split Points)
The K table stores the split points that give us the minimum cost for each subproblem. We generate it alongside our main DP table M.

For each subproblem M[i,j], we store in K[i,j] the value of k that gave us the minimum cost.

Procedure:
1. For each length L from 2 to n
2. For each starting point i from 1 to n-L+1
3. Calculate j = i+L-1
4. For each split point k from i to j-1:
   - Calculate cost = M[i,k] + M[k+1,j] + (rows(i) × cols(k) × cols(j))
   - If this cost is less than current minimum:
     * Update minimum cost in M[i,j]
     * Store k in K[i,j]

Example calculation for M[1,3]:
```
k = 1: cost = M[1,1] + M[2,3] + (35 × 15 × 30) = 0 + 11,250 + 15,750 = 27,000
k = 2: cost = M[1,2] + M[3,3] + (35 × 25 × 30) = 13,125 + 0 + 26,250 = 22,375 ← Minimum
Store K[1,3] = 2
```

Example calculation for M[2,4]:
```
k = 2: cost = M[2,2] + M[3,4] + (15 × 25 × 40) = 0 + 30,000 + 15,000 = 45,000
k = 3: cost = M[2,3] + M[4,4] + (15 × 30 × 40) = 11,250 + 0 + 18,000 = 29,250 ← Minimum
Store K[2,4] = 3
```

This process continues until we fill both M and K tables. The K table will then be used to reconstruct the optimal parenthesization.

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

## Brute Force Approach

The brute force approach for TSP involves generating all possible permutations of cities and finding the minimum cost path that visits all cities exactly once and returns to the starting city.

### Example with 4 Cities
Consider a graph with 4 cities (A, B, C, D) with the following distance matrix:

| From/To | A | B | C | D |
|---------|---|---|---|---|
| A       | 0 | 10| 15| 20|
| B       | 10| 0 | 35| 25|
| C       | 15| 35| 0 | 30|
| D       | 20| 25| 30| 0 |

### Decision Tree for TSP (Starting from City A)
```
                                                        A (0)
                            ┌──────────────────────────────┼──────────────────────────────┐
                            ↓10 [Cost to B = 10]           ↓15                            ↓20
                            B (10)                         C (15)                         D (20)
                ┌───────────┼─────────────────┐   ┌───────┼─────────────┐        ┌───────┼─────────────┐   
                ↓35         ↓25               ↓35 ↓10      ↓30          ↓35      ↓25      ↓30          ↓25
[First Branch]  C (45)      D (35)            C   B (25)   D (45)       B (50)   B (45)   C (50)       B (45)
Cost: A→B = 10  │           │                 │   │         │            │        │         │            │
      B→C = 35  ↓30         ↓30               ↓30 ↓25       ↓25          ↓25     ↓35       ↓35          ↓35
Total = 45      D (75)      C (65)            D   D (50)    B (70)       D (75)  C (80)   B (85)       C (80)
                │           │                 │   │         │            │        │         │            │
Cost: C→D = 30  ↓20         ↓15               ↓20 ↓20       ↓10          ↓20     ↓15       ↓10          ↓15
Total = 75      A (95)      A (80)            A   A (70)    A (80)       A (95)  A (95)   A (95)       A (95)
                │           │                 │   │         │            │        │         │            │
Cost: D→A = 20  └─────────[Path 1]───────────┘   └────────[Path 2]─────┘        └────────[Path 3]─────┘
Final = 95      [Not Optimal: 95]                 [Optimal: 80]                   [Not Optimal: 95]

Detailed Cost for Path 1 (A→B→C→D→A):
1. A → B: 10 (Initial edge)
2. B → C: 35 (Running total = 45)
3. C → D: 30 (Running total = 75)
4. D → A: 20 (Final total = 95)

[Cost]          [95]        [80]              [95] [70]     [80]         [95]    [95]     [95]         [95]
[Path]          [1]         [2*]              [3]  [4]      [5*]         [6]     [7]      [8]          [9]

Legend:
↓ Edge cost
(xx) Cumulative cost
[*] Optimal path
```

### C Implementation of Brute Force Approach
```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define MAX_CITIES 10

// Function to calculate total path cost
int calculatePathCost(int graph[MAX_CITIES][MAX_CITIES], int path[], int n) {
    int cost = 0;
    for (int i = 0; i < n - 1; i++) {
        cost += graph[path[i]][path[i + 1]];
    }
    // Add cost of returning to starting city
    cost += graph[path[n - 1]][path[0]];
    return cost;
}

// Function to print the path
void printPath(int path[], int n) {
    printf("Path: ");
    for (int i = 0; i < n; i++) {
        printf("%c ", path[i] + 'A');  // Convert to city letters (A, B, C, D)
    }
    printf("%c\n", path[0] + 'A');     // Return to start
}

// Function to generate all possible permutations
void findAllPaths(int graph[MAX_CITIES][MAX_CITIES], int path[], int visited[], 
                  int pos, int n, int *minCost, int bestPath[]) {
    if (pos == n) {
        // Calculate cost of current permutation
        int currentCost = calculatePathCost(graph, path, n);
        
        // Print current path and its cost
        printf("Found path: ");
        printPath(path, n);
        printf("Cost: %d\n", currentCost);
        
        // Update minimum cost if current cost is less
        if (currentCost < *minCost) {
            *minCost = currentCost;
            // Save the best path
            for (int i = 0; i < n; i++) {
                bestPath[i] = path[i];
            }
        }
        return;
    }

    // Try all unvisited cities
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            visited[i] = 1;
            path[pos] = i;
            findAllPaths(graph, path, visited, pos + 1, n, minCost, bestPath);
            visited[i] = 0;  // Backtrack
        }
    }
}

// Main TSP function
void solveTSP(int graph[MAX_CITIES][MAX_CITIES], int n) {
    int *path = (int *)malloc(n * sizeof(int));
    int *visited = (int *)calloc(n, sizeof(int));
    int *bestPath = (int *)malloc(n * sizeof(int));
    int minCost = INT_MAX;

    // Start from city 0 (A)
    path[0] = 0;
    visited[0] = 1;

    printf("\nFinding all possible paths...\n");
    findAllPaths(graph, path, visited, 1, n, &minCost, bestPath);

    printf("\nOptimal Solution:\n");
    printf("Minimum Cost: %d\n", minCost);
    printf("Best ");
    printPath(bestPath, n);

    free(path);
    free(visited);
    free(bestPath);
}

int main() {
    // Example with 4 cities (A, B, C, D)
    int n = 4;
    int graph[MAX_CITIES][MAX_CITIES] = {
        {0,  10, 15, 20},
        {10, 0,  35, 25},
        {15, 35, 0,  30},
        {20, 25, 30, 0}
    };

    printf("Traveling Salesman Problem (Brute Force)\n");
    printf("\nDistance Matrix:\n");
    printf("  A  B  C  D\n");
    for (int i = 0; i < n; i++) {
        printf("%c ", i + 'A');
        for (int j = 0; j < n; j++) {
            printf("%2d ", graph[i][j]);
        }
        printf("\n");
    }

    solveTSP(graph, n);
    return 0;
}
```

Sample Output:
```
Traveling Salesman Problem (Brute Force)

Distance Matrix:
  A  B  C  D
A  0 10 15 20 
B 10  0 35 25 
C 15 35  0 30 
D 20 25 30  0 

Finding all possible paths...
Found path: A B C D A
Cost: 95
Found path: A B D C A
Cost: 80
Found path: A C B D A
Cost: 95
Found path: A C D B A
Cost: 80
Found path: A D B C A
Cost: 95
Found path: A D C B A
Cost: 95

Optimal Solution:
Minimum Cost: 80
Best Path: A B D C A
```

### Dynamic Programming Approach for TSP

Consider a graph with 6 cities (A, B, C, D, E, F) with the following distance matrix:

| From/To | A | B | C | D | E | F |
|---------|---|---|---|---|---|---|
| A       | 0 | 10| 15| 20| 25| 30|
| B       | 10| 0 | 35| 25| 30| 20|
| C       | 15| 35| 0 | 30| 20| 25|
| D       | 20| 25| 30| 0 | 15| 10|
| E       | 25| 30| 20| 15| 0 | 35|
| F       | 30| 20| 25| 10| 35| 0 |

### Step-by-Step Solution

#### Step 1: Base Cases (S = Φ, empty set)
Calculate the cost of returning directly to the start city A from all other cities:
- Cost(B,Φ,A) = d(B,A) = 10
- Cost(C,Φ,A) = d(C,A) = 15
- Cost(D,Φ,A) = d(D,A) = 20
- Cost(E,Φ,A) = d(E,A) = 25
- Cost(F,Φ,A) = d(F,A) = 30

#### Step 2: One city in set S (S = {B})
Calculate minimum cost when B is fixed and we need to visit other cities before returning to A:
- Cost(C,{B},A) = d[C,B] + Cost(B,Φ,A) = 35 + 10 = 45
- Cost(D,{B},A) = d[D,B] + Cost(B,Φ,A) = 25 + 10 = 35
- Cost(E,{B},A) = d[E,B] + Cost(B,Φ,A) = 30 + 10 = 40
- Cost(F,{B},A) = d[F,B] + Cost(B,Φ,A) = 20 + 10 = 30

#### Step 3: One city in set S (S = {C})
Calculate minimum cost when C is fixed and we need to visit other cities before returning to A:
- Cost(B,{C},A) = d[B,C] + Cost(C,Φ,A) = 35 + 15 = 50
- Cost(D,{C},A) = d[D,C] + Cost(C,Φ,A) = 30 + 15 = 45
- Cost(E,{C},A) = d[E,C] + Cost(C,Φ,A) = 20 + 15 = 35
- Cost(F,{C},A) = d[F,C] + Cost(C,Φ,A) = 25 + 15 = 40

#### Step 4: One city in set S (S = {D})
Calculate minimum cost when D is fixed and we need to visit other cities before returning to A:
- Cost(B,{D},A) = d[B,D] + Cost(D,Φ,A) = 25 + 20 = 45
- Cost(C,{D},A) = d[C,D] + Cost(D,Φ,A) = 30 + 20 = 50
- Cost(E,{D},A) = d[E,D] + Cost(D,Φ,A) = 15 + 20 = 35
- Cost(F,{D},A) = d[F,D] + Cost(D,Φ,A) = 10 + 20 = 30

#### Step 5: One city in set S (S = {E})
Calculate minimum cost when E is fixed and we need to visit other cities before returning to A:
- Cost(B,{E},A) = d[B,E] + Cost(E,Φ,A) = 30 + 25 = 55
- Cost(C,{E},A) = d[C,E] + Cost(E,Φ,A) = 20 + 25 = 45
- Cost(D,{E},A) = d[D,E] + Cost(E,Φ,A) = 15 + 25 = 40
- Cost(F,{E},A) = d[F,E] + Cost(E,Φ,A) = 35 + 25 = 60

#### Step 6: One city in set S (S = {F})
Calculate minimum cost when F is fixed and we need to visit other cities before returning to A:
- Cost(B,{F},A) = d[B,F] + Cost(F,Φ,A) = 20 + 30 = 50
- Cost(C,{F},A) = d[C,F] + Cost(F,Φ,A) = 25 + 30 = 55
- Cost(D,{F},A) = d[D,F] + Cost(F,Φ,A) = 10 + 30 = 40
- Cost(E,{F},A) = d[E,F] + Cost(F,Φ,A) = 35 + 30 = 65

#### Step 7: Two cities in set S (S = {B,C})
Calculate minimum cost when visiting both B and C before returning to A:
- Cost(D,{B,C},A) = min{
  d[D,B] + Cost(B,{C},A),
  d[D,C] + Cost(C,{B},A)
} = min{25 + 50, 30 + 50} = 75
- Cost(E,{B,C},A) = min{
  d[E,B] + Cost(B,{C},A),
  d[E,C] + Cost(C,{B},A)
} = min{30 + 50, 20 + 50} = 70
- Cost(F,{B,C},A) = min{
  d[F,B] + Cost(B,{C},A),
  d[F,C] + Cost(C,{B},A)
} = min{20 + 50, 25 + 50} = 70

#### Step 8: Two cities in set S (S = {B,D})
Calculate minimum cost when visiting both B and D before returning to A:
- Cost(C,{B,D},A) = min{
  d[C,B] + Cost(B,{D},A),
  d[C,D] + Cost(D,{B},A)
} = min{35 + 45, 30 + 45} = 75
- Cost(E,{B,D},A) = min{
  d[E,B] + Cost(B,{D},A),
  d[E,D] + Cost(D,{B},A)
} = min{30 + 45, 15 + 45} = 60
- Cost(F,{B,D},A) = min{
  d[F,B] + Cost(B,{D},A),
  d[F,D] + Cost(D,{B},A)
} = min{20 + 45, 10 + 45} = 55

#### Step 9: Two cities in set S (S = {B,E})
Calculate minimum cost when visiting both B and E before returning to A:
- Cost(C,{B,E},A) = min{
  d[C,B] + Cost(B,{E},A),
  d[C,E] + Cost(E,{B},A)
} = min{35 + 40, 20 + 55} = 75
- Cost(D,{B,E},A) = min{
  d[D,B] + Cost(B,{E},A),
  d[D,E] + Cost(E,{B},A)
} = min{25 + 40, 15 + 55} = 65
- Cost(F,{B,E},A) = min{
  d[F,B] + Cost(B,{E},A),
  d[F,E] + Cost(E,{B},A)
} = min{20 + 40, 35 + 55} = 60

#### Step 10: Two cities in set S (S = {B,F})
Calculate minimum cost when visiting both B and F before returning to A:
- Cost(C,{B,F},A) = min{
  d[C,B] + Cost(B,{F},A),
  d[C,F] + Cost(F,{B},A)
} = min{35 + 50, 25 + 50} = 75
- Cost(D,{B,F},A) = min{
  d[D,B] + Cost(B,{F},A),
  d[D,F] + Cost(F,{B},A)
} = min{25 + 50, 10 + 50} = 60
- Cost(E,{B,F},A) = min{
  d[E,B] + Cost(B,{F},A),
  d[E,F] + Cost(F,{B},A)
} = min{30 + 50, 35 + 50} = 80

#### Step 11: Two cities in set S (S = {C,D})
Calculate minimum cost when visiting both C and D before returning to A:
- Cost(B,{C,D},A) = min{
  d[B,C] + Cost(C,{D},A),
  d[B,D] + Cost(D,{C},A)
} = min{35 + 45, 25 + 50} = 75
- Cost(E,{C,D},A) = min{
  d[E,C] + Cost(C,{D},A),
  d[E,D] + Cost(D,{C},A)
} = min{20 + 45, 15 + 50} = 65
- Cost(F,{C,D},A) = min{
  d[F,C] + Cost(C,{D},A),
  d[F,D] + Cost(D,{C},A)
} = min{25 + 45, 10 + 50} = 60

#### Step 12: Two cities in set S (S = {C,E})
Calculate minimum cost when visiting both C and E before returning to A:
- Cost(B,{C,E},A) = min{
  d[B,C] + Cost(C,{E},A),
  d[B,E] + Cost(E,{C},A)
} = min{35 + 45, 30 + 45} = 75
- Cost(D,{C,E},A) = min{
  d[D,C] + Cost(C,{E},A),
  d[D,E] + Cost(E,{C},A)
} = min{30 + 45, 15 + 45} = 60
- Cost(F,{C,E},A) = min{
  d[F,C] + Cost(C,{E},A),
  d[F,E] + Cost(E,{C},A)
} = min{25 + 45, 35 + 45} = 70

#### Step 13: Two cities in set S (S = {C,F})
Calculate minimum cost when visiting both C and F before returning to A:
- Cost(B,{C,F},A) = min{
  d[B,C] + Cost(C,{F},A),
  d[B,F] + Cost(F,{C},A)
} = min{35 + 40, 20 + 55} = 75
- Cost(D,{C,F},A) = min{
  d[D,C] + Cost(C,{F},A),
  d[D,F] + Cost(F,{C},A)
} = min{30 + 40, 10 + 55} = 65
- Cost(E,{C,F},A) = min{
  d[E,C] + Cost(C,{F},A),
  d[E,F] + Cost(F,{C},A)
} = min{20 + 40, 35 + 55} = 60

#### Step 14: Two cities in set S (S = {D,E})
Calculate minimum cost when visiting both D and E before returning to A:
- Cost(B,{D,E},A) = min{
  d[B,D] + Cost(D,{E},A),
  d[B,E] + Cost(E,{D},A)
} = min{25 + 40, 30 + 40} = 65
- Cost(C,{D,E},A) = min{
  d[C,D] + Cost(D,{E},A),
  d[C,E] + Cost(E,{D},A)
} = min{30 + 40, 20 + 40} = 60
- Cost(F,{D,E},A) = min{
  d[F,D] + Cost(D,{E},A),
  d[F,E] + Cost(E,{D},A)
} = min{10 + 40, 35 + 40} = 50

#### Step 15: Three cities in set S (S = {B,C,D})
Calculate minimum cost when visiting B, C, and D before returning to A:
- Cost(E,{B,C,D},A) = min{
  d[E,B] + Cost(B,{C,D},A),
  d[E,C] + Cost(C,{B,D},A),
  d[E,D] + Cost(D,{B,C},A)
} = min{30 + 75, 20 + 75, 15 + 75} = 90
- Cost(F,{B,C,D},A) = min{
  d[F,B] + Cost(B,{C,D},A),
  d[F,C] + Cost(C,{B,D},A),
  d[F,D] + Cost(D,{B,C},A)
} = min{20 + 75, 25 + 75, 10 + 75} = 85

#### Step 16: Three cities in set S (S = {B,C,E})
Calculate minimum cost when visiting B, C, and E before returning to A:
- Cost(D,{B,C,E},A) = min{
  d[D,B] + Cost(B,{C,E},A),
  d[D,C] + Cost(C,{B,E},A),
  d[D,E] + Cost(E,{B,C},A)
} = min{25 + 75, 30 + 75, 15 + 70} = 85
- Cost(F,{B,C,E},A) = min{
  d[F,B] + Cost(B,{C,E},A),
  d[F,C] + Cost(C,{B,E},A),
  d[F,E] + Cost(E,{B,C},A)
} = min{20 + 75, 25 + 75, 35 + 70} = 95

#### Step 17: Three cities in set S (S = {B,C,F})
Calculate minimum cost when visiting B, C, and F before returning to A:
- Cost(D,{B,C,F},A) = min{
  d[D,B] + Cost(B,{C,F},A),
  d[D,C] + Cost(C,{B,F},A),
  d[D,F] + Cost(F,{B,C},A)
} = min{25 + 75, 30 + 75, 10 + 70} = 80
- Cost(E,{B,C,F},A) = min{
  d[E,B] + Cost(B,{C,F},A),
  d[E,C] + Cost(C,{B,F},A),
  d[E,F] + Cost(F,{B,C},A)
} = min{30 + 75, 20 + 75, 35 + 70} = 95

#### Step 18: Three cities in set S (S = {B,D,E})
Calculate minimum cost when visiting B, D, and E before returning to A:
- Cost(C,{B,D,E},A) = min{
  d[C,B] + Cost(B,{D,E},A),
  d[C,D] + Cost(D,{B,E},A),
  d[C,E] + Cost(E,{B,D},A)
} = min{35 + 65, 30 + 60, 20 + 65} = 85
- Cost(F,{B,D,E},A) = min{
  d[F,B] + Cost(B,{D,E},A),
  d[F,D] + Cost(D,{B,E},A),
  d[F,E] + Cost(E,{B,D},A)
} = min{20 + 65, 10 + 60, 35 + 65} = 70

#### Step 19: Three cities in set S (S = {B,D,F})
Calculate minimum cost when visiting B, D, and F before returning to A:
- Cost(C,{B,D,F},A) = min{
  d[C,B] + Cost(B,{D,F},A),
  d[C,D] + Cost(D,{B,F},A),
  d[C,F] + Cost(F,{B,D},A)
} = min{35 + 60, 30 + 60, 25 + 55} = 80
- Cost(E,{B,D,F},A) = min{
  d[E,B] + Cost(B,{D,F},A),
  d[E,D] + Cost(D,{B,F},A),
  d[E,F] + Cost(F,{B,D},A)
} = min{30 + 60, 15 + 60, 35 + 55} = 75

#### Step 20: Three cities in set S (S = {B,E,F})
Calculate minimum cost when visiting B, E, and F before returning to A:
- Cost(C,{B,E,F},A) = min{
  d[C,B] + Cost(B,{E,F},A),
  d[C,E] + Cost(E,{B,F},A),
  d[C,F] + Cost(F,{B,E},A)
} = min{35 + 80, 20 + 80, 25 + 60} = 85
- Cost(D,{B,E,F},A) = min{
  d[D,B] + Cost(B,{E,F},A),
  d[D,E] + Cost(E,{B,F},A),
  d[D,F] + Cost(F,{B,E},A)
} = min{25 + 80, 15 + 80, 10 + 60} = 70

#### Step 21: Three cities in set S (S = {C,D,E})
Calculate minimum cost when visiting C, D, and E before returning to A:
- Cost(B,{C,D,E},A) = min{
  d[B,C] + Cost(C,{D,E},A),
  d[B,D] + Cost(D,{C,E},A),
  d[B,E] + Cost(E,{C,D},A)
} = min{35 + 65, 25 + 60, 30 + 60} = 85
- Cost(F,{C,D,E},A) = min{
  d[F,C] + Cost(C,{D,E},A),
  d[F,D] + Cost(D,{C,E},A),
  d[F,E] + Cost(E,{C,D},A)
} = min{25 + 65, 10 + 60, 35 + 60} = 70

#### Step 22: Three cities in set S (S = {C,D,F})
Calculate minimum cost when visiting C, D, and F before returning to A:
- Cost(B,{C,D,F},A) = min{
  d[B,C] + Cost(C,{D,F},A),
  d[B,D] + Cost(D,{C,F},A),
  d[B,F] + Cost(F,{C,D},A)
} = min{35 + 65, 25 + 65, 20 + 60} = 80
- Cost(E,{C,D,F},A) = min{
  d[E,C] + Cost(C,{D,F},A),
  d[E,D] + Cost(D,{C,F},A),
  d[E,F] + Cost(F,{C,D},A)
} = min{20 + 65, 15 + 65, 35 + 60} = 80

#### Step 23: Three cities in set S (S = {C,E,F})
Calculate minimum cost when visiting C, E, and F before returning to A:
- Cost(B,{C,E,F},A) = min{
  d[B,C] + Cost(C,{E,F},A),
  d[B,E] + Cost(E,{C,F},A),
  d[B,F] + Cost(F,{C,E},A)
} = min{35 + 70, 30 + 70, 20 + 60} = 80
- Cost(D,{C,E,F},A) = min{
  d[D,C] + Cost(C,{E,F},A),
  d[D,E] + Cost(E,{C,F},A),
  d[D,F] + Cost(F,{C,E},A)
} = min{30 + 70, 15 + 70, 10 + 60} = 70

#### Step 24: Three cities in set S (S = {D,E,F})
Calculate minimum cost when visiting D, E, and F before returning to A:
- Cost(B,{D,E,F},A) = min{
  d[B,D] + Cost(D,{E,F},A),
  d[B,E] + Cost(E,{D,F},A),
  d[B,F] + Cost(F,{D,E},A)
} = min{25 + 50, 30 + 50, 20 + 50} = 70
- Cost(C,{D,E,F},A) = min{
  d[C,D] + Cost(D,{E,F},A),
  d[C,E] + Cost(E,{D,F},A),
  d[C,F] + Cost(F,{D,E},A)
} = min{30 + 50, 20 + 50, 25 + 50} = 70

#### Step 25: Four cities in set S (S = {B,C,D,E})
Calculate minimum cost when visiting B, C, D, and E before returning to A:
- Cost(F,{B,C,D,E},A) = min{
  d[F,B] + Cost(B,{C,D,E},A),
  d[F,C] + Cost(C,{B,D,E},A),
  d[F,D] + Cost(D,{B,C,E},A),
  d[F,E] + Cost(E,{B,C,D},A)
} = min{20 + 90, 25 + 90, 10 + 90, 35 + 90} = 100

#### Final Step: Optimal Solution (S = {B,C,D,E,F})
The minimum cost path starting from A, visiting all cities exactly once, and returning to A is:
Cost(A,{B,C,D,E,F},A) = min{
  d[A,B] + Cost(B,{C,D,E,F},A),
  d[A,C] + Cost(C,{B,D,E,F},A),
  d[A,D] + Cost(D,{B,C,E,F},A),
  d[A,E] + Cost(E,{B,C,D,F},A),
  d[A,F] + Cost(F,{B,C,D,E},A)
} = min{10 + 100, 15 + 100, 20 + 100, 25 + 100, 30 + 100} = 110

The optimal path can be reconstructed by backtracking through the DP table:
A → B → C → D → E → F → A with total cost 110.

### Time and Space Complexity
- Time Complexity: O(n²2ⁿ) where n is the number of cities
- Space Complexity: O(n2ⁿ) for storing the DP states

### Explanation

1. **Distance Matrix**: The distance matrix is expanded to include 6 cities, with new distances added for cities E and F.

2. **Code Adjustments**: The `MAX_CITIES` constant is updated to 6, and the `graph` array is expanded to accommodate the new cities and their distances.

3. **DP Table Initialization**: The `dp` array is initialized to handle the increased number of states due to the additional cities.

This updated implementation will calculate the minimum cost path for visiting all 6 cities and returning to the starting city using dynamic programming.


### C Implementation using Dynamic Programming
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <limits.h>

#define MAX_CITIES 6
#define INF INT_MAX

int dp[1 << MAX_CITIES][MAX_CITIES];
int visited_all;

// Function to get minimum cost using DP
int tsp(int mask, int pos, int graph[MAX_CITIES][MAX_CITIES]) {
    // If all cities are visited
    if (mask == visited_all) {
        return graph[pos][0];  // Return to starting city
    }
    
    // If this state is already computed
    if (dp[mask][pos] != -1) {
        return dp[mask][pos];
    }
    
    int ans = INF;
    
    // Try to visit all unvisited cities
    for (int city = 0; city < MAX_CITIES; city++) {
        if ((mask & (1 << city)) == 0) {  // If city is not visited
            int newAns = graph[pos][city] + tsp(mask | (1 << city), city, graph);
            if (newAns < ans) {
                ans = newAns;
            }
        }
    }
    
    return dp[mask][pos] = ans;
}

void solveTSP_DP(int graph[MAX_CITIES][MAX_CITIES]) {
    // Initialize visited_all and dp array
    visited_all = (1 << MAX_CITIES) - 1;
    memset(dp, -1, sizeof(dp));
    
    // Start from city 0 with only first city visited
    int minCost = tsp(1, 0, graph);
    
    printf("\nDP Solution:\n");
    printf("Minimum Cost: %d\n", minCost);
    
    // Print DP table state
    printf("\nDP Table State (Partial View):\n");
    for (int mask = 0; mask < (1 << MAX_CITIES); mask++) {
        for (int pos = 0; pos < MAX_CITIES; pos++) {
            if (dp[mask][pos] != -1) {
                printf("dp[%d][%d] = %d\n", mask, pos, dp[mask][pos]);
            }
        }
    }
}

int main() {
    int graph[MAX_CITIES][MAX_CITIES] = {
        {0,  10, 15, 20, 25, 30},
        {10, 0,  35, 25, 30, 20},
        {15, 35, 0,  30, 20, 25},
        {20, 25, 30, 0,  15, 10},
        {25, 30, 20, 15, 0,  35},
        {30, 20, 25, 10, 35, 0}
    };

    printf("TSP using Dynamic Programming\n");
    printf("\nDistance Matrix:\n");
    printf("  A  B  C  D  E  F\n");
    for (int i = 0; i < MAX_CITIES; i++) {
        printf("%c ", i + 'A');
        for (int j = 0; j < MAX_CITIES; j++) {
            printf("%2d ", graph[i][j]);
        }
        printf("\n");
    }

    solveTSP_DP(graph);
    return 0;
}
```

# 0/1 Knapsack Problem

## Problem Definition
The 0/1 Knapsack problem is a classic optimization problem where we need to select items with given weights and values to maximize total value while keeping the total weight under a given capacity.

## Example Problem
Consider a knapsack with capacity W = 10 kg and 10 items with following weights and values:

| Item | Weight (kg) | Value ($) |
|------|-------------|-----------|
| 1    | 2          | 20        |
| 2    | 3          | 30        |
| 3    | 4          | 45        |
| 4    | 1          | 15        |
| 5    | 3          | 25        |
| 6    | 2          | 35        |
| 7    | 5          | 55        |
| 8    | 1          | 10        |
| 9    | 4          | 50        |
| 10   | 2          | 40        |

## Solution Steps

### 1. Create DP Table
- Create a table with items (n+1) as rows and weights (W+1) as columns
- Rows: 0 to 10 (items)
- Columns: 0 to 10 (weights)

### 2. Initialize Base Cases
- First row (no items): All zeros
- First column (zero weight): All zeros

### 3. Fill DP Table - Step by Step Construction

#### Step 1: Row 1 (Item 1: 2kg, $20)
For w < 2: Copy from above (can't include item)
For w ≥ 2: max(20 + dp[0][w-2], dp[0][w])

| i\w | 0 | 1 | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|---|----|----|----|----|----|----|----|----|-----|
| 0   | 0 | 0 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |
| 1   | 0 | 0 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 |

Example calculation for w=3:
- Can't add new item (20 + dp[0][1] = 20)
- Keep previous (dp[0][3] = 0)
- Take maximum: max(20, 0) = 20

#### Step 2: Row 2 (Item 2: 3kg, $30)
For w < 3: Copy from above
For w ≥ 3: max(30 + dp[1][w-3], dp[1][w])

| i\w | 0 | 1 | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|---|----|----|----|----|----|----|----|----|-----|
| 0   | 0 | 0 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |
| 1   | 0 | 0 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 |
| 2   | 0 | 0 | 20 | 30 | 30 | 50 | 50 | 50 | 50 | 50 | 50 |

Example calculation for w=5:
- Add new item (30 + dp[1][2] = 30 + 20 = 50)
- Keep previous (dp[1][5] = 20)
- Take maximum: max(50, 20) = 50

#### Step 3: Row 3 (Item 3: 4kg, $45)
For w < 4: Copy from above
For w ≥ 4: max(45 + dp[2][w-4], dp[2][w])

| i\w | 0 | 1 | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|---|----|----|----|----|----|----|----|----|-----|
| 0   | 0 | 0 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |
| 1   | 0 | 0 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 |
| 2   | 0 | 0 | 20 | 30 | 30 | 50 | 50 | 50 | 50 | 50 | 50 |
| 3   | 0 | 0 | 20 | 30 | 45 | 50 | 65 | 75 | 75 | 95 | 95 |

Example calculation for w=6:
- Add new item (45 + dp[2][2] = 45 + 20 = 65)
- Keep previous (dp[2][6] = 50)
- Take maximum: max(65, 50) = 65

#### Step 4: Row 4 (Item 4: 1kg, $15)
For w ≥ 1: max(15 + dp[3][w-1], dp[3][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 3   | 0 | 0  | 20 | 30 | 45 | 50 | 65 | 75 | 75 | 95 | 95 |
| 4   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|

Example calculation for w=7:
- Add new item (15 + dp[3][6] = 15 + 65 = 80)
- Keep previous (dp[3][7] = 75)
- Take maximum: max(80, 75) = 80

#### Step 5: Row 5 (Item 5: 3kg, $25)
For w ≥ 3: max(25 + dp[4][w-3], dp[4][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 4   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|
| 5   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|

Example calculation for w=8:
- Add new item (25 + dp[4][5] = 25 + 60 = 85)
- Keep previous (dp[4][8] = 90)
- Take maximum: max(85, 90) = 90

#### Step 6: Row 6 (Item 6: 2kg, $35)
For w ≥ 2: max(35 + dp[5][w-2], dp[5][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 5   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|
| 6   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 115|

Example calculation for w=4:
- Add new item (35 + dp[5][2] = 35 + 20 = 55)
- Keep previous (dp[5][4] = 45)
- Take maximum: max(55, 45) = 55

#### Step 7: Row 7 (Item 7: 5kg, $55)
For w ≥ 5: max(55 + dp[6][w-5], dp[6][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 6   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 115|
| 7   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|

Example calculation for w=10:
- Add new item (55 + dp[6][5] = 55 + 70 = 125)
- Keep previous (dp[6][10] = 115)
- Take maximum: max(125, 115) = 125

#### Step 8: Row 8 (Item 8: 1kg, $10)
For w ≥ 1: max(10 + dp[7][w-1], dp[7][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 7   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|
| 8   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|

Example calculation for w=6:
- Add new item (10 + dp[7][5] = 10 + 70 = 80)
- Keep previous (dp[7][6] = 80)
- Take maximum: max(80, 80) = 80
Note: No improvement as item 8's value/weight ratio is lower than previous items

#### Step 9: Row 9 (Item 9: 4kg, $50)
For w ≥ 4: max(50 + dp[8][w-4], dp[8][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 8   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|
| 9   | 0 | 15 | 35 | 50 | 55 | 70 | 85 | 90 | 105| 120| 135|

Example calculation for w=8:
- Add new item (50 + dp[8][4] = 50 + 55 = 105)
- Keep previous (dp[8][8] = 100)
- Take maximum: max(105, 100) = 105

#### Step 10: Row 10 (Item 10: 2kg, $40)
For w ≥ 2: max(40 + dp[9][w-2], dp[9][w])

| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|----|
| 9   | 0 | 15 | 35 | 50 | 55 | 70 | 85 | 90 | 105| 120| 135|
| 10  | 0 | 15 | 40 | 55 | 75 | 90 | 95 | 115| 130| 135| 155|

Example calculation for w=10:
- Add new item (40 + dp[9][8] = 40 + 105 = 145)
- Keep previous (dp[9][10] = 135)
- Take maximum: max(145, 135) = 155

Key observations from the step-by-step construction:

1. Value Accumulation:
   - Each row represents considering one more item
   - Values generally increase or stay the same as more items become available

2. Weight Constraints:
   - Items can only be added when remaining weight is sufficient
   - Smaller items (like item 4, 1kg) provide more flexibility

3. Value/Weight Trade-offs:
   - Some items (like item 8) don't improve the solution
   - Higher value items may not be chosen if they take too much weight

4. Optimal Substructure:
   - Each cell uses results from previous row
   - Final solution builds upon optimal solutions to smaller subproblems

The final cell dp[10][10] = 155 represents the maximum possible value achievable with the 10kg weight limit, considering all items.

### 4. Final DP Table
| i\w | 0 | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 |
|-----|---|----|----|----|----|----|----|----|----|----|-----|
| 0   | 0 | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  | 0  |
| 1   | 0 | 0  | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 | 20 |
| 2   | 0 | 0  | 20 | 30 | 30 | 50 | 50 | 50 | 50 | 50 | 50 |
| 3   | 0 | 0  | 20 | 30 | 45 | 50 | 65 | 75 | 75 | 95 | 95 |
| 4   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|
| 5   | 0 | 15 | 20 | 35 | 45 | 60 | 65 | 80 | 90 | 95 | 110|
| 6   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 115|
| 7   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|
| 8   | 0 | 15 | 35 | 50 | 55 | 70 | 80 | 85 | 100| 105| 125|
| 9   | 0 | 15 | 35 | 50 | 55 | 70 | 85 | 90 | 105| 120| 135|
| 10  | 0 | 15 | 40 | 55 | 75 | 90 | 95 | 115| 130| 135| 155|

### 5. Find Selected Items
Backtrack through the DP table:
1. Start at dp[10][10] = 155
2. If dp[i][w] ≠ dp[i-1][w], item i was selected
   - Subtract item's weight from w
   - Continue with dp[i-1][w-weight[i]]
3. Otherwise, continue with dp[i-1][w]

Selected items:
- Item 10 (2kg, $40)
- Item 9 (4kg, $50)
- Item 6 (2kg, $35)
- Item 4 (1kg, $15)

## Final Solution
- Maximum value: $155
- Selected items: 4, 6, 9, and 10
- Total weight used: 9kg

## Implementation

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_ITEMS 11
#define MAX_WEIGHT 11

int max(int a, int b) {
    return (a > b) ? a : b;
}

void knapsack(int W, int weights[], int values[], int n) {
    int dp[MAX_ITEMS][MAX_WEIGHT];
    
    // Initialize base cases
    for (int w = 0; w <= W; w++)
        dp[0][w] = 0;
    for (int i = 0; i <= n; i++)
        dp[i][0] = 0;
    
    // Fill dp table
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= W; w++) {
            if (weights[i-1] <= w)
                dp[i][w] = max(values[i-1] + dp[i-1][w-weights[i-1]], 
                              dp[i-1][w]);
            else
                dp[i][w] = dp[i-1][w];
        }
    }
    
    // Print result and selected items
    printf("Maximum value: $%d\n", dp[n][W]);
    
    int w = W;
    int i = n;
    printf("Selected items:\n");
    while (i > 0 && w > 0) {
        if (dp[i][w] != dp[i-1][w]) {
            printf("Item %d (Weight: %dkg, Value: $%d)\n", 
                   i, weights[i-1], values[i-1]);
            w = w - weights[i-1];
        }
        i--;
    }
}
```

## Complexity Analysis
- Time Complexity: O(nW) where n is number of items and W is knapsack capacity
- Space Complexity: O(nW) for the DP table

## Applications
1. Resource allocation in computing
2. Cargo loading
3. Investment decision making
4. Portfolio optimization
5. Project selection under constraints

