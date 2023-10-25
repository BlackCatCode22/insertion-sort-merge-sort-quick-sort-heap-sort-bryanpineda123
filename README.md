# tCppSorts02
insertion, merge, quick, heap

In Class Demo

25 Oct 23

1. Insertion Sort
Imagine you're playing cards. You're dealt cards one by one. As you receive each card, you insert it in its correct position among the ones you already have. That's what insertion sort does.

cpp
Copy code
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];  // Take one card (or number) at a time
        int j = i - 1;

        // Move elements of arr[0..i-1] that are greater than key
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;  // Place our card (number) in its correct position
    }
}

2. Merge Sort
Imagine you have two small piles of cards sorted in increasing order. If you want to combine them into one pile, you would compare the top cards of each pile, take the smaller one, and repeat until you've gone through both piles. Merge sort works by repeatedly splitting the deck in half until each half has one card, and then merging those halves back together.

cpp
Copy code
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    // Create temp arrays
    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    // Copy any remaining elements
    while (i < n1) {
        arr[k++] = L[i++];
    }
    while (j < n2) {
        arr[k++] = R[j++];
    }
}

void mergeSort(int arr[], int l, int r) {
    if (l >= r) return; 

    int m = l + (r - l) / 2;  // Find the middle of the array

    mergeSort(arr, l, m);   // Sort the left half
    mergeSort(arr, m + 1, r);  // Sort the right half

    merge(arr, l, m, r);   // Merge the sorted halves
}

3. Quick Sort
Quick sort works by picking an element from the array (called the "pivot") and putting all smaller elements before it, and all larger ones after it. It then does the same for the two halves and keeps doing this recursively.

cpp
Copy code
int partition(int arr[], int low, int high) {
    int pivot = arr[high]; 
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }
    std::swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

4. Heap Sort
Imagine you have a special tree where a parent always has a larger value than its children. This tree can be easily represented as an array. The idea is to build this tree (heapify) and repeatedly take the largest element (root of the tree) and replace it with the last element in the array.

cpp
Copy code
void heapify(int arr[], int n, int i) {
    int largest = i;  
    int l = 2 * i + 1;  
    int r = 2 * i + 2;  

    if (l < n && arr[l] > arr[largest])
        largest = l;

    if (r < n && arr[r] > arr[largest])
        largest = r;

    if (largest != i) {
        std::swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i > 0; i--) {
        std::swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}

