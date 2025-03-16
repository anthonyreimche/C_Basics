# C Conditionals

## If Statement
```c
if (condition) {
    // Code executed if condition is true
}
```

## If-Else Statement
```c
if (condition) {
    // Code executed if condition is true
} else {
    // Code executed if condition is false
}
```

## If-Else If-Else Chain
```c
if (condition1) {
    // Code executed if condition1 is true
} else if (condition2) {
    // Code executed if condition1 is false and condition2 is true
} else {
    // Code executed if all conditions are false
}
```

## Ternary Operator
```c
// condition ? value_if_true : value_if_false
int max = (a > b) ? a : b;  // Assigns larger of a and b to max
```

## Switch Statement
```c
switch (expression) {
    case value1:
        // Code for value1
        break;
    case value2:
        // Code for value2
        break;
    default:
        // Code if no case matches
}
```

## Comparison Operators
```c
a == b    // Equal to
a != b    // Not equal to
a < b     // Less than
a > b     // Greater than
a <= b    // Less than or equal to
a >= b    // Greater than or equal to
```

## Logical Operators
```c
a && b    // Logical AND (true if both a and b are true)
a || b    // Logical OR (true if either a or b is true)
!a        // Logical NOT (true if a is false)
```

## Short-Circuit Evaluation
```c
// In a && b, if a is false, b is not evaluated
if (ptr != NULL && ptr->value > 0) {
    // Safe because ptr is checked before accessing ptr->value
}

// In a || b, if a is true, b is not evaluated
if (isValid() || tryToMakeValid()) {
    // tryToMakeValid() only called if isValid() returns false
}
```

## Common Patterns
```c
// Guard clause
if (error_condition) {
    // Handle error
    return error_code;
}
// Continue with normal execution

// Null check
if (ptr == NULL) {
    // Handle null pointer
    return;
}

// Range check
if (value < MIN || value > MAX) {
    // Handle out of range
}
```
