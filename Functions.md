# C Functions

## Basic Function
```c
// return_type function_name(parameter_list)
int add(int a, int b) {
    return a + b;  // Must return a value matching return type
}

// Call the function
int sum = add(5, 3);  // sum = 8
```

## Function Prototype
```c
// Declare function before use
int multiply(int a, int b);  // Prototype

int main() {
    int product = multiply(4, 5);  // Call function
    return 0;
}

// Define function later
int multiply(int a, int b) {
    return a * b;
}
```

## Return Values
```c
// Function must return value of declared type
double getAverage(int a, int b) {
    return (a + b) / 2.0;  // Returns double
}

// Multiple return statements possible
int getMax(int a, int b) {
    if (a > b) {
        return a;
    }
    return b;
}

// void means no return value needed
void printMessage(char* message) {
    printf("%s\n", message);
    // No return statement required
    // Can use "return;" to exit early if needed
}
```

## Parameter Passing
```c
// Pass by value (copy of data)
void increment(int x) {
    x++;  // Only modifies local copy
}

// Pass by reference (using pointers)
void incrementRef(int* x) {
    (*x)++;  // Modifies original value
}

int num = 10;
increment(num);     // num still 10
incrementRef(&num); // num becomes 11
```

## Array Parameters
```c
// Arrays are passed as pointers
void processArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2;  // Modifies original array
    }
}

// Equivalent declaration
void processArray(int* arr, int size) {
    // Same function, different syntax
}
```

## Function with Variable Arguments
```c
#include <stdarg.h>

// Ellipsis (...) for variable arguments
int sum(int count, ...) {
    va_list args;
    va_start(args, count);
    
    int total = 0;
    for (int i = 0; i < count; i++) {
        total += va_arg(args, int);
    }
    
    va_end(args);
    return total;
}

// Call with different number of arguments
sum(3, 10, 20, 30);  // 60
sum(5, 1, 2, 3, 4, 5);  // 15
```

## Inline Functions
```c
// Hint to compiler to substitute function code at call site
inline int max(int a, int b) {
    return (a > b) ? a : b;
}
```

## Function Pointers
```c
// Declare a function pointer
int (*operation)(int, int);

// Assign address of a function
operation = add;  // Points to add function

// Call function through pointer
int result = operation(5, 3);  // Same as add(5, 3)

// Function pointer as parameter
int applyOp(int (*op)(int, int), int a, int b) {
    return op(a, b);
}

// Call with function address
applyOp(add, 5, 3);  // 8
```

## Recursive Functions
```c
// Function that calls itself
int factorial(int n) {
    if (n <= 1) {
        return 1;  // Base case
    }
    return n * factorial(n - 1);  // Recursive case
}
```

## Static Functions
```c
// Function only visible in current file
static int privateFunction(int x) {
    return x * x;
}
