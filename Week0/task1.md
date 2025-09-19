# Week 0 – Chip Design Flow Summary

### Summary of Chip Design Flow

1. **Specification & Application (O0, O1 stage)**  
   - The process begins by specifying the application in **C language** (compiled using GCC, in this case RISC-V GCC).  
   - The **C model acts as the specification (Spec)** of the hardware.  
   - The output from this stage is called **O1**.  
   - The goal is to verify that **O0 (the original spec) = O1 (compiled output)**. Once this matches, the specification is **frozen**.

2. **Hardware Representation (O2 stage)**  
   - Next, a **soft copy of the hardware** is written, using RTL in languages such as **Verilog** (or high-level hardware description tools like Bluespec or GCELL).  
   - The application is run on this hardware representation to generate **O2 output**.  
   - The check is that **O1 = O2**, ensuring RTL correctly matches the C specification.

3. **Processor and Peripherals / IPs**  
   - The design moves into building hardware blocks in Verilog:  
     - **Processor**: Must be written in **synthesizable Verilog**.  
     - **Peripherals / IPs**:  
       - **Macros**: Reusable synthesizable blocks (e.g., a clock divider).  
       - **Analog IPs**: Functional blocks such as a **10-bit ADC**, **PLL**, or **clock multiplier**. These are functional RTL models, not required to be synthesizable.

4. **SoC Integration (O3 stage)**  
   - Processor, peripherals, and IPs are integrated into a complete **SoC**.  
   - GPIOs and interconnects are added.  
   - The output here is **O3**, which must match earlier outputs: **O1 = O2 = O3**.

5. **Physical Design (RTL to GDS – O4 stage)**  
   - The verified RTL is taken through the **physical design flow**:  
     - Floorplanning, placement, clock tree synthesis (CTS), and routing.  
     - Generates the **GDSII file**.  
   - The output here is **O4**, and final verification ensures **O1 = O2 = O3 = O4**.

6. **Microcontroller vs. Microprocessor**  
   - **Microprocessor**: CPU core only (e.g., Intel 8085, 8086). External components are required for memory, peripherals, and I/O.  
   - **Microcontroller**: CPU + memory + peripherals + I/O all integrated on a single chip (SoC). Example: chips in Arduino boards or iWatch.

7. **Tape-out and Tape-in**  
   - **Tape-out**: The final GDSII file is sent to the foundry for fabrication.  
   - **Tape-in**: The fabricated silicon chip returns from the foundry for testing and deployment.

8. **Target Applications**  
   - The designed processor runs at **100 MHz – 130 MHz**.  
   - Targeted for products like **Arduino boards, smartwatches (iWatch), TV panels, and AC applications**.

---

✅ **Final Goal:**  
At every stage, the outputs must match: **O1 = O2 = O3 = O4**. This ensures the silicon chip behaves exactly as specified in the original C model.

