# VSD MINI INTERNSHIP
## Introduction to Risc
### The VSDSquadron Mini is a tiny RISC-V development board. It features a 32-bit RISC-V core, multiple clock options, 15 GPIO pins, and various communication ports like SPI and I2C.

## Features
##### Processor: 32-bit RISC-V core (RV32EC instruction set)
##### Clock: Built-in 24MHz RC oscillator (x2 options), external oscillator slot
##### Memory: 2KB SRAM, 16KB Flash.
##### I/O: 15 GPIO pins
##### Communication Interface: USART, I2C, SPI
##### Watch timer and Real clock timer
## Steps involved
### 1.Installation of Virtual Box
![Screenshot (394)](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/5f62ae3a-d472-4338-b7da-0dea937f1d09)
### 2.Installation of Ubuntu software

![Screenshot (395)](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/6b62b95e-23e4-4016-9d23-6e636b363199)
### 3.Compute the C code to execute the sum of 1 to N number:

![Screenshot (396)](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/9e1841dc-7a43-4cd8-8448-07b771f85e31)

### 4.Output of the code


![Screenshot 2024-06-28 230805](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/dc675bdc-5dd3-4cad-afbc-f7bb48519bcc)
### 5.Conversion of C code into RISC intruction Set
###### Using the command riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c


![Screenshot (397)](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/89096eeb-2e14-4467-8b5e-07b8e5aecce3)
### 6.Calculation of Risc -v 


![Screenshot (398)](https://github.com/Saidharshinee/vsdminiintern/assets/170953134/14f5c5f1-b038-4209-a3b9-6cbf2800df40)



## Task 2
### SMART ELEVATOR CONTROLLER
### 1. C code for Elevator
#### Creating the file using the command leafpad elevator.c &
#### 
#include <stdio.h>
#include <stdbool.h>
#define NUM_FLOORS 10
#define NUM_ELEVATORS 1

// Elevator states
typedef enum {
    IDLE,
    MOVING_UP,
    MOVING_DOWN,
    DOOR_OPEN,
    DOOR_CLOSED
} ElevatorState;

// Elevator struct
typedef struct {
    int currentFloor;
    ElevatorState state;
} Elevator;

// Function prototypes
void initializeElevator(Elevator *elevator);
void moveElevator(Elevator *elevator, int targetFloor);
void openDoor(Elevator *elevator);
void closeDoor(Elevator *elevator);

int main() {
    Elevator elevators[NUM_ELEVATORS];
    int targetFloor;

    // Initialize elevator(s)
    for (int i = 0; i < NUM_ELEVATORS; i++) {
        initializeElevator(&elevators[i]);
    }

    // Example scenario: Request to go to floor 5
    targetFloor = 5;

    // Assuming there's only one elevator in this example
    moveElevator(&elevators[0], targetFloor);

    return 0;
}

void initializeElevator(Elevator *elevator) {
    elevator->currentFloor = 1;  // Start at floor 1
    elevator->state = IDLE;
}

void moveElevator(Elevator *elevator, int targetFloor) {
    if (elevator->currentFloor < targetFloor) {
        elevator->state = MOVING_UP;
        printf("Elevator moving up...\n");
        while (elevator->currentFloor < targetFloor) {
            elevator->currentFloor++;
            // Simulating movement delay
            printf("Floor %d\n", elevator->currentFloor);
        }
    } else if (elevator->currentFloor > targetFloor) {
        elevator->state = MOVING_DOWN;
        printf("Elevator moving down...\n");
        while (elevator->currentFloor > targetFloor) {
            elevator->currentFloor--;
            // Simulating movement delay
            printf("Floor %d\n", elevator->currentFloor);
        }
    }

    // Arrived at target floor
    elevator->state = DOOR_OPEN;
    openDoor(elevator);
    closeDoor(elevator);
}

void openDoor(Elevator *elevator) {
    elevator->state = DOOR_OPEN;
    printf("Elevator door opening...\n");
    // Simulating door opening delay
    printf("Door opened.\n");
}

void closeDoor(Elevator *elevator) {
    elevator->state = DOOR_CLOSED;
    // Simulating door closing delay
    printf("Elevator door closing...\n");
    printf("Door closed.\n");
}

![Screenshot (400)](https://github.com/user-attachments/assets/86f23431-68ed-48ef-873e-8a528c1ae1d3)
![Screenshot (401)](https://github.com/user-attachments/assets/f6d51de7-ffdd-44cb-8a4b-b11e6b98c769)
![Screenshot (402)](https://github.com/user-attachments/assets/dd7fe80d-62cc-4852-b1ce-cb225387f6b1)

![Screenshot (403)](https://github.com/user-attachments/assets/3485b59e-6dbd-46ed-aa83-d6750babb415)

#### OVERVIEW
### The Smart Elevator Controller project leverages ultrasonic sensing technology, the CH32V003 RISC-V processor, a servo motor, a touch sensor, and an LED display to create an automated and user-friendly elevator control system. This system operates by detecting the presence and position of individuals within the elevator using an ultrasonic sensor, which sends signals to the CH32V003 RISC-V processor. Upon receiving these signals, the processor activates a servo motor to move the elevator to the appropriate floor, uses touch sensors to determine the current floor, and displays the floor number using LEDs. This setup ensures seamless, efficient, and safe operation of the elevator, enhancing user convenience and safety by eliminating the need for manual control.
### COMPONENTS REQUIRED
## 
CH32V003X

Ultrasonic Sensor (HC-SR04)

Servo Motor (e.g., MG90S)

Touch Sensor

LED Lights

Resistors (appropriate values for LEDs)

Breadboard

Jumper Wires
### PIN DIAGRAM
![Screenshot (404)](https://github.com/user-attachments/assets/9ac34524-881d-40bd-bc4a-2af0e43834de)
### CODE

' ' ' #include <stdio.h>
#include <stdint.h>
#include "CH32V003.h" // Include the appropriate header file for the CH32V003 processor
#include "lcd.h"      // Include your LCD library header
#include "delay.h"    // Include a delay library for timing

// Pin definitions
#define TRIG_PIN    PC0
#define ECHO_PIN    PC1
#define SERVO_PIN   PD1
#define TOUCH_PIN   PD2
#define LED1_PIN    PC2
#define LED2_PIN    PC3

void GPIO_Init() {
    // Initialize GPIO pins for output/input
    // Setup TRIG_PIN, SERVO_PIN, LED1_PIN, LED2_PIN as outputs
    // Setup ECHO_PIN, TOUCH_PIN as inputs
    // You need to write specific code to initialize the GPIO pins as per your hardware setup
}

void Ultrasonic_Init() {
    // Initialize the ultrasonic sensor
    GPIO_Init();
}

uint32_t Ultrasonic_Read() {
    uint32_t duration, distance;

    // Trigger the ultrasonic sensor
    GPIO_WriteBit(TRIG_PIN, Bit_SET);
    delay_us(10); // 10 microseconds pulse
    GPIO_WriteBit(TRIG_PIN, Bit_RESET);

    // Measure the echo time
    while (GPIO_ReadInputDataBit(ECHO_PIN) == Bit_RESET); // Wait for the echo to start
    duration = 0;
    while (GPIO_ReadInputDataBit(ECHO_PIN) == Bit_SET) {
        duration++;
        delay_us(1);
    }

    // Calculate the distance in centimeters
    distance = (duration / 2) / 29.1;

    return distance;
}

void Servo_Init() {
    // Initialize the servo motor
    GPIO_Init();
}

void Servo_SetAngle(uint8_t angle) {
    // Set the servo motor to a specific angle
    // Convert angle to pulse width
    uint16_t pulse_width = 1000 + ((angle * 1000) / 180); // 1ms to 2ms pulse width for 0 to 180 degrees
    GPIO_WriteBit(SERVO_PIN, Bit_SET);
    delay_us(pulse_width);
    GPIO_WriteBit(SERVO_PIN, Bit_RESET);
    delay_us(20000 - pulse_width); // 20ms period - pulse width
}

void LED_DisplayFloor(uint8_t floor) {
    // Display the current floor using LEDs
    GPIO_WriteBit(LED1_PIN, (floor == 0) ? Bit_SET : Bit_RESET);
    GPIO_WriteBit(LED2_PIN, (floor == 1) ? Bit_SET : Bit_RESET);
}

uint8_t TouchSensor_Read() {
    // Read the current floor from the touch sensor
    if (GPIO_ReadInputDataBit(TOUCH_PIN) == Bit_SET) {
        return 1; // Assuming touch sensor indicates the first floor
    }
    return 0; // Assuming no touch indicates the ground floor
}

int main(void) {
    uint32_t distance;
    uint8_t current_floor = 0;

    // Initialize all components
    Ultrasonic_Init();
    Servo_Init();
    GPIO_Init();

    while (1) {
        // Read distance from the ultrasonic sensor
        distance = Ultrasonic_Read();

        // Determine the floor based on the distance
        if (distance < 10) {
            current_floor = TouchSensor_Read();
        }

        // Move the servo motor to the corresponding floor
        if (current_floor == 0) {
            Servo_SetAngle(0); // Move to ground floor
        } else if (current_floor == 1) {
            Servo_SetAngle(90); // Move to first floor
        }

        // Display the current floor using LEDs
        LED_DisplayFloor(current_floor);

        // Small delay before the next measurement
        delay_ms(500);
    }

    return 0;
}
' ' '
## TASK 7
