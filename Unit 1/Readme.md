# Master Theorem

The Master Theorem provides a way to solve recurrence relations of the form:

\[ T(n) = aT\left(\frac{n}{b}\right) + f(n) \]

where:
- \( a \geq 1 \) is the number of subproblems in the recursion,
- \( b > 1 \) is the factor by which the subproblem size is reduced in each step,
- \( f(n) \) is an asymptotically positive function that represents the cost of the work done outside the recursive calls.

The theorem states that the solution to the recurrence is:

- **Case 1**: If \( f(n) = O(n^c) \) where \( c < \log_b a \), then \( T(n) = \Theta(n^{\log_b a}) \).
- **Case 2**: If \( f(n) = \Theta(n^c) \) where \( c = \log_b a \), then \( T(n) = \Theta(n^c \log n) \).
- **Case 3**: If \( f(n) = \Omega(n^c) \) where \( c > \log_b a \), and if \( a f\left(\frac{n}{b}\right) \leq k f(n) \) for some constant \( k < 1 \) and sufficiently large \( n \), then \( T(n) = \Theta(f(n)) \).

## Examples

### Case 1: \( f(n) = O(n^c) \) where \( c < \log_b a \)

1. **Recurrence**: \( T(n) = 2T\left(\frac{n}{2}\right) + n \)  
   **Solution**: \( \log_2 2 = 1 \), \( f(n) = n = O(n^1) \), so \( T(n) = \Theta(n \log n) \).

2. **Recurrence**: \( T(n) = 3T\left(\frac{n}{4}\right) + n \)  
   **Solution**: \( \log_4 3 \approx 0.792 \), \( f(n) = n = O(n^1) \), so \( T(n) = \Theta(n^{0.792}) \).

3. **Recurrence**: \( T(n) = 4T\left(\frac{n}{2}\right) + n \)  
   **Solution**: \( \log_2 4 = 2 \), \( f(n) = n = O(n^1) \), so \( T(n) = \Theta(n^2) \).

4. **Recurrence**: \( T(n) = 8T\left(\frac{n}{3}\right) + n \)  
   **Solution**: \( \log_3 8 \approx 1.893 \), \( f(n) = n = O(n^1) \), so \( T(n) = \Theta(n^{1.893}) \).

5. **Recurrence**: \( T(n) = 9T\left(\frac{n}{3}\right) + n \)  
   **Solution**: \( \log_3 9 = 2 \), \( f(n) = n = O(n^1) \), so \( T(n) = \Theta(n^2) \).

### Case 2: \( f(n) = \Theta(n^c) \) where \( c = \log_b a \)

1. **Recurrence**: \( T(n) = 2T\left(\frac{n}{2}\right) + n \log n \)  
   **Solution**: \( \log_2 2 = 1 \), \( f(n) = n \log n = \Theta(n^1 \log n) \), so \( T(n) = \Theta(n \log^2 n) \).

2. **Recurrence**: \( T(n) = 4T\left(\frac{n}{2}\right) + n^2 \)  
   **Solution**: \( \log_2 4 = 2 \), \( f(n) = n^2 = \Theta(n^2) \), so \( T(n) = \Theta(n^2 \log n) \).

3. **Recurrence**: \( T(n) = 3T\left(\frac{n}{3}\right) + n \log n \)  
   **Solution**: \( \log_3 3 = 1 \), \( f(n) = n \log n = \Theta(n^1 \log n) \), so \( T(n) = \Theta(n \log^2 n) \).

4. **Recurrence**: \( T(n) = 5T\left(\frac{n}{5}\right) + n \log n \)  
   **Solution**: \( \log_5 5 = 1 \), \( f(n) = n \log n = \Theta(n^1 \log n) \), so \( T(n) = \Theta(n \log^2 n) \).

5. **Recurrence**: \( T(n) = 2T\left(\frac{n}{4}\right) + n^{\log_4 2} \)  
   **Solution**: \( \log_4 2 = 0.5 \), \( f(n) = n^{0.5} = \Theta(n^{0.5}) \), so \( T(n) = \Theta(n^{0.5} \log n) \).

### Case 3: \( f(n) = \Omega(n^c) \) where \( c > \log_b a \)

1. **Recurrence**: \( T(n) = 2T\left(\frac{n}{2}\right) + n^2 \)  
   **Solution**: \( \log_2 2 = 1 \), \( f(n) = n^2 = \Omega(n^2) \), so \( T(n) = \Theta(n^2) \).

2. **Recurrence**: \( T(n) = 3T\left(\frac{n}{2}\right) + n^3 \)  
   **Solution**: \( \log_2 3 \approx 1.585 \), \( f(n) = n^3 = \Omega(n^3) \), so \( T(n) = \Theta(n^3) \).

3. **Recurrence**: \( T(n) = 4T\left(\frac{n}{3}\right) + n^3 \)  
   **Solution**: \( \log_3 4 \approx 1.261 \), \( f(n) = n^3 = \Omega(n^3) \), so \( T(n) = \Theta(n^3) \).

4. **Recurrence**: \( T(n) = 5T\left(\frac{n}{4}\right) + n^3 \)  
   **Solution**: \( \log_4 5 \approx 1.161 \), \( f(n) = n^3 = \Omega(n^3) \), so \( T(n) = \Theta(n^3) \).

5. **Recurrence**: \( T(n) = 6T\left(\frac{n}{5}\right) + n^4 \)  
   **Solution**: \( \log_5 6 \approx 1.113 \), \( f(n) = n^4 = \Omega(n^4) \), so \( T(n) = \Theta(n^4) \).
