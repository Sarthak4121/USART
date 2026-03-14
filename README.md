# Serial Communication using UART in Verilog

## Overview
This project implements a **UART (Universal Asynchronous Receiver/Transmitter)** communication system using **Verilog HDL**.  
The design demonstrates serial data transmission and reception without using a Finite State Machine (FSM).

Instead of FSM control, the implementation uses **shift registers, bit counters, and a baud rate prescaler** to handle serial communication timing and data framing.

The design was simulated using **EDA Playground** to verify correct transmission and reception of data.

---

## UART Frame Format

UART communication transmits data serially using the following frame structure:

```
Start Bit | Data Bits (8) | Stop Bit
    0     |   D0–D7       |    1
```

Each data byte is transmitted as **10 bits**.

---

## Features

- UART transmitter implemented in Verilog  
- UART receiver implemented in Verilog  
- Uses **shift registers and counters (no FSM)**  
- Supports **8-bit data transmission**  
- Start and stop bit framing  
- Baud rate control using **prescaler**  
- Simulation verified through waveform analysis  

---

## Project Structure

```
UART-Verilog
│
├── uart_tx_simple.v
├── uart_rx_simple.v
├── uart_top.v
├── uart_tb.v
├── waveform.png
└── README.md
```

---

## Module Description

### UART Transmitter (`uart_tx_simple`)
The transmitter module performs the following functions:

- Accepts 8-bit parallel input data  
- Adds start bit and stop bit to create a **10-bit frame**  
- Uses a **shift register** to send data serially  
- Uses a **bit counter** to track transmitted bits  
- `tx_busy` signal indicates active transmission  

---

### UART Receiver (`uart_rx_simple`)

The receiver performs the following operations:

- Detects **start bit (falling edge)**  
- Samples incoming bits using **baud rate timing**  
- Stores received bits in a shift register  
- Outputs received data on `rx_data`  
- `rx_valid` signal indicates valid received data  

---

### Top Module (`uart_top`)

The top module connects:

- UART Transmitter  
- UART Receiver  

The transmitter output `txd` is connected to the receiver input `rxd` for simulation and testing.

---

### Testbench (`uart_tb`)

The testbench is used to:

- Generate clock and reset signals  
- Provide input data for transmission  
- Observe transmitted and received signals  
- Verify correct UART communication  

---

## Simulation Results

Simulation confirms that:

- Data is transmitted with **correct start, data, and stop bits**  
- Receiver successfully reconstructs the original data  
- Control signals such as **tx_busy and rx_valid** behave correctly  

Example test data:

| Input Data | Serial Frame | Received Data |
|------------|-------------|---------------|
| 01010101 | 0-01010101-1 | 01010101 |
| 11110000 | 0-11110000-1 | 11110000 |
| 10101010 | 0-10101010-1 | 10101010 |

---

## Tools Used

- Verilog HDL  
- EDA Playground  
- Digital Design Concepts (Shift Registers, Counters)

---

## Limitations

- Fixed baud rate using prescaler  
- No parity bit support  
- No error detection mechanism  
- Not designed for high-speed industrial applications  

---

## Future Improvements

Possible improvements include:

- Configurable baud rate generator  
- FSM-based UART design  
- Parity and error detection  
- FIFO buffering  
- FPGA hardware implementation  

---

## Author

**Sarthak Sutariya**  
B.Tech – Electronics and Communication Engineering  
Charotar University of Science and Technology (CHARUSAT)

Project Title: *Serial Communication using UART in Verilog* 
