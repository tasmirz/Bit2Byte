# Arrays
An array is a collection of items stored at contiguous memory locations. The idea is to store multiple items of the same type together. This makes it easier to calculate the position of each element by simply adding an offset to a base value, i.e., the memory location of the first element of the array (generally denoted by the name of the array).

$$
    x_{i} =x_{0} + size * i
$$

## Declaration of Arrays

In C++, arrays are declared as follows:

```cpp
type arrayName[arraySize];
```

- `type`: This is the data type of the elements to be stored in the array.
- `arrayName`: This is the name of the array.
- `arraySize`: This is the number of elements in the array.

### Example

```cpp
int numbers[5]; // declares an array of 5 integers
```

## Initialization of Arrays

Arrays can be initialized at the time of declaration. The syntax is:

```cpp
type arrayName[arraySize] = {value1, value2, ..., valueN};
```

### Example

```cpp
int numbers[5] = {1, 2, 3, 4, 5}; // initializes an array of 5 integers
```

## Accessing Array Elements

Array elements are accessed using their index. The index of the first element is 0, the second element is 1, and so on.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    cout << "The first element is " << numbers[0] << endl;
    cout << "The third element is " << numbers[2] << endl;
    return 0;
}
```

## Looping Through Arrays

You can use loops to iterate through the elements of an array.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    for(int i = 0; i < 5; i++) {
        cout << "Element at index " << i << " is " << numbers[i] << endl;
    }
    return 0;
}
```

## Multidimensional Arrays

C++ allows multidimensional arrays. The simplest form of a multidimensional array is the two-dimensional array.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int matrix[2][3] = {
        {1, 2, 3},
        {4, 5, 6}
    };
    for(int i = 0; i < 2; i++) {
        for(int j = 0; j < 3; j++) {
            cout << "Element at matrix[" << i << "][" << j << "] is " << matrix[i][j] << endl;
        }
    }
    return 0;
}
```

## Insertion in Arrays

Insertion refers to adding an element at a specific position in an array. Since arrays have a fixed size, you may need to shift elements to make space for the new element.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[6] = {1, 2, 3, 4, 5};
    int position = 2; // position to insert the new element
    int value = 10; // value to be inserted

    for (int i = 5; i > position; i--) {
        numbers[i] = numbers[i - 1];
    }
    numbers[position] = value;

    for (int i = 0; i < 6; i++) {
        cout << numbers[i] << " ";
    }
    return 0;
}
```

## Deletion in Arrays

Deletion refers to removing an element from a specific position in an array. This requires shifting elements to fill the gap left by the removed element.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    int position = 2; // position to delete the element

    for (int i = position; i < 4; i++) {
        numbers[i] = numbers[i + 1];
    }

    for (int i = 0; i < 4; i++) {
        cout << numbers[i] << " ";
    }
    return 0;
}
```

## Searching in Arrays

Searching refers to finding the position of a specific element in an array. The simplest search algorithm is linear search.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    int value = 3; // value to be searched
    int position = -1;

    for (int i = 0; i < 5; i++) {
        if (numbers[i] == value) {
            position = i;
            break;
        }
    }

    if (position != -1) {
        cout << "Element found at index " << position << endl;
    } else {
        cout << "Element not found" << endl;
    }
    return 0;
}
```

## Merging Arrays

Merging refers to combining two arrays into a single array.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr1[3] = {1, 2, 3};
    int arr2[3] = {4, 5, 6};
    int merged[6];

    for (int i = 0; i < 3; i++) {
        merged[i] = arr1[i];
    }
    for (int i = 0; i < 3; i++) {
        merged[i + 3] = arr2[i];
    }

    for (int i = 0; i < 6; i++) {
        cout << merged[i] << " ";
    }
    return 0;
}
```
