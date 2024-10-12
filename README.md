# VLSI-SoC-Design-RTL2GDS Flow using OpenLANE/Sky130
VSDSquadron, a cutting-edge development board based on the RISC-V architecture that is fully open-source and this processor has general-purpose interfaces that enable features of RISC-V instruction set architecture 
(ISA). In this workshop, I'm  focused on implementing the primary macro/block of the VSDSquadron processor using OpenLANE from RTL2GDSII. The VSDSquadron chip is a specialized development board often used in projects involving in various sensors, communication interfaces, and processing capabilities to support complex tasks.

#### Trainer/Mentor: Kunal Ghosh, Mohamed Shalan, Nickson Jose,

## About VSDFLOW (RTL-to-GDS) - synthesized netlist (Yosys), PNR tool (Qflow), STA tool (Opentimer)
vsdflow' is an  automated EDA tool based on TCL scripting which involves implementing in RTL language, and convert the design to hardware using VSD (RTL-to-GDS) flow ans it is developed using OPHW tools, where the user gives input RTL in verilog. From here on the VSDFLOW takes control, RTL is synthesized (using Yosys). There after the synthesized netlist is given to PNR tool (Qflow) and finally Sign-off is done with STA tool (using Opentimer). The output of the flow is GDSII layout and performance & area metrics of your design. VSDFLOW is is tested for 30k instance count design like ARM Cortex-M0, RISC-V picorv32, and also it can be tested for multi-million instance count using hierarchical design or glue logic.

#### Overview
OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, Fault and custom methodology scripts for design exploration and optimization. The flow performs full ASIC implementation steps from RTL all the way down to GDSII - this capability will be released in the coming weeks with completed SoC design examples that have been sent to SkyWater for fabricaiton. 

## OpenLANE Design Stages via Interactive Mode

1. ./flow.tcl -interactive
2. % package require openlane 0.9
3. prep -design <design> -tag <tag> -config <config> -init_design_config -overwrite
4. run_synthesis
5. run_floorplan
6. run_placement
7. run_cts
8. run_routing
9. run_magic
10. run_magic_spice_export
11. run_magic_drc
12. run_netgen
13. run_magic_antenna_check

## Chapter -1: OpenLANE Directory Structure & openLANE flow directory

* work/tools/openlane_working_dir/openlane  (Directory to invoke the tool for working)
* sky130A will be used for this project
* pdks (skywater: all the pdk related files, timing files, tech files, lef, cell lef, open_pdks: silicon foundry files (any foundary) they are compatible to work with commercial tools and this convert commercial to opensource suport using scripts/files, sky130A: is for purely for opensource applications/designs)
* sky130A (libs.ref: contains all the process specific layer info, timing (PVT corners), libs, lef, verilog,rtl; lib.tech: specific to the tool-layout,spice,maic,qflow,openlane)
* We will use sky130A variant in the design implementation with sky130_fd_sc_hd

![image](https://github.com/user-attachments/assets/0bac2173-e9b9-41f5-b68a-965e18294219)

![image](https://github.com/user-attachments/assets/4224a4f9-a2c2-4cbe-84c8-c2eea2e664b1)

![image](https://github.com/user-attachments/assets/e776f29a-5850-4afc-8bb6-237aee3608e2)


#### Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

#### alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
#### We have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

#### OpenLANE flow contained docker sub-system so invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

#### OpenLANE flow required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

#### Open the design with some necessary files and directories of 'picorv32a' using the below command
prep -design picorv32a

#### Run synthesis flow using below command
run_synthesis

#### Exit from OpenLANE flow & docker sub-system
exit


Screenshots examples for the reference.
![image](https://github.com/user-attachments/assets/aa91bbd1-7393-4620-9f43-194a3d3c7a02)

![image](https://github.com/user-attachments/assets/02110eb5-8d89-424c-9a31-bc6c5fe1bdeb)

![image](https://github.com/user-attachments/assets/7f0b175c-11e5-4d7c-b546-92dbc366b1a8)

![image](https://github.com/user-attachments/assets/31012a31-f858-4dfe-84b5-b6280d7c0162)

![image](https://github.com/user-attachments/assets/64523b16-29e7-472c-961d-445ca8ae1497)

![image](https://github.com/user-attachments/assets/a2fe8e41-a5a8-4032-8744-040256fcbbc0)

#### Calculating D-Flop Ratio in the design from synthesis statistics report:

Flop Ratio (FR) = (No. of Flip Flops [dfxtp_2:1613]/Total Number of Cells [14876])*100
FR=0.108429685*100 = 10.85%

![image](https://github.com/user-attachments/assets/29bf8ae9-05d5-4091-a7bb-f6da5b4a993f)

## Chapter-2: Floorplan and INTRO to Library Cell

Implementing the picorv32a Design FP Using OpenLANE flow.

1. Define die area in Microns.
2. Load FP DEF in Magic Tool.
    -  cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/07-09_20-37/results/floorplan/
    -  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
4. Execute congestion-Aware based Placement.
5. Load placement DEF in Magic Tool.

The following are the executing commands and image references for the above steps: 
1. cd Desktop/work/tools/openlane_working_dir/openlane
2. alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
3. docker
4. ./flow.tcl -interactive
5. package require openlane 0.9
6. run_synthesis
7. run_floorplan
8. exit

![image](https://github.com/user-attachments/assets/3f27f271-1e68-4327-8781-0f2ddfbad4d1)

![image](https://github.com/user-attachments/assets/072b124d-3625-4f8a-8127-97a676f543f9)

![image](https://github.com/user-attachments/assets/ce07f689-6ab0-463c-b1ee-751ad9a21311)

#### Die area of the chip is X: 660um & Y: 671.4um  
![image](https://github.com/user-attachments/assets/71608836-52f5-4fd2-af46-05bed7c68a4e)

Floorplan Loaded in Magic using tech file, lef file, def file
1. cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/07-09_20-37/results/floorplan/
2. magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

![image](https://github.com/user-attachments/assets/5711f76c-b9a5-4866-8735-52223f60a107)

![image](https://github.com/user-attachments/assets/736d78d6-dc78-4b9f-895a-82e07f56f259)










