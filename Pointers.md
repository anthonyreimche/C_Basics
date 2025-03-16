# C Pointers

## Pointers Basics
```c
int num = 10;
int *ptr = &num;        // Declare pointer to int, store address of num

*ptr = 20;              // Modify value (num is now 20)
printf("%d", *ptr);     // Access value through pointer
printf("%p", ptr);      // Print address stored in pointer
```

## Pointer Arithmetic
```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;           // Points to first element

printf("%d", *p);       // 10 (first element)
printf("%d", *(p+1));   // 20 (second element)
printf("%d", *(p+2));   // 30 (third element)
p++;                    // Move to next element
```

## Pointers and Arrays
```c
// Array names decay to pointers in most contexts
int arr[5] = {10, 20, 30, 40, 50};
int *ptr = arr;  // ptr points to first element of arr

// Key differences:
sizeof(arr);     // Returns size of entire array (5 * sizeof(int))
sizeof(ptr);     // Returns size of pointer only (4 or 8 bytes)

// Cannot reassign array name
// arr = ptr;    // ERROR: arr is not modifiable
ptr = arr + 1;   // Valid: ptr now points to second element

// These are equivalent ways to access elements:
arr[2];          // Using array notation
*(arr + 2);      // Using pointer arithmetic
ptr[2];          // Pointers can use array notation
*(ptr + 2);      // Using pointer arithmetic with pointer
```

## Function Parameters
```c
// When arrays are passed to functions, they decay to pointers
void processArray(int *arr, int size) {
    // arr is a pointer, not a true array
    printf("%zu", sizeof(arr));  // Size of pointer, not array
    
    for(int i = 0; i < size; i++) {
        arr[i] *= 2;     // Modify original array elements
    }
}

// These declarations are equivalent
void func1(int arr[]);   // Array syntax
void func2(int *arr);    // Pointer syntax
```

## Common Pointer Mistakes
```c
int *ptr;              // Uninitialized pointer (dangerous)
*ptr = 10;             // ERROR: Dereferencing uninitialized pointer

int *p = malloc(sizeof(int));
// ... use p ...
free(p);               // Free allocated memory
*p = 20;               // ERROR: Using after free
```

## Pointer to Pointer
```c
int num = 10;
int *ptr = &num;       // Pointer to int
int **pptr = &ptr;     // Pointer to pointer to int

printf("%d", **pptr);  // 10 (double dereference)
```

## Void Pointers
```c
void *vptr;            // Generic pointer type
int num = 10;
float f = 3.14;

vptr = &num;           // Can point to any data type
printf("%d", *(int*)vptr);  // Must cast before dereferencing

vptr = &f;
printf("%f", *(float*)vptr);
```
