# Digital VLSI design & SoC planning - NASSCOM, VSD
## Day 1
- introduction to open source SoC design tools and the various parties involved
- introduction to Openlane flow
- tool installation
- exploring openlane tool directory
- running tool using interactive flow
- preping design
- running synthesis
- checking output files
- assignment : Flop ratio = 1613/14876 = 0.10842968539930088733530518956709 = 10.84%

```
docker
pwd
ls -ltr
flow.tcl -interactive 
package require openlane 0.9
prep -design picorv32a
run_synthesis

```

![Open source EDA tools](day1/1.png)
Fig: Open source EDA tools
![Openlane ASIC flow](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day1/Untitled%20picture.png)
Fig: Openlane ASIC flow
![RTL to GDSII flow ](day1/2.png)
Fig: RTL to GDSII flow 
![Openlane interactive flow](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day1/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_01_52_30.png)
Fig: Openlane interactive flow
![Exploring Openlane directory](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day1/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_03_06_15.png)
Fig: Exploring Openlane directory
![Synthesis result](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day1/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_02_58_13.png)
Fig: Synthesis result
![Synthesis resultant files exploration](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day1/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_03_07_04.png)
Fig: Synthesis resultant files exploration

# Day 2
- Floorplanning
- Define width and height of core and die
- Define locaation of preplaced cells
- Decoupling Capacitor
- Power planning
- Pin placement
- Logical cell placement blockage
- Die area = (660685/1000)(671405/1000) = 443,587.212425 sq um


```
run_floorplan
```
or
```
init_floorplan
place_io
tap_decap_or
```
To check floorplan layout
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

- Placement
- Bind netlist with physical cells
- optimize placement using wire length and capacitance
- Repeters to maintain signal integrity but loss of area
- capacitance leads to slew

```
run_placement
```
check output
```
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-08_03-33/results/placement$ magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
optimization
```
set ::env(FP_IO_MODE) 2
run_floorplan
```

- Library characterization and modelling
- Cell design flow
- Characterization flow
- - Read model file
  - read extracted spice netlist
  - define buffer behavior
  - read buffer subcircuit
  - read necessary power supply
  - attach stimulus to charcterization setup
  - give necessary output capacitance
  - give simulation command (.trans, .dc)
- input 1-8 to GUNa software (Fig)
- - Timing & noise power characterization output
  
- Timing introduction
- - Timing threshold definitions
  - Timing characterization
  - - Propagation delay
    - Transition time
