# Insertion Sort

## Intro

Suppose you are supposed to sort some sorts. Obviously you will go through all of 'em, right?

Well, while iterating, you will turn backwards to find the right place for each book, think in this way.&#x20;

## Code

```cpp
#include <iostream>

using namespace std;

void insertionSort(int* arr, int size) {
    for (int i = 1; i < size; i++) {
        int x = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > x) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = x;
    }
}

void print(int* arr, int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {5, 2, 4, 6, 1, 3};
    insertionSort(arr, sizeof(arr)/sizeof(arr[0]));
    print(arr, sizeof(arr)/sizeof(arr[0]));
}
```