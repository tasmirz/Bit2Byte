![Heap.excalidraw](Heap.excalidraw.md)
The reader is asked to create a queue, where elements have priority.

Uprooting and numbering the nodes consecutively,
![Heap Array.excalidraw](Heap%20Array.excalidraw.md)
A pattern is observable:
$$node - \lceil{x/2} \rceil = parent node $$
$$ left = parent *2 - 1 $$
$$ right = parent *2 $$
This indicates that this structure can be put into a random accessible contiguous storage. By applying any rules on this structure, a new data structure may be formed.

## Types of Heaps

### 1. Max-Heap
In a max-heap, the value of each node is greater than or equal to the values of its children. The highest value is at the root.

### 2. Min-Heap
In a min-heap, the value of each node is less than or equal to the values of its children. The lowest value is at the root.

## Heap Operations

### 1. Insertion
To insert a new element into a heap, add the element at the end of the heap and then heapify up to maintain the heap property.

#### Max-Heap Insertion
```cpp
void insertMaxHeap(vector<int>& heap, int value) {
    heap.push_back(value);
    int i = heap.size() - 1;
    while (i != 0 && heap[(i - 1) / 2] < heap[i]) {
        swap(heap[i], heap[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}
```

#### Min-Heap Insertion
```cpp
void insertMinHeap(vector<int>& heap, int value) {
    heap.push_back(value);
    int i = heap.size() - 1;
    while (i != 0 && heap[(i - 1) / 2] > heap[i]) {
        swap(heap[i], heap[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}
```

### 2. Deletion
To delete the root element from a heap, replace it with the last element in the heap and then heapify down to maintain the heap property.

#### Max-Heap Deletion
```cpp
void deleteMaxHeap(vector<int>& heap) {
    if (heap.size() == 0) return;
    heap[0] = heap.back();
    heap.pop_back();
    int i = 0;
    while (2 * i + 1 < heap.size()) {
        int j = 2 * i + 1;
        if (j + 1 < heap.size() && heap[j] < heap[j + 1]) j++;
        if (heap[i] >= heap[j]) break;
        swap(heap[i], heap[j]);
        i = j;
    }
}
```

#### Min-Heap Deletion
```cpp
void deleteMinHeap(vector<int>& heap) {
    if (heap.size() == 0) return;
    heap[0] = heap.back();
    heap.pop_back();
    int i = 0;
    while (2 * i + 1 < heap.size()) {
        int j = 2 * i + 1;
        if (j + 1 < heap.size() && heap[j] > heap[j + 1]) j++;
        if (heap[i] <= heap[j]) break;
        swap(heap[i], heap[j]);
        i = j;
    }
}
```

### 3. Peek
To get the root element (maximum in max-heap or minimum in min-heap) without removing it.

#### Peek
```cpp
int peekHeap(const vector<int>& heap) {
    if (heap.size() == 0) throw out_of_range("Heap is empty");
    return heap[0];
}
```

### 4. Heapify
To convert an arbitrary array into a heap, start from the last non-leaf node and heapify down each node.

### 4. Heapify

#### Max-Heapify
```cpp
void maxHeapify(vector<int>& heap, int i) {
    int size = heap.size();
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < size && heap[left] > heap[largest]) largest = left;
    if (right < size && heap[right] > heap[largest]) largest = right;

    if (largest != i) {
        swap(heap[i], heap[largest]);
        maxHeapify(heap, largest);
    }
}

void buildMaxHeap(vector<int>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; i--) {
        maxHeapify(heap, i);
    }
}
```

#### Min-Heapify
```cpp
void minHeapify(vector<int>& heap, int i) {
    int size = heap.size();
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < size && heap[left] < heap[smallest]) smallest = left;
    if (right < size && heap[right] < heap[smallest]) smallest = right;

    if (smallest != i) {
        swap(heap[i], heap[smallest]);
        minHeapify(heap, smallest);
    }
}

void buildMinHeap(vector<int>& heap) {
    for (int i = heap.size() / 2 - 1; i >= 0; i--) {
        minHeapify(heap, i);
    }
}
```

### 5. Extract-Max/Min
To remove and return the root element from the heap, replace it with the last element and heapify down.

#### Extract-Max
```cpp
int extractMax(vector<int>& heap) {
    if (heap.size() == 0) throw out_of_range("Heap is empty");
    int maxVal = heap[0];
    heap[0] = heap.back();
    heap.pop_back();
    heapify(heap, 0, true);
    return maxVal;
}
```

#### Extract-Min
```cpp
int extractMin(vector<int>& heap) {
    if (heap.size() == 0) throw out_of_range("Heap is empty");
    int minVal = heap[0];
    heap[0] = heap.back();
    heap.pop_back();
    heapify(heap, 0, false);
    return minVal;
}
```

### 6. Increase/Decrease-Key
To increase or decrease the value of a node, adjust the value and then heapify up or down as necessary to maintain the heap property.

#### Increase-Key
```cpp
void increaseKey(vector<int>& heap, int i, int newValue) {
    if (newValue < heap[i]) throw invalid_argument("New value is smaller than current value");
    heap[i] = newValue;
    while (i != 0 && heap[(i - 1) / 2] < heap[i]) {
        swap(heap[i], heap[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}
```

#### Decrease-Key
```cpp
void decreaseKey(vector<int>& heap, int i, int newValue) {
    if (newValue > heap[i]) throw invalid_argument("New value is larger than current value");
    heap[i] = newValue;
    heapify(heap, i, false);
}
```