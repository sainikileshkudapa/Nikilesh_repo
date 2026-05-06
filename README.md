# Synchronous FIFO Design in Verilog

This project implements a Synchronous FIFO (First In First Out) memory using Verilog HDL along with a testbench for simulation and verification.

## Project Files

* `synfifo.v`
  Verilog RTL design of the synchronous FIFO.

* `synfifo_tb.v`
  Testbench used to simulate and verify FIFO functionality.

---

## Features

* Synchronous read and write operations
* FIFO full condition detection
* FIFO empty condition detection
* Parameterized FIFO behavior
* Simulation-ready Verilog code

---

## FIFO Overview

A FIFO is a memory structure where:

* Data written first is read first
* Data operations are controlled using a clock signal

This design uses:

* Write pointer
* Read pointer
* Status flags (`full`, `empty`)

---

## Simulation

The testbench verifies:

* Write operations
* Read operations
* FIFO full condition
* FIFO empty condition

---

## Tools Used

* Verilog HDL
* Xilinx Vivado

---

## How to Run in Vivado

1. Open Vivado
2. Create a new RTL project
3. Add:

   * `synfifo.v`
   * `synfifo_tb.v`
4. Set `synfifo_tb.v` as simulation source
5. Run Behavioral Simulation

---

## Authors

* Sai Nikilesh Kudapa
* Charan Kopparla
