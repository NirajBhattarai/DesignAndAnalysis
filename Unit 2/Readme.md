```
#include <stdio.h>

// Function to compute the GCD of two numbers
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

int main() {
    int num1, num2, result;

    // Input two numbers
    printf("Enter two numbers: ");
    scanf("%d %d", &num1, &num2);

    // Compute GCD
    result = gcd(num1, num2);

    // Output the result
    printf("GCD of %d and %d is: %d\n", num1, num2, result);

    return 0;
}

```