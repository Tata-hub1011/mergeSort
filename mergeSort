

#include <iostream>
#include <vector>
#include <future>
#include <algorithm>


void merge(int* arr, int l, int m, int r)
{
    int nl = m - l + 1;
    int nr = r - m;

    std::vector<int> left(nl);
    std::vector<int> right(nr);

    for (int i = 0; i < nl; i++)
        left[i] = arr[l + i];
    for (int j = 0; j < nr; j++)
        right[j] = arr[m + 1 + j];

    int i = 0, j = 0;
    int k = l;

    while (i < nl && j < nr) {
        if (left[i] <= right[j]) {
            arr[k] = left[i];
            i++;
        }
        else {
            arr[k] = right[j];
            j++;
        }
        k++;
    }

    while (i < nl) {
        arr[k] = left[i];
        i++;
        k++;
    }

    while (j < nr) {
        arr[k] = right[j];
        j++;
        k++;
    }
}



void mergeSort(int* arr, int l, int r) {
    if (l >= r) return;

    int m = l + (r - l) / 2;

    if (r - l < 1000) {
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
    }
    else {
       
        std::future<void> left_side = std::async(std::launch::async, [&]() {
            mergeSort(arr, l, m);
            });

        mergeSort(arr, m + 1, r);

        left_side.get();
    }

    merge(arr, l, m, r);
}

int main() {
    int size = 20;
    int arr[] = { 90, 45, 12, 8, 34, 1, 15, 2, 7, 55, 4, 3, 66, 88, 11, 22, 33, 44, 77, 10 };

    mergeSort(arr, 0, size - 1);

    for (int i = 0; i < size; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}


