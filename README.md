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
