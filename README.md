# Digital VLSI SoC Design & Planning
This repository offers resources and examples for designing and planning VLSI (Very Large Scale Integration) and SoC (System on Chip) systems, covering the complete design flow from specifications to physical implementation with a focus on modern semiconductor methodologies and tools.
# VLSI Desgin Flow
#### _The VLSI Design Flow involves a series of well-defined steps to convert a high-level system specification into a physical silicon chip._

<p align="center">
  <img src="https://github.com/user-attachments/assets/e208d6c8-ef85-435d-bca9-783ac4b5d0ce" width="600">
</p>
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

# Content
## Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK
**1. Understanding the Chip Package and Wire Bonding:**

 In embedded boards, what we call the "chip" is actually its package—a protective casing around the actual chip. The chip itself is typically located at the center of the 
 package, with connections established using the wire bonding method, a basic wired connection.
 
**2. Structure of a Semiconductor Die:**

Inside a chip, signals to and from the external world pass through pads. The core, housing the chip's digital logic, is surrounded by these pads. Together, the core and pads form the die, the fundamental unit of semiconductor manufacturing.

**3. Foundries, IPs, and Macros in Semiconductor Manufacturing:**

A foundry is where semiconductor chips are manufactured. Foundry IPs are specialized intellectual properties requiring advanced expertise, while repeatable digital logic blocks are known as macros.

### Understanding ISA (Instruction Set Architecture)
- **Compilation:** The C program is compiled into assembly language using a specific ISA, such as RISC-V (Reduced Instruction Set Computing - V).
- **Conversion:** The assembly code is then translated into machine language (binary logic 0s and 1s) that the hardware understands.
- **Implementation:** The RISC-V specification is implemented using an RTL (Register Transfer Level) hardware description language.
- **Physical Design:** The RTL is converted into a physical layout using the standard PnR (Place and Route) or RTL-to-GDSII flow.

# Implementation

### Design Preparation and Synthesis Run Snapshots

![Screenshot from 2025-01-12 00-06-07](https://github.com/user-attachments/assets/b34c009e-f916-4a8e-93aa-3169a7f213ce)

![Screenshot from 2025-01-12 00-07-15](https://github.com/user-attachments/assets/4a365e1f-d909-4c9f-8c63-d4df3641cda1)

![Screenshot from 2025-01-12 00-09-13](https://github.com/user-attachments/assets/42c4ec9d-2c76-4e58-bce3-dfb7381d35e1)


## Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

The **yosys_2.stat.rpt** file is generated as part of the synthesis process in Yosys, an open-source hardware synthesis tool. It provides a comprehensive report of synthesis statistics, offering detailed insights into the design post-synthesis.
<details>
<summary>This yosys_2.stat.rpt file helps designers analyze the following aspects of their hardware design:</summary>

- **Module Statistics:** Details of synthesized modules, including their instances and resource utilization.
- **Cell Statistics:** Information on the types and counts of standard cells or logic elements used.
- **Top-Level Design Summary:** Overall summary of the synthesized design, including the total number of cells, I/O ports, and gate count.
- **Utilization Metrics:** Resource usage such as logic gates, registers, and multiplexers.
- **Warnings and Errors:** Alerts regarding issues encountered during synthesis, such as unconnected ports or unsupported constructs.
</details>

### Calculating the Flop Ratio:

Flop Ratio = Number of D Flipflops / Total number of cells

Percentage of DFF's = Flop Ratio * 100

### Synthesis Report for PicoRV32A

![Screenshot from 2025-01-12 00-21-45](https://github.com/user-attachments/assets/506fdd01-eee0-4d72-bd12-ee6c38eb2697)

![Screenshot from 2025-01-12 00-21-55](https://github.com/user-attachments/assets/ddca09a1-c143-4d49-a91d-083e032ed889)

No. of D Flipflops = 1613

No. Cells = 14876

Flop Ratio = No. of D Flipflops/ No. of Cells = 1613 / 14876

## Flop Ratio = 0.1084

Percentage of DFF's = 0.1084 * 100 
## Percentage of DFF's = 10.842 %

# Day 2 - Good floorplan vs bad floorplan and introduction to library cells

Floorplanning is a critical step in the physical design flow of a System-on-Chip (SoC). It involves defining the layout of various blocks and components on the chip to optimize performance, area, power, and manufacturability.

<details>
<summary>Key Goals of Floorplanning:</summary>

- **Optimize Placement:** Arrange logic blocks and macros efficiently to minimize wirelength and reduce delay.
- **Power Management:** Ensure proper placement of power distribution networks.
- **Thermal Management:** Avoid hotspots by spreading power-hungry blocks appropriately.
- **Clock Distribution:** Facilitate uniform and low-skew clock routing.
- **Area Utilization:** Maximize the utilization of the available chip area while leaving room for routing and buffers.
- **Partitioning:** Group related modules together for better performance and ease of routing.
</details>

<details>
<summary>Key Steps in Floorplanning:</summary>
- **Chip and Core Area Definition:** Define the overall dimensions of the chip and core area.
- **Macro Placement:** Place large blocks like memories, IP cores, and analog components.
- **Boundary Constraints:** Specify I/O pin placement and keep-out zones.
- **Power Planning:** Establish power grids and ensure uniform power distribution.
- **Placement Blockages:** Mark areas where placement is restricted (e.g., under macros).
- **Aspect Ratio and Die Size:** Determine the chip aspect ratio and calculate die size based on design requirements.
</details>

# Utilization Factor and Aspect Ratio in Chip Design

The utilization factor and aspect ratio are key metrics in chip design, especially during floorplanning, as they play a vital role in optimizing layout for efficiency in performance, power consumption, and manufacturability.

**Utilization Factor:**

The utilization factor is the ratio of the area occupied by standard cells, macros, and other active components to the total available core area of the chip.

  ### Utilisation factor = Area occupied by netlist / Total Area of the Core
<details>
  <summary>Purpose and Standard Metrics</summary>
  
**Purpose:**

- Ensures efficient use of available space.
- Leaves enough room for routing wires and buffers.

**Typical Values:**

- Low Utilization: Leads to wasted space but allows easier routing.
- High Utilization: Saves area but may cause routing congestion and timing issues.
</details>

**Aspect Ratio:**

The aspect ratio defines the shape of the chip or core area by comparing its height to its width.

### Aspect Ratio = Height / Width
<details>
  <summary>Purpose and Standard Metrics</summary>
  
**Purpose:**

- Determines whether the chip is square, rectangular, or elongated.
- Impacts the placement of components and the efficiency of routing.

**Typical Values:**

- An aspect ratio close to 1 results in a square layout, which is often ideal for balanced placement and routing.
- Rectangular shapes are used when specific design constraints (like die size or I/O pin placement) demand it.
</details>

