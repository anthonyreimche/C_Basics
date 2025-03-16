# C Programming for Robotics & Electrical Engineering

## Program Structure Overview

### 1. File Organization
```
project_name/
  ├── include/             // Header files (.h)
  ├── src/                 // Source files (.c)
  ├── lib/                 // External libraries
  ├── build/               // Compiled objects
  └── Makefile             // Build instructions
```

### 2. Standard Program Layout
```c
/****** INCLUDES ******/
#include <stdio.h>      // Standard libraries first
#include <stdlib.h>
#include "myheader.h"   // Custom headers next

/****** CONSTANTS & MACROS ******/
#define MAX_SENSORS 8
#define MOTOR_TIMEOUT 1000
#define CONVERT_TO_RPM(x) ((x) * 60)

/****** GLOBAL VARIABLES ******/
int g_systemState = 0;
float g_sensorReadings[MAX_SENSORS];

/****** FUNCTION PROTOTYPES ******/
void initializeSystem(void);
int readSensor(int sensorId);
void setMotorSpeed(int motorId, int speed);
bool isSystemCalibrated(void);

/****** MAIN FUNCTION ******/
int main(void) {
    // Program execution starts here
    return 0;
}

/****** FUNCTION IMPLEMENTATIONS ******/
// All other functions defined here
```

## From Pseudocode to Implementation

### Step 1: Define the Problem
```
// PROBLEM STATEMENT:
// Create a function to control a DC motor based on sensor readings
// - Read analog sensor
// - Apply PID control algorithm
// - Set motor PWM output
```

### Step 2: Write Pseudocode
```
// PSEUDOCODE:
// Function: controlMotor
// Input: sensorId, targetValue, motorId
// Output: none (void)
//
// 1. Read current sensor value
// 2. Calculate error (target - current)
// 3. Apply PID algorithm to error
// 4. Limit output to valid range
// 5. Set motor speed to calculated value
// 6. Log operation
```

### Step 3: Create Function Prototype
```c
/**
 * Controls motor speed using PID based on sensor feedback
 * @param sensorId ID of the feedback sensor (0-7)
 * @param targetValue Desired sensor reading
 * @param motorId ID of the motor to control (0-3)
 * @return Success status (0 = success, negative = error code)
 */
int controlMotor(int sensorId, float targetValue, int motorId);
```

### Step 4: Implement the Function
```c
int controlMotor(int sensorId, float targetValue, int motorId) {
    // Validate inputs
    if (sensorId < 0 || sensorId >= MAX_SENSORS) {
        return -1;  // Invalid sensor ID
    }
    if (motorId < 0 || motorId > 3) {
        return -2;  // Invalid motor ID
    }
    
    // Read current value
    float currentValue = readSensor(sensorId);
    if (currentValue < 0) {
        return -3;  // Sensor reading failed
    }
    
    // Calculate error
    float error = targetValue - currentValue;
    
    // Apply PID algorithm (simplified)
    float output = applyPID(error, sensorId);
    
    // Limit output to valid range (-100 to 100 percent)
    if (output > 100.0f) output = 100.0f;
    if (output < -100.0f) output = -100.0f;
    
    // Set motor speed
    setMotorSpeed(motorId, (int)output);
    
    // Log operation
    logOperation("Motor control", motorId, output);
    
    return 0;  // Success
}
```

## Function Types for Robotics Applications

### 1. Initialization Functions
```c
/**
 * Initialize hardware components
 * - Called once at program start
 * - Sets up peripherals, calibrates sensors
 */
void initializeSystem(void) {
    // Initialize hardware
    initGPIO();
    initSensors();
    initMotors();
    
    // Perform calibration
    calibrateSensors();
    
    // Set initial state
    g_systemState = SYSTEM_READY;
}
```

### 2. Sensor Interface Functions
```c
/**
 * Read analog sensor value with noise filtering
 * @param sensorId Sensor to read (0-7)
 * @return Filtered sensor value or negative error code
 */
float readSensor(int sensorId) {
    // Validate input
    if (sensorId < 0 || sensorId >= MAX_SENSORS) {
        return -1.0f;
    }
    
    // Read multiple samples for filtering
    float sum = 0.0f;
    for (int i = 0; i < 10; i++) {
        sum += readAnalogInput(sensorId);
        delayMicroseconds(100);
    }
    
    // Return average (filtered) reading
    return sum / 10.0f;
}
```

### 3. Actuator Control Functions
```c
/**
 * Set motor speed with safety limits
 * @param motorId Motor to control (0-3)
 * @param speed Speed value (-100 to 100 percent)
 */
void setMotorSpeed(int motorId, int speed) {
    // Validate inputs
    if (motorId < 0 || motorId > 3) {
        logError("Invalid motor ID");
        return;
    }
    
    // Apply safety limits
    if (speed > 100) speed = 100;
    if (speed < -100) speed = -100;
    
    // Convert percentage to PWM value (0-255)
    int pwmValue;
    if (speed >= 0) {
        pwmValue = (speed * 255) / 100;
        setMotorDirection(motorId, FORWARD);
    } else {
        pwmValue = (-speed * 255) / 100;
        setMotorDirection(motorId, REVERSE);
    }
    
    // Set PWM output
    setPWMOutput(motorId, pwmValue);
}
```

### 4. Validator Functions
```c
/**
 * Check if system is properly calibrated
 * @return true if calibrated, false otherwise
 */
bool isSystemCalibrated(void) {
    // Check calibration flag
    if (!(g_systemState & SYSTEM_CALIBRATED)) {
        return false;
    }
    
    // Verify sensor readings are within expected ranges
    for (int i = 0; i < MAX_SENSORS; i++) {
        if (g_sensorReadings[i] < MIN_VALID_READING || 
            g_sensorReadings[i] > MAX_VALID_READING) {
            return false;
        }
    }
    
    return true;
}
```

### 5. Algorithm Functions
```c
/**
 * Apply PID control algorithm
 * @param error Current error value
 * @param channelId Control channel ID
 * @return Control output
 */
float applyPID(float error, int channelId) {
    static float lastError[MAX_CHANNELS] = {0};
    static float errorSum[MAX_CHANNELS] = {0};
    
    // PID constants
    const float Kp = 2.0f;   // Proportional gain
    const float Ki = 0.1f;   // Integral gain
    const float Kd = 0.5f;   // Derivative gain
    
    // Calculate PID terms
    float proportional = error * Kp;
    
    errorSum[channelId] += error;
    float integral = errorSum[channelId] * Ki;
    
    float derivative = (error - lastError[channelId]) * Kd;
    lastError[channelId] = error;
    
    // Combine terms
    float output = proportional + integral + derivative;
    
    return output;
}
```

### 6. State Machine Functions
```c
/**
 * Update system state based on current conditions
 * @return New state
 */
int updateSystemState(void) {
    switch (g_systemState) {
        case STATE_IDLE:
            if (isStartButtonPressed()) {
                return STATE_STARTING;
            }
            break;
            
        case STATE_STARTING:
            if (isSystemCalibrated()) {
                return STATE_RUNNING;
            } else if (isErrorDetected()) {
                return STATE_ERROR;
            }
            break;
            
        case STATE_RUNNING:
            if (isStopButtonPressed()) {
                return STATE_STOPPING;
            } else if (isErrorDetected()) {
                return STATE_ERROR;
            }
            break;
            
        // Additional states...
    }
    
    return g_systemState;  // No change
}
```

## Complete Program Example: Line Following Robot

```c
/****** INCLUDES ******/
#include <stdio.h>
#include <stdbool.h>
#include "robot_hardware.h"

/****** CONSTANTS & MACROS ******/
#define NUM_SENSORS 5
#define LEFT_MOTOR 0
#define RIGHT_MOTOR 1
#define BASE_SPEED 50
#define MAX_SPEED 80
#define MIN_SPEED 20

/****** GLOBAL VARIABLES ******/
int g_systemState = STATE_IDLE;
float g_lineSensorValues[NUM_SENSORS];
bool g_isCalibrated = false;

/****** FUNCTION PROTOTYPES ******/
void initializeRobot(void);
void calibrateSensors(void);
float readLineSensor(int sensorId);
void updateSensorReadings(void);
float calculateLinePosition(void);
void setMotorSpeeds(float linePosition);
void updateSystemState(void);
bool isSystemCalibrated(void);

/****** MAIN FUNCTION ******/
int main(void) {
    // Initialize robot hardware
    initializeRobot();
    
    // Main control loop
    while (1) {
        // Update system state
        updateSystemState();
        
        // Process based on current state
        switch (g_systemState) {
            case STATE_IDLE:
                // Do nothing, wait for start button
                break;
                
            case STATE_CALIBRATING:
                calibrateSensors();
                break;
                
            case STATE_RUNNING:
                // Read sensors
                updateSensorReadings();
                
                // Calculate line position (-1.0 to 1.0)
                float linePosition = calculateLinePosition();
                
                // Control motors based on line position
                setMotorSpeeds(linePosition);
                break;
                
            case STATE_ERROR:
                // Stop motors
                setMotorSpeed(LEFT_MOTOR, 0);
                setMotorSpeed(RIGHT_MOTOR, 0);
                
                // Flash error LED
                toggleErrorLED();
                delay(500);
                break;
        }
        
        // Small delay to prevent CPU hogging
        delay(10);
    }
    
    return 0;  // Never reached
}

/****** FUNCTION IMPLEMENTATIONS ******/

void initializeRobot(void) {
    // Initialize hardware components
    initGPIO();
    initSensors();
    initMotors();
    
    // Set initial state
    g_systemState = STATE_IDLE;
}

void calibrateSensors(void) {
    // Calibration code...
    g_isCalibrated = true;
    g_systemState = STATE_RUNNING;
}

float readLineSensor(int sensorId) {
    // Read and filter sensor value
    float sum = 0.0f;
    for (int i = 0; i < 5; i++) {
        sum += readAnalogInput(sensorId);
        delayMicroseconds(100);
    }
    return sum / 5.0f;
}

void updateSensorReadings(void) {
    for (int i = 0; i < NUM_SENSORS; i++) {
        g_lineSensorValues[i] = readLineSensor(i);
    }
}

float calculateLinePosition(void) {
    // Weighted average calculation
    float weightedSum = 0.0f;
    float sum = 0.0f;
    
    for (int i = 0; i < NUM_SENSORS; i++) {
        float position = (float)i / (NUM_SENSORS - 1) * 2.0f - 1.0f;
        weightedSum += position * g_lineSensorValues[i];
        sum += g_lineSensorValues[i];
    }
    
    if (sum > 0.0f) {
        return weightedSum / sum;
    } else {
        return 0.0f;  // No line detected
    }
}

void setMotorSpeeds(float linePosition) {
    // Proportional control for line following
    int leftSpeed = BASE_SPEED - (int)(linePosition * 30.0f);
    int rightSpeed = BASE_SPEED + (int)(linePosition * 30.0f);
    
    // Apply limits
    if (leftSpeed > MAX_SPEED) leftSpeed = MAX_SPEED;
    if (leftSpeed < MIN_SPEED) leftSpeed = MIN_SPEED;
    if (rightSpeed > MAX_SPEED) rightSpeed = MAX_SPEED;
    if (rightSpeed < MIN_SPEED) rightSpeed = MIN_SPEED;
    
    // Set motor speeds
    setMotorSpeed(LEFT_MOTOR, leftSpeed);
    setMotorSpeed(RIGHT_MOTOR, rightSpeed);
}

void updateSystemState(void) {
    switch (g_systemState) {
        case STATE_IDLE:
            if (isStartButtonPressed()) {
                g_systemState = STATE_CALIBRATING;
            }
            break;
            
        case STATE_RUNNING:
            if (isStopButtonPressed()) {
                g_systemState = STATE_IDLE;
                // Stop motors
                setMotorSpeed(LEFT_MOTOR, 0);
                setMotorSpeed(RIGHT_MOTOR, 0);
            } else if (isBatteryLow()) {
                g_systemState = STATE_ERROR;
            }
            break;
            
        // Other state transitions...
    }
}

bool isSystemCalibrated(void) {
    return g_isCalibrated;
}
```
