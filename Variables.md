# C Variables

## Basic Declaration
```c
int number = 10;        // Declare and initialize
int count;              // Declare only
count = 5;              // Assign later
```

## Common Data Types
| Type | Use | Example | Format |
|------|-----|---------|--------|
| `int` | Whole numbers | `int age = 25;` | `%d` |
| `float` | Decimal numbers | `float price = 9.99f;` | `%f` |
| `double` | Precise decimals | `double pi = 3.14159;` | `%lf` |
| `char` | Single character | `char grade = 'A';` | `%c` |
| `bool` | True/false (C99) | `bool done = true;` | `%d` |

## Type Modifiers
```c
unsigned int positive = 10;    // Only positive values
long int bigNumber = 123456L;  // Larger range
```

## Constants
```c
const int MAX = 100;           // Cannot be changed
#define PI 3.14159             // Preprocessor constant
```

## Variable Naming
- Start with letter or underscore
- Use letters, numbers, underscores
- Case-sensitive (`count` ≠ `Count`)

## Multiple Variables
```c
int x = 5, y = 10, z = 15;     // Same type
```

## Type Conversion
```c
float f = 10.5;
int i = (int)f;                // Explicit cast: 10
```

---
