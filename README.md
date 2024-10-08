# VLSI-SoC-Design-RTL2GDS Flow using OpenLANE/Sky130
VSDSquadron, a cutting-edge development board based on the RISC-V architecture that is fully open-source and this processor has general-purpose interfaces that enable features of RISC-V instruction set architecture 
(ISA). In this workshop, I'm  focused on implementing the primary macro/block of the VSDSquadron processor using OpenLANE from RTL2GDSII. The VSDSquadron chip is a specialized development board often used in projects involving in various sensors, communication interfaces, and processing capabilities to support complex tasks.

#### Trainer/Mentor: Kunal Ghosh, Mohamed Shalan, Nickson Jose,

## About VSDFLOW (RTL-to-GDS) - synthesized netlist (Yosys), PNR tool (Qflow), STA tool (Opentimer)
vsdflow' is an  automated EDA tool based on TCL scripting which involves implementing in RTL language, and convert the design to hardware using VSD (RTL-to-GDS) flow ans it is developed using OPHW tools, where the user gives input RTL in verilog. From here on the VSDFLOW takes control, RTL is synthesized (using Yosys). There after the synthesized netlist is given to PNR tool (Qflow) and finally Sign-off is done with STA tool (using Opentimer). The output of the flow is GDSII layout and performance & area metrics of your design. VSDFLOW is is tested for 30k instance count design like ARM Cortex-M0, RISC-V picorv32, and also it can be tested for multi-million instance count using hierarchical design or glue logic.

#### Overview
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault and custom methodology scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII - this capability will be released in the coming weeks with completed SoC design examples that have been sent to SkyWater for fabricaiton. 

## OpenLANE Directory Struture

* work/tools/openlane_working_dir/openlane  (Directory to invoke the tool for working)
* sky130A will be used for this project
* pdks (skywater: all the pdk related files, timing files, tech files, lef, cell lef, open_pdks: silicon foundry files (any foundary) they are compatible to work with commercial tools and this convert commercial to opensource suport using scripts/files, sky130A: is for purely for opensource applications/designs)
* sky130A (libs.ref: contains all the process specific layer info, timing (PVT corners), libs, lef, verilog,rtl; lib.tech: specific to the tool-layout,spice,maic,qflow,openlane)
* We will use sky130A variant in the design implementation with sky130_fd_sc_hd

![image](https://github.com/user-attachments/assets/0bac2173-e9b9-41f5-b68a-965e18294219)

![image](https://github.com/user-attachments/assets/4224a4f9-a2c2-4cbe-84c8-c2eea2e664b1)

![image](https://github.com/user-attachments/assets/e776f29a-5850-4afc-8bb6-237aee3608e2)


# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit

Screenshots examples for the reference.
![image](https://github.com/user-attachments/assets/aa91bbd1-7393-4620-9f43-194a3d3c7a02)

![image](https://github.com/user-attachments/assets/02110eb5-8d89-424c-9a31-bc6c5fe1bdeb)


