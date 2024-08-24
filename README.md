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

## Day 2
### Floorplanning
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
### Placement
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

### Library characterization and modelling
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


## Day 3
### Std cell design
- available at https://github.com/nickson-jose/vsdstdcelldesign
  - Not covered in detail in this course
  - Study spice deck for cell
  - study cell model files
  - Evaluate effect of size of pmos and nmos cells
    <img width="585" alt="spice deck" src="https://github.com/user-attachments/assets/243fac1a-5403-43f9-95ef-16a17d11129e">
    <img width="569" alt="size comp" src="https://github.com/user-attachments/assets/ad6b9c8f-195e-4665-aa66-c8ae5d315d97">
    <img width="443" alt="spice model file" src="https://github.com/user-attachments/assets/6f505ddb-5433-4648-9a4f-c6382db3da30">

- We Then learned the basics of the fabrication process
  - 16 mask CMOS process
      - Selecting a substrate
      - N well and P well formation
      - Creating active region for transistors (mask1)
      - Gate Formation
      - Light doped drain (LDD) formation
      - Source and drain formation
      - Forming contacts and local interconnects
      - Higher level metal formation
<img width="460" alt="fabricated cmos" src="https://github.com/user-attachments/assets/2a753413-cf36-4e8e-8363-aefb4638a3f5">

- custom cell
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane$ git clone https://github.com/nickson-jose/vsdstdcelldesign.git

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic$ cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$ magic -T sky130.tech sky130_inv.mag 

vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$ magic -T sky130A.tech sky130_inv.mag 

ngspice sky130_inv.spice
```
### Extracting cell to use in design
- Extract the custom inverter cell using ext2spice
  - Extract cell
  - ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_14_24_10](https://github.com/user-attachments/assets/c70c7b72-76e3-4278-9e38-0c5562ced0ec)

  - study cell layout using magic & check drc (lab)
  - ![drc](https://github.com/user-attachments/assets/3bca3c4c-e1dc-4e34-80c2-5f866c5dd621)

  - run ngspice simulation
![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_14_48_50](https://github.com/user-attachments/assets/91802287-fe01-403e-9c6d-6cf58da88a6b)

```
    To deal with spikes
    Close less
    Open spice file
    Change defined between output Y pin and gnd
    Change 0.02 farad to 0.2 farad
```
![image](https://github.com/user-attachments/assets/60b1d784-ff8a-4170-80fd-fc083be46c3f)

  - calculated
    - fall transition
    - ![fall transition 20](https://github.com/user-attachments/assets/b0b68f66-c476-4ba3-9d0a-db1c30310582)
    - ![fall transition 80](https://github.com/user-attachments/assets/a5b7786f-b75a-4126-9b1a-fd3c4fdd85f0)


```
x0 = 2.18e-09, y0 = 0.66

x0 = 2.121e-09, y0 = 2.63979

==> 0.059ns
```
  - - rise transition
    - ![rise transition 20](https://github.com/user-attachments/assets/c79888c8-c83f-4a17-aea1-75d71f62cfb1)
    - ![rise transition 80](https://github.com/user-attachments/assets/9d0a55fb-cf27-420a-8b71-4e68b42fa935)


```
x0 = 4.02002e-09, y0 = 0.659928

x0 = 4.08115e-09, y0 = 2.64128

==> 0.06113 ns
```
  - - fall delay
    - ![fall delay](https://github.com/user-attachments/assets/9c386c8a-ba70-4fc4-a1a0-eda141cf540b)

```
x1 = 2.15007e-09, y1 = 1.65
x0 = 2.18664e-09, y0 = 1.65

==> 0.03657 ns
```
  - - rise delay
    - ![rise delay](https://github.com/user-attachments/assets/009ec3ec-423d-43db-a3db-be985ddb457f)

```
x0 = 4.05002e-09, y0 = 1.64994

x0 = 4.05322e-09, y0 = 1.65012

==> 0.0032 ns
```
- Now we have characterised out inverter, we now create a LEF file which we use in our openlane for picorv32
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/libs$ sky130_rohang.lef
```
 ### Lab introduction to magic tools option and DRC rules
```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

tar xfz drc_tests.tgz
```
- Draw large area of m3 contact
  ![m3contact](https://github.com/user-attachments/assets/29c6800e-9b3f-452e-978b-b0131f49feea)
```
cif see via2
```
  ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_17_29_17](https://github.com/user-attachments/assets/12b8c405-af1f-4118-a8f1-e8ca9e051728)

- - Tech files has commands to tell magic how to draw contact cuts inside contact area


- Lab excersize fix ploy.9 error in sky130 tech file
```
poly

distance nplyres and poly = 0.240 microns

rule: ploy.09
Poly resistor spacing to poly or spacing (no overlap) to diff/tap 0.480µm

==> rule violation
```
![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_17_42_42](https://github.com/user-attachments/assets/bc3e96c4-6754-4e77-8070-7931d8fbf14b)
![poly](https://github.com/user-attachments/assets/f1a4bdff-4eea-418c-89d4-4882d2c36d3e)
![ploy rule 9](https://github.com/user-attachments/assets/12a6c036-dcde-4d4c-9a3a-72ff6a20aee7)
![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_18_42_45](https://github.com/user-attachments/assets/7fc4f7aa-af7d-46ec-b3b6-23da311b0328)

- implement poly resistor spacing to diff and tap

-Lab challenge to find missing or incorrect rules and fix them

  - Rule n well.4 is example i.e. all n well will contain metal contacted tap
    ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_19_00_10](https://github.com/user-attachments/assets/e1bdf96d-9fa2-41da-890e-131a5e28b6b6)
    ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_19_36_33](https://github.com/user-attachments/assets/62fff7cd-2900-4053-93f6-926974a3d865)
    ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_19_39_04](https://github.com/user-attachments/assets/1f2c30e6-982a-412a-9776-d5a27367fa23)






