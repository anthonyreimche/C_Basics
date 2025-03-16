# Getting Started with C Programming

## Where to Begin

## Understanding Program Structure

### The Basic Template
```c
// 1. Include necessary libraries
#include <stdio.h>
#include <stdlib.h>

// 2. Define constants and macros
#define MAX_SIZE 100

// 3. Declare global variables (use sparingly)
int globalCounter = 0;

// 4. Declare function prototypes
void greetUser(char* name);

// 5. Main function - program entry point
int main() {
    // Local variable declarations
    char userName[50];
    
    // Program logic
    printf("Enter your name: ");
    scanf("%s", userName);
    
    greetUser(userName);
    
    return 0;
}

// 6. Function implementations
void greetUser(char* name) {
    printf("Hello, %s!\n", name);
}
```

## Step-by-Step Development Process

### 1. Understand the Problem
```
Before writing any code, ask yourself:
- What is the program supposed to do?
- What inputs will it need?
- What outputs should it produce?
- What steps are required to transform inputs to outputs?
```

### 2. Plan Your Approach
```
Break down the problem into smaller tasks:
- What variables will you need?
- What calculations must be performed?
- What user interactions are required?
- What functions would make the code clearer?
```

### 3. Write a Simple Version First
```c
// Example: Program to calculate average of numbers
#include <stdio.h>

int main() {
    int count, i;
    float sum = 0, number, average;
    
    // Get count of numbers
    printf("How many numbers? ");
    scanf("%d", &count);
    
    // Get numbers and calculate sum
    for(i = 0; i < count; i++) {
        printf("Enter number %d: ", i+1);
        scanf("%f", &number);
        sum += number;
    }
    
    // Calculate and display average
    average = sum / count;
    printf("Average: %.2f\n", average);
    
    return 0;
}
```

### 4. Test and Debug
```
- Test with normal inputs
- Test with edge cases (very large/small values)
- Test with invalid inputs
- Fix any issues you find
```

### 5. Refine and Improve
```c
// Improved version with functions and error handling
#include <stdio.h>

float getAverage(float numbers[], int count);

int main() {
    int count, i;
    float numbers[100], average;
    
    // Get count with validation
    do {
        printf("How many numbers (1-100)? ");
        scanf("%d", &count);
    } while(count < 1 || count > 100);
    
    // Get numbers
    for(i = 0; i < count; i++) {
        printf("Enter number %d: ", i+1);
        scanf("%f", &numbers[i]);
    }
    
    // Calculate and display average
    average = getAverage(numbers, count);
    printf("Average: %.2f\n", average);
    
    return 0;
}

float getAverage(float numbers[], int count) {
    float sum = 0;
    int i;
    
    for(i = 0; i < count; i++) {
        sum += numbers[i];
    }
    
    return sum / count;
}
```

## Common Beginner Mistakes and How to Avoid Them

### 1. Forgetting Semicolons
```c
// Wrong
printf("Hello")
int x = 5

// Correct
printf("Hello");
int x = 5;
```

### 2. Confusing = and ==
```c
// Wrong (assigns 5 to x, always true)
if (x = 5) {
    printf("x is 5\n");
}

// Correct (checks if x equals 5)
if (x == 5) {
    printf("x is 5\n");
}
```

### 3. Array Indexing
```c
// Wrong (accesses beyond array bounds)
int numbers[5];
numbers[5] = 10;  // Error! Valid indices are 0-4

// Correct
int numbers[5];
numbers[4] = 10;  // Last element
```

### 4. Not Initializing Variables
```c
// Wrong
int sum;
sum += 10;  // sum has undefined value

// Correct
int sum = 0;
sum += 10;  // sum is now 10
```

### 5. Forgetting to Include Libraries
```c
// Wrong
int main() {
    printf("Hello\n");  // Error if stdio.h not included
    return 0;
}

// Correct
#include <stdio.h>

int main() {
    printf("Hello\n");
    return 0;
}
```

## Building Your Complete Program

### Example: Temperature Converter
```c
/*
 * Temperature Converter
 * Converts between Celsius and Fahrenheit
 */
#include <stdio.h>

// Function prototypes
float celsiusToFahrenheit(float celsius);
float fahrenheitToCelsius(float fahrenheit);
void displayMenu();
int getMenuChoice();

int main() {
    int choice;
    float temperature, result;
    
    do {
        // Display menu and get user choice
        displayMenu();
        choice = getMenuChoice();
        
        // Process based on choice
        switch(choice) {
            case 1:  // Celsius to Fahrenheit
                printf("Enter temperature in Celsius: ");
                scanf("%f", &temperature);
                result = celsiusToFahrenheit(temperature);
                printf("%.2f°C = %.2f°F\n\n", temperature, result);
                break;
                
            case 2:  // Fahrenheit to Celsius
                printf("Enter temperature in Fahrenheit: ");
                scanf("%f", &temperature);
                result = fahrenheitToCelsius(temperature);
                printf("%.2f°F = %.2f°C\n\n", temperature, result);
                break;
                
            case 3:  // Exit
                printf("Goodbye!\n");
                break;
                
            default:  // Invalid choice
                printf("Invalid choice. Please try again.\n\n");
        }
    } while(choice != 3);
    
    return 0;
}

// Convert Celsius to Fahrenheit
float celsiusToFahrenheit(float celsius) {
    return (celsius * 9/5) + 32;
}

// Convert Fahrenheit to Celsius
float fahrenheitToCelsius(float fahrenheit) {
    return (fahrenheit - 32) * 5/9;
}

// Display menu options
void displayMenu() {
    printf("Temperature Converter\n");
    printf("1. Celsius to Fahrenheit\n");
    printf("2. Fahrenheit to Celsius\n");
    printf("3. Exit\n");
    printf("Enter your choice (1-3): ");
}

// Get and validate menu choice
int getMenuChoice() {
    int choice;
    scanf("%d", &choice);
    return choice;
}
```


### Debugging Tips
```
1. Use printf statements to track variable values
2. Check for common errors first
3. Test small parts of your code separately
4. Use a debugger for complex issues
5. Take breaks - fresh eyes often spot problems quickly
```
