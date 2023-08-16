Divide and Conquer Algorithms



## Randomized Quick Sort

```
#include <stdio.h>
#include <stdlib.h> // Required for rand() and srand()
#include <time.h>   // Required for time()

// `rand()` function isn't very good for generating random numbers because of its 
// linear congruential generator
// https://stackoverflow.com/questions/67665466/unable-to-understand-the-code-for-linear-congruential-generator

int getRandomIndex(int low, int high) {
    return (rand() % (high - low + 1)) + low;
}

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void randomizedQuickSort(int arr[], int low, int high) {
    if(low < high) {
        int randomIndex = getRandomIndex(low,high);
        swap(&arr[randomIndex], &arr[high]);
        int pi = partition(arr, low, high);
        randomizedQuickSort(arr, low, pi - 1);
        randomizedQuickSort(arr, pi + 1, high);
    }
}

int main() {
    srand(time(NULL)); // Seed the random number generator

    int arr[] = {5,1,3,6,10,13};
    int size = sizeof(arr) / sizeof(arr[0]);
    randomizedQuickSort(arr, 0, size-1);

    printf("Sorted array: \n");
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);

    return 0;
}

```