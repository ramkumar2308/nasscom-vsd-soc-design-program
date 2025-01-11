# Digital VLSI SoC Design & Planning
#### _2 Week digital VLSI SoC design and planning workshop with complete RTL2GDSII flow_
This repository offers resources and examples for designing and planning VLSI (Very Large Scale Integration) and SoC (System on Chip) systems, covering the complete design flow from specifications to physical implementation with a focus on modern semiconductor methodologies and tools.
# VLSI Desgin Flow
#### _The VLSI Design Flow involves a series of well-defined steps to convert a high-level system specification into a physical silicon chip._

<details>
<summary>The flow is divided into front-end and back-end stages:</summary>
**1. Specification:**
- Define system-level functionality, performance, power, and area requirements.
- Decide on architecture and high-level design specifications.
  
**2. Architecture Design:**
- Plan the system architecture, including processor, memory, and interconnects.
- Allocate resources and create block-level diagrams.

**3. RTL Design (Register Transfer Level):**
- Write the functional design using Hardware Description Languages (HDLs) like Verilog or VHDL.
- Implement the digital logic design.

**4. Functional Verification:**
- Verify the RTL design against the specifications.
- Use testbenches, simulations, and formal verification to ensure correctness.

**6. Synthesis:**
- Convert the RTL code into a gate-level netlist using a synthesis tool.
- Optimize for area, power, and timing constraints.

**6. Design for Testability (DFT):**
- Add test structures like scan chains or Built-In Self-Test (BIST) to facilitate post-fabrication testing.

**7. Floorplanning:**
- Define the physical layout of the chip, including placement of blocks and I/O pins.
- Plan for power, clock distribution, and routing channels.

**8. Placement:**
- Place the standard cells and macro blocks from the gate-level netlist within the floorplan.

**9. Clock Tree Synthesis (CTS):**
- Design a balanced clock tree to minimize skew and ensure timing integrity.

**10. Routing:**
- Connect all the components using metal layers for signal and power routing.

**11. Static Timing Analysis (STA):**
- Analyze the design to ensure it meets all timing requirements.

**12. Power Analysis:**
- Evaluate the power consumption and optimize for power efficiency.

**13. Physical Verification:**
- Perform checks like Design Rule Check (DRC) and Layout vs. Schematic (LVS) to ensure the layout matches the design.

**14. Tape-Out:**
- Finalize the design and prepare it for manufacturing.

**15. Fabrication:**
- Send the tape-out design to a foundry for silicon fabrication.

**16. Testing and Validation:**
- Test the manufactured chip using Automatic Test Equipment (ATE) to ensure it functions as intended.
</details>
These steps ensure a systematic and efficient approach to designing reliable, high-performance VLSI chips.
