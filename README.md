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

## Utilization Factor and Aspect Ratio in Chip Design

The utilization factor and aspect ratio are key metrics in chip design, especially during floorplanning, as they play a vital role in optimizing layout for efficiency in performance, power consumption, and manufacturability.

**Utilization Factor:**

The utilization factor is the ratio of the area occupied by standard cells, macros, and other active components to the total available core area of the chip.

![Screenshot (1079)](https://github.com/user-attachments/assets/98381907-4010-4cb6-a070-041535eadc0a)


![Screenshot (1081)](https://github.com/user-attachments/assets/efa6fe15-3895-4ab9-a6d7-13dde2465f93)

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

![Screenshot (1079)](https://github.com/user-attachments/assets/98381907-4010-4cb6-a070-041535eadc0a)

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

## Preplaced cells:

preplaced cells refer to functional blocks or modules that are placed in specific locations on the chip before the detailed placement and routing phases. These cells are typically critical components that must meet certain design constraints, such as timing, power, or connectivity requirements.


![Screenshot (1086)](https://github.com/user-attachments/assets/18400f2f-4a6e-4e97-a2eb-53402f85ae10)

<details>
  <Summary>Steps to Define the Location of Preplaced Cells:</Summary>
 
  - Analyze Functional Requirements
    
  - Partition the Chip
  
  - Place Based on Timing Constraints
  
  - Optimize Power Distribution
  
  - Manage Thermal Constraints
  
  - Respect Physical Constraints
  
  - Define Block Shapes and Boundaries
  
  - Account for Routing Congestion
  
  - Iterate and Validate

</details>

### Illustrative Snapshots of Preplaced Cells: Layout and Design Considerations

![Screenshot (1083)](https://github.com/user-attachments/assets/4117a140-1c35-4b0d-a3d8-a1350ab0f5da)



![Screenshot (1085)](https://github.com/user-attachments/assets/1f6247cc-56b0-4db6-b34b-534a75ec7771)


### Proposed Placement:

#### Complete Design:

![Screenshot (1103)](https://github.com/user-attachments/assets/0d1f3b22-d427-4e7a-a490-d8c65019c969)




**Launch Flip-Flop (LFF):**

Place at the bottom-left corner of the logic block as the starting point of the signal path.

**AND Gate:**

Place to the right of the LFF, ensuring minimal wire length between them.

**OR Gate:**

Place to the right of the AND gate, maintaining a compact signal path.

**Capture Flip-Flop (CFF):**

Place at the top-right corner, completing the critical timing path.

**Decoupling Capacitors:**

Place near the LFF and CFF to stabilize the supply voltage during switching.
Also, distribute capacitors close to the AND and OR gates to reduce noise and ensure smooth transitions.

![Screenshot (1091)](https://github.com/user-attachments/assets/54412b0a-0121-42df-8b56-b72a269a9fc3)

## Configuration of the Design:

![Screenshot from 2025-01-19 23-49-02](https://github.com/user-attachments/assets/e816b412-b787-40ef-ad62-625a47acb097)

The configuration file for floorplanning in VLSI SoC design includes several key sections. The [GENERAL] section specifies design parameters such as the name of the SoC design, the manufacturing technology node, the standard cell library to be used, the aspect ratio of the die, and the total die area.

- The **Synthesis** Converts high-level RTL design into a gate-level netlist using standard cell libraries, optimizing for area, power, and performance while meeting timing constraints.

![Screenshot from 2025-01-19 23-47-42](https://github.com/user-attachments/assets/29539722-625b-4431-b39b-c19ffb828e71)


- The **FLOORPLAN_CONSTRAINTS** section defines constraints like the percentage of core area utilized by cells, the margin around the core, the minimum spacing between IO cells and the core, and whether to block specific regions from cell placement.

![Screenshot from 2025-01-19 23-47-54](https://github.com/user-attachments/assets/4f05d12d-eedb-4b81-810f-e554af58498f)

- The **POWER_PLAN** section provides details for power distribution, including the metal layers used for the power grid, the width and spacing of power straps, and the locations of power and ground pins.

- The **MACROS** section includes parameters for macro placement, such as the placement strategy, the minimum spacing between macros, and the allowed orientations for macros.

- The **PLACEMENT** section includes constraints on cell placement, such as the maximum allowable displacement for cells and the standard cell row height.

![Screenshot from 2025-01-19 23-48-01](https://github.com/user-attachments/assets/6f2199b8-d920-4ebd-b72d-c65811a424d3)

- The **Routing** Connects the placed components using metal layers, adhering to design rules and minimizing delays, congestion, and signal integrity issues.

- The **Magic** A VLSI layout tool used for creating, editing, and verifying physical designs, including Design Rule Checking (DRC) and visualization.

![Screenshot from 2025-01-19 23-48-09](https://github.com/user-attachments/assets/8fc16883-1fdd-4b05-bfa3-15c80c85dc4d)

- **The LVS (Layout vs. Schematic)** Verifies that the physical layout matches the intended circuit schematic by comparing connectivity and component parameters.

- The **Flow Control** Manages the sequence of design steps (e.g., synthesis, placement, routing) and automates tasks to ensure smooth and efficient execution of the design flow.

![Screenshot from 2025-01-19 23-48-21](https://github.com/user-attachments/assets/baca0be8-a873-4a7f-bdae-152dc253ce89)


This structure ensures the design adheres to physical and technological constraints while optimizing placement and routing.

### Power planning

Power planning in the SoC (System-on-Chip) design flow is a critical aspect of ensuring that the chip meets its power, performance, and thermal requirements. It involves a combination of architectural, physical design, and verification steps to manage power consumption effectively. 

<details>
  <summary>Snapshots of the detailed explanation on Power Planning:</summary>

![Screenshot (1092)](https://github.com/user-attachments/assets/5d10ef97-2b84-4933-bab2-dd1a5e6d67b2)


![Screenshot (1093)](https://github.com/user-attachments/assets/20a37c22-47f3-4880-8be6-f71197b810c2)


![Screenshot (1094)](https://github.com/user-attachments/assets/df506785-4a21-4f22-b0dd-a159f8f3ad6b)

![Screenshot (1095)](https://github.com/user-attachments/assets/63c4f11e-f605-4805-8fbc-2b7613d34aa1)

![Screenshot (1096)](https://github.com/user-attachments/assets/16d6e771-f911-4cff-8588-6474a9cc65d0)
</details>

![Screenshot (1097)](https://github.com/user-attachments/assets/3a5fa361-0782-43fe-abe9-d8359c8fd03c)

### Pin Placement and Logical Cell Placement Blockage in SoC Design

**Pin Placement**
  
- Pin placement is crucial for ensuring efficient routing and signal integrity in an SoC design.

![Screenshot (1106)](https://github.com/user-attachments/assets/4339e04e-fc40-4273-98d9-02821ee6eba5)

**Power and Ground Pin Placement:**
  
- Distribute power pins evenly to minimize resistance and support current distribution across the chip.
- Place power pins near high-power blocks like processors to ensure proper power delivery.

**Placement Based on Block Locations:**

- Ensure pins for each block are placed near their corresponding cells to reduce long routing paths, improving speed and power efficiency.

**Logical Cell Placement Blockage**

![Screenshot (1106)](https://github.com/user-attachments/assets/ae5b6a83-d4d0-4a6f-9fe7-96456765e2bc)


<details>
  <summary>After power planning, cells are placed within the chip, respecting power domains and avoiding blockages.
</summary>
  
 **Respect Power Domains:**

- Cells should be placed in their respective power domains, ensuring they match the power requirements of each region.
  
**Avoid Blockages:**

- Physical Blockages: Regions where no cells can be placed due to power grids or analog circuits.
- Power Blockages: Areas where power-domain boundaries prevent placement of certain cells.
- Thermal Blockages: Areas where high-power cells should be avoided to prevent overheating.

**Placement of High-Power Modules:**

- High-power modules (e.g., processors, GPUs) should be placed strategically to avoid thermal issues and ensure proper cooling.

</details>

## Snapshots of the Floorplan and Placement:

- Contents of the floorplan.tcl file

![Screenshot from 2025-01-19 11-25-16](https://github.com/user-attachments/assets/b64705e1-468f-473f-89e7-88a0507aaf97)

![Screenshot from 2025-01-19 11-25-12](https://github.com/user-attachments/assets/d63041a0-fa7c-49af-b5df-89d498d686fb)

- Layout formation by reading the picorv32a.def file using magic tool for displaying the layout:

![Screenshot from 2025-01-19 11-32-47](https://github.com/user-attachments/assets/0ec5ac73-af9a-4cce-98a7-1a7d48780b5a)

![Screenshot from 2025-01-19 11-32-01](https://github.com/user-attachments/assets/fb833b4c-dfb3-4b50-a27a-828faf0d538c)

![Screenshot from 2025-01-19 11-30-06](https://github.com/user-attachments/assets/9280b5d3-1cfa-4cc0-89f9-67472eab3c49)

- Output of the layout by changing the distance between the IO pins to 2:

**set ::env(FP_IO_MODE) 2;**

![Screenshot from 2025-01-19 11-04-19](https://github.com/user-attachments/assets/397ac730-0f69-4396-92c0-d7f7efec6513)

- Layout fromation after reating the Placement.def file and displaying the layout using magic:

![Screenshot from 2025-01-19 11-39-17](https://github.com/user-attachments/assets/a3a80246-c5e9-4f7f-bfd1-89e5b15bd328)

![Screenshot from 2025-01-19 11-37-37](https://github.com/user-attachments/assets/d2e27d6c-ce33-4ea0-93b0-85fbaa053267)

### Die area:

- The die area refers to the total physical area of the silicon chip that contains all the integrated components, such as processors, memory, and peripherals. 

- It is typically measured in square micrometers (µm²) and is a critical parameter that impacts the cost, performance, and power efficiency of the SoC.

![Screenshot from 2025-01-19 11-29-29](https://github.com/user-attachments/assets/97ee5c53-6357-43de-b9fd-a22b242ccb06)

Die area = value / 1000 micrometer

Die area = (660685 / 1000 = 660.685 micrometer, 671405 / 1000 = 671.405 micromter)

## Die area = (660.685, 671.405) mm2
