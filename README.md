# 2D Convolutional Network (CNN Layer) - VHDL Implementation

This project involves the design and VHDL implementation of a two-dimensional Convolutional Network (CN), developed for the *Electronics & Communication Systems* course at the University of Pisa (Academic Year 2025/2026).

**Authors:** * Samuel Scarabelli
* [Francesco Rossi Paccani](https://github.com/FrancescoRossiPaccani)

## 🎯 Project Objective
The system performs a convolution operation between an input matrix and a filter. The design was developed using a bottom-up approach and can handle 8-bit serial inputs, ensuring correct processing even under partial data-loading conditions.

## ⚙️ Developed Architectures
The project includes two different RTL implementations:

1. **Original Version:** Utilizes a pure combinational approach for processing, leveraging a chain of Ripple Carry Adders (RCA) and parallel multiplexers. It generates a new output element every clock cycle ([`Conv_2d.vhdl`](./src/Conv_2d.vhdl)).
2. **Optimized Version:** Designed to reduce the critical path and maximize the clock frequency. It replaces the RCA chain with a specialized synchronous counter (`COUNTER_OPT`) and the multiplexers with a shift register. The data flow is managed by a Finite State Machine (FSM), making the system highly scalable as the matrix (N) and filter (M) dimensions increase ([`Conv_2d_opt.vhdl`](./src/Conv_2d_opt.vhdl)).

## 🧪 Validation and Testing
The design was rigorously verified using **ModelSim**, achieving **100% code coverage**.
* We performed 7 distinct testbenches to verify the module's behavior under normal conditions and critical scenarios (e.g., incorrect control signals, race conditions).
* The hardware results were validated by automatically comparing them with a **high-level model written in C++**.

## 📊 FPGA Synthesis Results
The implementation was tested on the **xc7z010clg400-1** FPGA target using Vivado:
* **Efficiency and Power:** The optimized version shows lower dynamic power consumption, with a reduction of about 14% (13 mW) compared to the original version for small matrices (N=5, M=3).
* **Scalability and Timing:** When drastically increasing the dimensions (e.g., N=27, M=16), the original version fails the timing constraints (negative WNS), while **the optimized version maintains a highly positive Worst Negative Slack (WNS)**, confirming excellent robustness and high-frequency tolerance.

## 📄 Documentation
For an in-depth analysis of the RTL architecture, the tests performed, and the Vivado power/timing reports, please refer to the official documentation in the `docs/` folder.

## ⚖️ License
This project is released under the MIT License. See the `LICENSE` file for details.
