# C Enums

## Basic Enum Declaration
```c
// Define an enumeration type
enum Days {
    MONDAY,    // 0 (default)
    TUESDAY,   // 1
    WEDNESDAY, // 2
    THURSDAY,  // 3
    FRIDAY,    // 4
    SATURDAY,  // 5
    SUNDAY     // 6
};

// Declare a variable of enum type
enum Days today = WEDNESDAY;

// Use in conditions
if (today == FRIDAY) {
    printf("It's Friday!\n");
}
```

## Custom Values
```c
enum Months {
    JAN = 1,  // Start at 1 instead of 0
    FEB,      // 2 (auto-incremented)
    MAR,      // 3
    APR,      // 4
    MAY = 10, // Explicitly set to 10
    JUN,      // 11 (continues from 10)
    JUL       // 12
};

enum Status {
    ERROR = -1,
    SUCCESS = 0,
    PENDING = 5,
    RUNNING = 10
};
```

## Typedef with Enum
```c
// Create a named enum type
typedef enum {
    RED,
    GREEN,
    BLUE
} Color;

// Now use without 'enum' keyword
Color backgroundColor = BLUE;
```

## Enum as Flags (Bitmasks)
```c
// Powers of 2 for bitwise operations
enum FilePermissions {
    READ    = 1 << 0,  // 1 (binary: 001)
    WRITE   = 1 << 1,  // 2 (binary: 010)
    EXECUTE = 1 << 2   // 4 (binary: 100)
};

// Combine flags with bitwise OR
int userPermissions = READ | WRITE;  // 3 (binary: 011)

// Check flags with bitwise AND
if (userPermissions & EXECUTE) {
    printf("Has execute permission\n");
} else {
    printf("No execute permission\n");
}
```

## Enum Size and Type
```c
// Enums are typically stored as integers
printf("Size of enum: %zu bytes\n", sizeof(enum Days));  // Usually 4 bytes

// Specify underlying type (C99)
enum Numbers : unsigned char {
    ONE = 1,
    TWO,
    THREE
};  // Uses only 1 byte
```

## Iterating Through Enums
```c
// Iterate through all days
for (enum Days day = MONDAY; day <= SUNDAY; day++) {
    // Process each day
    printf("Day %d\n", day);
}

// Using array of strings with enum
const char* dayNames[] = {
    "Monday", "Tuesday", "Wednesday", "Thursday",
    "Friday", "Saturday", "Sunday"
};

// Print day name
enum Days today = THURSDAY;
printf("Today is %s\n", dayNames[today]);  // "Today is Thursday"
```

## Enum in Switch Statements
```c
enum TrafficLight {
    RED_LIGHT,
    YELLOW_LIGHT,
    GREEN_LIGHT
};

enum TrafficLight light = YELLOW_LIGHT;

switch (light) {
    case RED_LIGHT:
        printf("Stop!\n");
        break;
    case YELLOW_LIGHT:
        printf("Caution!\n");
        break;
    case GREEN_LIGHT:
        printf("Go!\n");
        break;
}
```

## Forward Declaration
```c
// Declare enum before defining
enum Directions;  // Forward declaration

// Use in function prototype
void setDirection(enum Directions dir);

// Define later
enum Directions {
    NORTH,
    SOUTH,
    EAST,
    WEST
};
```
