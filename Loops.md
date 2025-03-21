# C Loops

## For Loop
```c
// for (initialization; condition; update)
for (int i = 0; i < 10; i++) {
    printf("%d ", i);  // Prints 0 to 9
}
```

## While Loop
```c
// while (condition)
int i = 0;
while (i < 10) {
    printf("%d ", i);  // Prints 0 to 9
    i++;
}
```

## Do-While Loop
```c
// do { code } while (condition);
int i = 0;
do {
    printf("%d ", i);  // Prints 0 to 9
    i++;
} while (i < 10);
```

## Nested Loops
```c
// Loop inside another loop
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        printf("(%d,%d) ", i, j);
    }
    printf("\n");
}
```

## Loop Control
```c
// Break - exits the loop immediately
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break;  // Exit when i is 5
    }
    printf("%d ", i);  // Prints 0 to 4
}

// Continue - skips the rest of the current iteration
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue;  // Skip even numbers
    }
    printf("%d ", i);  // Prints odd numbers 1, 3, 5, 7, 9
}
```

## Infinite Loops
```c
// Intentional infinite loop
while (1) {
    // Code runs forever unless break is used
    if (exitCondition) {
        break;
    }
}

// Another form
for (;;) {
    // Code runs forever unless break is used
}
```

## Common Loop Patterns
```c
// Array iteration
int arr[5] = {10, 20, 30, 40, 50};
for (int i = 0; i < 5; i++) {
    printf("%d ", arr[i]);
}

// Countdown
for (int i = 10; i > 0; i--) {
    printf("%d ", i);  // 10 down to 1
}

// Processing strings
char str[] = "Hello";
for (int i = 0; str[i] != '\0'; i++) {
    printf("%c ", str[i]);
}
```

## Loop with Multiple Variables
```c
// Initialize and update multiple variables
for (int i = 0, j = 10; i < j; i++, j--) {
    printf("i=%d, j=%d\n", i, j);
}
```

## Recursion
```c
// Function that calls itself
int factorial(int n) {
    // Base case (stopping condition)
    if (n <= 1) {
        return 1;
    }
    // Recursive case
    return n * factorial(n - 1);
}

// Recursive function to calculate Fibonacci numbers
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## Tail Recursion
```c
// Optimized recursion that can be converted to iteration by compiler
int factorial_tail(int n, int result) {
    if (n <= 1) {
        return result;
    }
    return factorial_tail(n - 1, n * result);
}

// Call with: factorial_tail(5, 1);
```

## Goto Statement
```c
// Not recommended but can be used for complex control flow
int i = 0;
start:
    printf("%d ", i);
    i++;
    if (i < 10) {
        goto start;  // Jump back to start label
    }
```
