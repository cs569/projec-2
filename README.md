#include <iostream>
#include <vector>
#include <chrono> // For measuring time

using namespace std;

// Function for Simple Sort
void simpleSort(vector<int>& arr, int& comparisons, int& swaps) {
    comparisons = swaps = 0; // Initialize counts
    for (size_t i = 0; i < arr.size() - 1; ++i) {
        for (size_t j = i + 1; j < arr.size(); ++j) {
            comparisons++;
            if (arr[i] > arr[j]) {
                swap(arr[i], arr[j]);
                swaps++;
            }
        }
    }
}

// Function for Bubble Sort
void bubbleSort(vector<int>& arr, int& comparisons, int& swaps) {
    comparisons = swaps = 0; // Initialize counts
    bool swapped;
    for (size_t i = 0; i < arr.size() - 1; ++i) {
        swapped = false;
        for (size_t j = 0; j < arr.size() - i - 1; ++j) {
            comparisons++;
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swaps++;
                swapped = true;
            }
        }
        if (!swapped) break; // Stop if the array is already sorted
    }
}

// Function for Insertion Sort
void insertionSort(vector<int>& arr, int& comparisons, int& swaps) {
    comparisons = swaps = 0; // Initialize counts
    for (size_t i = 1; i < arr.size(); ++i) {
        int key = arr[i];
        size_t j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            comparisons++;
            arr[j + 1] = arr[j];
            j--;
            swaps++; // Count shift as a swap
        }
        arr[j + 1] = key;
        if (j >= 0) comparisons++; // Last comparison in while
    }
}

// Function for Selection Sort
void selectionSort(vector<int>& arr, int& comparisons, int& swaps) {
    comparisons = swaps = 0; // Initialize counts
    for (size_t i = 0; i < arr.size() - 1; ++i) {
        size_t minIndex = i;
        for (size_t j = i + 1; j < arr.size(); ++j) {
            comparisons++;
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        if (minIndex != i) {
            swap(arr[i], arr[minIndex]);
            swaps++;
        }
    }
}

// Function to display the array
void displayArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

// Main function
int main() {
    int n;
    cout << "Enter the number of elements: ";
    cin >> n;

    vector<int> data(n);
    cout << "Enter " << n << " integers: ";
    for (int i = 0; i < n; ++i) {
        cin >> data[i];
    }

    // Copy of the original data for each sorting algorithm
    vector<int> arr;

    // Sort using Simple Sort
    arr = data;
    int simpleComparisons, simpleSwaps;
    simpleSort(arr, simpleComparisons, simpleSwaps);
    cout << "Simple Sort: ";
    displayArray(arr);
    cout << "Comparisons: " << simpleComparisons << ", Swaps: " << simpleSwaps << endl;

    // Sort using Bubble Sort
    arr = data;
    int bubbleComparisons, bubbleSwaps;
    bubbleSort(arr, bubbleComparisons, bubbleSwaps);
    cout << "Bubble Sort: ";
    displayArray(arr);
    cout << "Comparisons: " << bubbleComparisons << ", Swaps: " << bubbleSwaps << endl;

    // Sort using Insertion Sort
    arr = data;
    int insertionComparisons, insertionSwaps;
    insertionSort(arr, insertionComparisons, insertionSwaps);
    cout << "Insertion Sort: ";
    displayArray(arr);
    cout << "Comparisons: " << insertionComparisons << ", Swaps: " << insertionSwaps << endl;

    // Sort using Selection Sort
    arr = data;
    int selectionComparisons, selectionSwaps;
    selectionSort(arr, selectionComparisons, selectionSwaps);
    cout << "Selection Sort: ";
    displayArray(arr);
    cout << "Comparisons: " << selectionComparisons << ", Swaps: " << selectionSwaps << endl;

    // Determine the most efficient algorithm
    int minComparisons =({simpleComparisons, bubbleComparisons, insertionComparisons, selectionComparisons;});
    int minSwaps =({simpleSwaps, bubbleSwaps, insertionSwaps, selectionSwaps;});

    cout << "\nMost efficient algorithm based on comparisons: ";
    if (minComparisons == simpleComparisons) cout << "Simple Sort" << endl;
    else if (minComparisons == bubbleComparisons) cout << "Bubble Sort" << endl;
    else if (minComparisons == insertionComparisons) cout << "Insertion Sort" << endl;
    else cout << "Selection Sort" << endl;

    cout << "Most efficient algorithm based on swaps: ";
    if (minSwaps == simpleSwaps) cout << "Simple Sort" << endl;
    else if (minSwaps == bubbleSwaps) cout << "Bubble Sort" << endl;
    else if (minSwaps == insertionSwaps) cout << "Insertion Sort" << endl;
    else cout << "Selection Sort" << endl;

    return 0;
}
