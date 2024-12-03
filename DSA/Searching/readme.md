## Linear Search

Linear search is a simple search algorithm that checks each element in the list sequentially until the target value is found or the list ends.

```cpp
#include <iostream>
#include <vector>

int linearSearch(const std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i; // Target found
        }
    }
    return -1; // Target not found
}

int main() {
    std::vector<int> arr = {1, 3, 5, 7, 9, 11};
    int target = 7;
    int result = linearSearch(arr, target);
    if (result != -1) {
        std::cout << "Element found at index " << result << std::endl;
    } else {
        std::cout << "Element not found" << std::endl;
    }
    return 0;
}
```

## Binary Search

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing the search interval in half.

```cpp
#include <iostream>
#include <vector>

int binarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid; // Target found
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1; // Target not found
}
```

## One-Sided Binary Search

One-sided binary search is a variation of binary search where the search space is reduced to one side based on a condition.

```cpp
#include <iostream>
#include <vector>

int oneSidedBinarySearch(const std::vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    if (left < arr.size() && arr[left] == target) {
        return left; // Target found
    }
    return -1; // Target not found
}
```