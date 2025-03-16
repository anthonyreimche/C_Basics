# C Arrays

## Array Declaration
```c
int numbers[5];                     // Declare array of 5 integers
int values[5] = {1, 2, 3, 4, 5};   // Declare and initialize
int partial[5] = {1, 2};           // Remaining elements are 0
int sized[] = {1, 2, 3};           // Size determined by initializer
char str[] = "hello";              // Character array with null terminator
```

## Array Access
```c
int arr[3] = {10, 20, 30};
printf("%d", arr[0]);    // First element (10)
printf("%d", arr[1]);    // Second element (20)
printf("%d", arr[2]);    // Third element (30)

// Modifying elements
arr[1] = 25;             // Second element is now 25
```

## Array and Pointers
```c
int arr[5] = {10, 20, 30, 40, 50};

// Array name gives address of first element
printf("%p", arr);       // Same as &arr[0]

// Access using pointer notation
printf("%d", *arr);      // First element (10)
printf("%d", *(arr+1));  // Second element (20)
printf("%d", *(arr+2));  // Third element (30)

// Array name cannot be reassigned
// arr = arr + 1;        // ERROR: not assignable
```

## Multidimensional Arrays
```c
// 2D array (3 rows, 4 columns)
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};

// Access elements
printf("%d", matrix[1][2]);  // Row 1, Column 2 (7)

// 3D array
int cube[2][3][4];           // 2 planes, 3 rows, 4 columns
```

## Array Size
```c
int arr[5] = {1, 2, 3, 4, 5};

// Number of elements in array
int size = sizeof(arr) / sizeof(arr[0]);  // 5

// Total bytes in array
int bytes = sizeof(arr);  // 20 (5 * 4 bytes)
```

## Arrays in Functions
```c
// Arrays are passed by reference (pointer)
void processArray(int arr[], int size) {
    // Changes affect original array
    for(int i = 0; i < size; i++) {
        arr[i] *= 2;
    }
    
    // Size must be passed separately
    // sizeof(arr) here would give pointer size, not array size
}

// Call with array
int numbers[5] = {1, 2, 3, 4, 5};
processArray(numbers, 5);
```

## Common Array Operations
```c
// Iterating through array
int sum = 0;
int nums[5] = {10, 20, 30, 40, 50};
for(int i = 0; i < 5; i++) {
    sum += nums[i];
}

// Copying arrays
int source[5] = {1, 2, 3, 4, 5};
int dest[5];
for(int i = 0; i < 5; i++) {
    dest[i] = source[i];
}
// Or use memcpy:
// memcpy(dest, source, sizeof(source));
```
