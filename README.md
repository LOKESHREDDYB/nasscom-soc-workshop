# VLSI-SoC-Design-RTL2GDS Flow using OpenLANE/Sky130
VSDSquadron, a cutting-edge development board based on the RISC-V architecture that is fully open-source and this processor has general-purpose interfaces that enable features of RISC-V instruction set architecture 
(ISA). In this workshop, I'm  focused on implementing the primary macro/block of the VSDSquadron processor using OpenLANE from RTL2GDSII. The VSDSquadron chip is a specialized development board often used in projects involving in various sensors, communication interfaces, and processing capabilities to support complex tasks.

#### Trainer/Mentor: Kunal Ghosh

## vsdflow
vsdflow' is an  automated EDA based TCL scripting tool which involves implementing in RTL language, and convert the design to hardware using VSD (RTL-to-GDS) flow ans it is developed using OPHW tools, where the user gives input RTL in verilog. From here on the VSDFLOW takes control, RTL is synthesized (using Yosys). There after the synthesized netlist is given to PNR tool (Qflow) and finally Sign-off is done with STA tool (using Opentimer). The output of the flow is GDSII layout and performance & area metrics of your design. VSDFLOW is is tested for 30k instance count design like ARM Cortex-M0, RISC-V picorv32, and also it can be tested for multi-million instance count using hierarchical design or glue logic.
