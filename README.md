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
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/floorplan%20ready.png)
Fig: Floorplan results
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_17_29_16.png)
Fig: Floorplanning log file exploration
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_15_08_2024_18_10_14.png)
Fig: Floorplanning log file exploration
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/15-08%20config%20tcl.png)
Fig: Floorplanning logs
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_08_55_02.png)
Fig: Floorplanning layout
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_08_55_59.png)
Fig: Showing decapacitors
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_08_57_08.png)
Fig: preplaced cells
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
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_09_09_59.png)
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_09_11_58.png)
Fig: Placement result
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/VirtualBox_vsdworkshop_nasscom_rohan_16_08_2024_09_12_25.png)
Fig: Placed cells

- Library characterization and modelling
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/Library%20characterization%20and%20modelling.png)
- Cell design flow
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/Cell%20design%20flow.png)
- Characterization flow
- - Read model file
  - read extracted spice netlist
  - define buffer behavior
  - read buffer subcircuit
  - read necessary power supply
  - attach stimulus to charcterization setup
  - give necessary output capacitance
  - give simulation command (.trans, .dc)
- input 1-8 to GUNa software (Fig below)
- - Timing & noise power characterization output
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/characteriztion%201.png)
![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/characterization%202.png)
- Timing introduction
- - Timing threshold definitions
    ![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/Timing.png)
  - Timing characterization
  - - Propagation delay
      ![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/prop%20delay.png)
    - Transition time
      ![](https://github.com/Rohan7Gupta/VSD_NASSCOM_SoC_Design_Program/blob/main/day2/transition.png)


# Day 3
- Std cell desgined and available at https://github.com/nickson-jose/vsdstdcelldesign
- Not covered in detail in this course
- Study spice deck for cell
- study cell model files
- Evaluate effect of size of pmos and nmos cells
- Extract cell
- study cell layout using magic & check drc (lab)
- run ngspice simulation
- calculated
  - fall transition
```
x0 = 2.18e-09, y0 = 0.66

x0 = 2.121e-09, y0 = 2.63979

==> 0.059ns
```
  - rise transition
```
x0 = 4.02002e-09, y0 = 0.659928

x0 = 4.08115e-09, y0 = 2.64128

==> 0.06113 ns
```
  - fall delay
```
x1 = 2.15007e-09, y1 = 1.65
x0 = 2.18664e-09, y0 = 1.65

==> 0.03657 ns
```
  - rise delay
```
x0 = 4.05002e-09, y0 = 1.64994

x0 = 4.05322e-09, y0 = 1.65012

==> 0.0032 ns
```
- custom cell
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane$ git clone https://github.com/nickson-jose/vsdstdcelldesign.git

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic$ cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$ magic -T sky130.tech sky130_inv.mag 

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$ magic -T sky130A.tech sky130_inv.mag 

ngspice sky130_inv.spice
```
