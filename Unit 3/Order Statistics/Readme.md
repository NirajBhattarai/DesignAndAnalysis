# CHAPTER 10: MEDIANS AND ORDER STATISTICS

The _ith_ order statistic of a set of _n_ elements is the _ith_ smallest element. For example, the minimum of a set of elements is the first order statistic (_i = 1_), and the maximum is the _nth_ order statistic (_i = n_). A median, informally, is the "halfway point" of the set. When _n_ is odd, the median is unique, occurring at _i = (n + 1)/2_. When _n_ is even, there are two medians, occurring at _i = n/2_ and _i = n/2 + 1_. Thus, regardless of the parity of _n_, medians occur at _i = (n + 1)/2_ and _i = (n + 1)/2_.

This chapter addresses the problem of selecting the _ith_ order statistic from a set of _n_ distinct numbers. We assume for convenience that the set contains distinct numbers, although virtually everything that we do extends to the situation in which a set contains repeated values. The selection problem can be specified formally as follows:

**Input**: A set _A_ of _n_ (distinct) numbers and a number _i_, with 1 ≤ _i_ ≤ _n_.

**Output**: The element _x ∈ A_ that is larger than exactly _i -1_ other elements of _A_.

The selection problem can be solved in _O(n lg n)_ time, since we can sort the numbers using heapsort or merge sort and then simply index the _ith_ element in the output array. There are faster algorithms, however.

In Section we examine the problem of selecting the minimum and maximum of a set of elements. More interesting is the general selection problem, which is investigated in the subsequent two sections.

## Selection(A, n):
1. Sort the array A in non-decreasing order
2. Return A[n-1]


```
#include <stdio.h>
#include <stdbool.h>

// Simple Bubble Sort Function
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        bool swapped = false;
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                swapped = true;
            }
        }
        if (!swapped) {
            break;
        }
    }
}

int selection(int arr[], int size, int n) {
    bubbleSort(arr, size);
    return arr[n-1];
}

int main() {
    int arr[] = {12, 11, 15, 10, 9, 1, 2, 3, 7, 8};
    int n = 4;
    int size = sizeof(arr) / sizeof(arr[0]);

    printf("The %dth smallest element is %d\n", n, selection(arr, size, n));
    return 0;
}

```

```
QuickSort(A, low, high):
1. if low < high:
2.     pivot = Partition(A, low, high)
3.     QuickSort(A, low, pivot-1)
4.     QuickSort(A, pivot+1, high)

Partition(A, low, high):
1. pivot = A[high]
2. i = low - 1
3. for j from low to high-1:
4.     if A[j] < pivot:
5.         i = i + 1
6.         swap A[i] and A[j]
7. swap A[i+1] and A[high]
8. return i+1

Selection(A, n):
1. QuickSort(A, 0, length(A)-1)
2. Return A[n-1]

```

```
#include <stdio.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j <= high-1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i+1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pivot = partition(arr, low, high);

        quickSort(arr, low, pivot - 1);
        quickSort(arr, pivot + 1, high);
    }
}

int selection(int arr[], int size, int n) {
    quickSort(arr, 0, size-1);
    return arr[n-1];
}

int main() {
    int arr[] = {12, 11, 15, 10, 9, 1, 2, 3, 7, 8};
    int n = 4;
    int size = sizeof(arr) / sizeof(arr[0]);

    printf("The %dth smallest element is %d\n", n, selection(arr, size, n));
    return 0;
}

```

```
Randomized-Partition(A, low, high):
1. i = Random number between low and high (inclusive)
2. swap A[i] and A[high]
3. return Partition(A, low, high)

Randomized-QuickSort(A, low, high):
1. if low < high:
2.     pivot = Randomized-Partition(A, low, high)
3.     Randomized-QuickSort(A, low, pivot-1)
4.     Randomized-QuickSort(A, pivot+1, high)

Selection(A, n):
1. Randomized-QuickSort(A, 0, length(A)-1)
2. Return A[n-1]

```

```

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j <= high-1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i+1], &arr[high]);
    return (i + 1);
}

int randomized_partition(int arr[], int low, int high) {
    srand(time(NULL));
    int random = low + rand() % (high - low);
    swap(&arr[random], &arr[high]);
    return partition(arr, low, high);
}

void randomized_quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pivot = randomized_partition(arr, low, high);

        randomized_quickSort(arr, low, pivot - 1);
        randomized_quickSort(arr, pivot + 1, high);
    }
}

int selection(int arr[], int size, int n) {
    randomized_quickSort(arr, 0, size-1);
    return arr[n-1];
}

int main() {
    int arr[] = {12, 11, 15, 10, 9, 1, 2, 3, 7, 8};
    int n = 4;
    int size = sizeof(arr) / sizeof(arr[0]);

    printf("The %dth smallest element is %d\n", n, selection(arr, size, n));
    return 0;
}

```


```
Select(A, i):
1. If |A| = 1 then return the only element in A.
2. Divide A into subsets of 5 elements. Let's say there are 'm' such subsets.
3. For each subset of 5, find the median. Call this set of medians 'M'.
4. medOfMed = Select(M, ⌊m/2⌋) (Recursively find the median of M).
5. Partition A around medOfMed. Let k be the rank of medOfMed in the partitioned array.
6. If i = k, return medOfMed.
7. If i < k, recursively find the ith smallest element in the left sub-array.
8. If i > k, recursively find the (i-k)th smallest element in the right sub-array.

```

```
#include <stdio.h>

void swap(int* a, int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}

int partition(int arr[], int l, int r, int x) {
    int i;
    for (i = l; i < r; i++)
        if (arr[i] == x)
            break;
    swap(&arr[i], &arr[r]);
    i = l;
    for (int j = l; j <= r - 1; j++) {
        if (arr[j] <= x) {
            swap(&arr[i], &arr[j]);
            i++;
        }
    }
    swap(&arr[i], &arr[r]);
    return i;
}

int findMedian(int arr[], int n) {
    int key;
    for (int i = 1; i < n; i++) {
        key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
    return arr[n / 2];
}

int kthSmallest(int arr[], int l, int r, int k) {
    if (k > 0 && k <= r - l + 1) {
        int n = r - l + 1;
        int i, median[(n + 4) / 5];
        for (i = 0; i < n / 5; i++)
            median[i] = findMedian(arr + l + i * 5, 5);
        if (i * 5 < n) {
            median[i] = findMedian(arr + l + i * 5, n % 5);
            i++;
        }
        int medOfMed = (i == 1) ? median[i - 1] : kthSmallest(median, 0, i - 1, i / 2);
        int pos = partition(arr, l, r, medOfMed);
        if (pos - l == k - 1)
            return arr[pos];
        if (pos - l > k - 1)
            return kthSmallest(arr, l, pos - 1, k);
        return kthSmallest(arr, pos + 1, r, k - pos + l - 1);
    }
    return -1;
}

int main() {
    int arr[] = {12, 3, 5, 7, 4, 19, 26, 1, 2, 10};
    int n = sizeof(arr) / sizeof(arr[0]), k = 5;
    printf("The %dth smallest element is %d\n", k, kthSmallest(arr, 0, n - 1, k));
    return 0;
}

```