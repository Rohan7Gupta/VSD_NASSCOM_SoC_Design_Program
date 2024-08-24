# Digital VLSI design & SoC planning - NASSCOM, VSD
This Readme is  a record of work done in the digital VLSI design & SoC planning course 5 day workshop by VSD and NASSCOM. 
![image](https://github.com/user-attachments/assets/8d78d017-2779-49ac-999c-370e2956e27b)


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

## Day 4
### Lef file extraction
- For pnr we only need vdd, gnd , input and output
- This info is in LEF file
- No logic info, so we protects IP
- Extract LEF file and plug into picorv32 flow
- Input and output port must lie on intersection of vertical and horizontal power tracks
- Width of std cell odd multiple of track pitch and height odd multiple of track verticle pitch
- Stdcell design: ports should be on intersection of horizontal and vertical tracks
- Each track spaced 0.34 verticals and 0.46 horizontal, for every metal layer
- ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_21_21_37](https://github.com/user-attachments/assets/1ef3d8bf-9e24-44dd-954e-7345609f80c0)
- width of std cell odd multiple of x pitch (0.46)
- ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_21_30_35](https://github.com/user-attachments/assets/dfdd9266-0b6c-41b0-ac7a-5d8fb62f4fd8)
- ![image](https://github.com/user-attachments/assets/d518011e-ef3e-4d6b-b2d0-ad74a06ae127)
- ![image](https://github.com/user-attachments/assets/9071f0ef-32f4-42bd-a645-a3fc7cbb7de0)
- Extract lef file now
- ![VirtualBox_vsdworkshop_nasscom_rohan_18_08_2024_21_56_41](https://github.com/user-attachments/assets/57c42b6f-5c79-4db5-8985-e5285f3ced5a)
- Extracted cell
- ![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_10_55_00](https://github.com/user-attachments/assets/4904538e-fa4c-4d9b-a6ea-1e73762bbb67)
- we use sky130_fd_sc_hd__typical.lib
  
### Running the openlane flow with our custom cell
```
prep -design picorv32a : create new runs
prep -design picorv32a -tag 15-09_06-28 -overwrite : use that dir

run_synthesis

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) DELAY

```
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_11_30_27](https://github.com/user-attachments/assets/b1244542-58d7-4475-b6e7-89ad4ccbf2d7)
Fig: Running Synthesis
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_11_30_36](https://github.com/user-attachments/assets/0559ae21-a16c-4029-9354-3d318d793b5a)
Fig: config.tcl
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_11_39_58](https://github.com/user-attachments/assets/21263085-2018-499a-a1a2-640e296cf9d0)
Fig: Our cell in synthesis file
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_11_40_17](https://github.com/user-attachments/assets/df51b846-1d54-47fd-84ef-be88216f9fc2)
Fig: Our custom cell in synthesis logs
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_11_40_25](https://github.com/user-attachments/assets/d611627e-19c2-4be0-beb9-feb16b1c779b)
Fig: Synthesis successful
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_18_41_02](https://github.com/user-attachments/assets/dd583e97-2428-4653-b106-c3649c63824b)
Fig: pre-STA result
- set synth strategy from AREA 0 to DELAY 0 (to reduce delay & slack)
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_19_00_09](https://github.com/user-attachments/assets/8e023432-fd70-4090-be61-1e146e086498)
```
Chip area for module '\picorv32a': 147712.918400
tns -711.59
wns -23.89

change strategy from AREA 0 to DELAY

Chip area for module '\picorv32a': 196832.528000
tns 0.00
wns 0.00

```
- set synth buffering & sizing
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_19_13_35](https://github.com/user-attachments/assets/7f659ac7-e8db-4e8f-a8e4-1d880f131eb5)

![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_19_20_37](https://github.com/user-attachments/assets/3c9b41be-3b7a-4838-a19e-b2b4b7ac4aeb)
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_19_23_12](https://github.com/user-attachments/assets/5841f2d1-412e-44f9-b9ff-eeb576bfa32b)
- Now we run synthesis again
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_19_33_22](https://github.com/user-attachments/assets/a46033f8-a6ef-4963-8e3e-c93f0f768db8)
- Our cell in merged.lef
- now we run floorplanning and placement again
- For floorplanning, run_floorplan does'nt work, so we use
```
init_floorplan
place_io
tap_decap_or
```
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_20_09_42](https://github.com/user-attachments/assets/a0669636-4ea6-4884-a779-805ef45258c4)

- run placement
```
run_placement
```
![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_20_13_11](https://github.com/user-attachments/assets/ddc21f9c-4d55-4198-a527-0d1724f52c0d)

![VirtualBox_vsdworkshop_nasscom_rohan_19_08_2024_20_11_44](https://github.com/user-attachments/assets/c601d0ae-345c-4def-80d4-2bd3d1bf3c35)

![rohang_placement_1](https://github.com/user-attachments/assets/7462d9dd-d203-4f93-83c0-45a232023fc6)
Fig: Our cell in placement
### Introduction to delay tables
![image](https://github.com/user-attachments/assets/73b8f7b7-d1a4-429b-927a-839468e0970a)

- Output Buffer capacitance not constant at different levels
  - Output load of one level input to another
  - Varying input transition at i/p of buffer
  - Varying output load at output of buffer
  - Hence varying delays
  - Hence we need delay table
  - Delay tables seperate for different gated/ logic devices
  - Here we tabularize buffer delay and characteristics

![image](https://github.com/user-attachments/assets/cae9122c-f962-47b6-9a53-b73a31e17a24)
![image](https://github.com/user-attachments/assets/c47e7bdc-554e-4fe6-b782-c67f427b8fdc)
  - delay at pt B = x9' + y15
  - delay at pt C = x9' + y15 , Hence we get slew = 0

  - But here if the level has different buffer sizes, we get slew
    - x9' + y15 & x9' + y17 ==> slew = y15-y17
- Hence we require identical buffer at same level
- and node driving same load at each level

- Now we deal with power in cts
  - ![image](https://github.com/user-attachments/assets/50ad3ca9-352f-48d6-a752-84791a98b135)
  - We do not need to propagate clock to inactive buffers

### running pre STA with ideal clocks using openSTA
![image](https://github.com/user-attachments/assets/f168834e-fed4-485e-a6d2-994c6a41fe15)
Fig: theta -> comb delay, T -> clk time, S-> setup time
![image](https://github.com/user-attachments/assets/21578bbb-1ea8-423e-a97f-965be22e9161)
![image](https://github.com/user-attachments/assets/d1686714-dbb0-40b0-a1cc-9584762658f8)


- creating stc file
  - ![my base sdc](https://github.com/user-attachments/assets/541fa5b2-a3d5-413d-8860-3c22381dc261)
```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 12.000
#set ::env(SYNTH_DRIVING_CELL) sky130_vsdinv
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 22.85
create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set IO_PCT 0.2
set input_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"


set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]
#set rst_indx [lsearch [all_inputs] [get_port resetn]]
set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]
#set all_inputs_wo_clk_rst [lreplace [all inputs_wo_clk $rst_indx $rst_indx]
set all_inputs_wo_clk_rst $all_inputs_wo_clk


#correct resetn
set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

# TODO set this as parameter
set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load $cap_load [all_outputs]

```
  - ![pre_sta](https://github.com/user-attachments/assets/29b0146f-72bd-4514-9b30-81ac4177ba38)
Fig: Pre STA config
```
set cmd units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um
read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/19-08_14-31/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns

```
  - ![slack22](https://github.com/user-attachments/assets/52827eed-7253-4192-b5da-26299e31d008)
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_00_20_16](https://github.com/user-attachments/assets/6079435b-6dc2-4d3f-9a4e-12bf93addf39)

Fig: Slack after STA
- To improve slack
  - Decrease max fanout
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_00_25_18](https://github.com/user-attachments/assets/f034444b-977f-4b6e-808b-fffdb3d326e4)
  - Replace cells with higher delays
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_00_49_59](https://github.com/user-attachments/assets/fbb6ee45-8db2-4658-82f1-ad3dc94774bc)
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_06_56_21](https://github.com/user-attachments/assets/6fa325bd-9468-4433-a4ab-6a2032433add)
  - Slack after decreased
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_06_56_52](https://github.com/user-attachments/assets/e092622d-4f39-4f47-a975-d0b28f6dcd20)
  - Replace more
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_07_00_53](https://github.com/user-attachments/assets/a06a0bd3-93d4-486a-b894-62bb051434c5)
  - Slack further reduced to -2.68 (still in violation but we can fix that after cts as we replace ideal clock with actual one)
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_07_12_49](https://github.com/user-attachments/assets/d8c835c3-bf1e-43f0-84c1-5f7493874ee9)

### Run Clock tree synthesis
![image](https://github.com/user-attachments/assets/5056ef55-f4d8-4708-9e68-3d9a3c208823)
Fig: clock needs to be propagated
![image](https://github.com/user-attachments/assets/e9aedea5-f928-4c1c-88c9-0577efda03f0)
Fig: example tree
![image](https://github.com/user-attachments/assets/5f8328a3-1fa7-478a-b865-0cee0f2225c8)
Fig: skew ==> bad tree
![image](https://github.com/user-attachments/assets/28273809-1c93-4494-ac34-ffb296ad0d94)
- H algorithm
  - almost zero skew
  - Now theres huge amt of capacotances
    - signal integrety problem
    - Add repeters
    - ![image](https://github.com/user-attachments/assets/b93233db-10fe-447e-a578-3aaf620fb512)
  - another problem : crosstalk
    - ![image](https://github.com/user-attachments/assets/53ff0488-47fb-4c29-b758-6bde776b07ef)
    - ![image](https://github.com/user-attachments/assets/f3366aa7-4b43-40a5-acd4-90f60a37a4eb)
    - sheilding wire connected to vdd and gnd as these wires do not switch
    - ![image](https://github.com/user-attachments/assets/f4a99d09-5b86-4615-81a4-12fdf6d80556)
  - as we design clock tree for zero skew, due to cross talk, delta delay and hence skew increases
    - thus as buffer inc, skew inc
  - ideally we should sheild all critical and clk nets seince we cannot shield everything due to routing constraints.
 
- Now we run cts
```
run_cts
```

![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_08_13_59](https://github.com/user-attachments/assets/3327fcf1-537b-4164-85db-519ea07d4bad)
![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_08_15_07](https://github.com/user-attachments/assets/37742f1a-7f2f-48b7-b6c9-6999ba86b5fb)
Fig: cts done, slack met
![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_12_48_46](https://github.com/user-attachments/assets/69f824be-fe76-495c-9e75-adb2d9bfff3c)
Fig: post cts layout

### Timing analysis with real clock using openroad
##### setup timing analysis
![image](https://github.com/user-attachments/assets/7e7e9ea4-e932-407c-992a-1b765adc1920)
![image](https://github.com/user-attachments/assets/1eb6c4fa-0513-4ad4-aa79-782644fc0810)

![image](https://github.com/user-attachments/assets/430e92e5-e0ba-4ed4-bc00-f12120556a86)

##### hold timing analysis
![image](https://github.com/user-attachments/assets/e941fdee-c7e8-475a-99ef-8cefc55464ac)
![image](https://github.com/user-attachments/assets/20dcdc24-8d3d-4c67-a100-e243db872e75)
![image](https://github.com/user-attachments/assets/0363b477-ad41-4867-b0f2-961fd5f0d4d5)

![image](https://github.com/user-attachments/assets/92e720e8-ec3e-4da3-ba0b-72aa03c41973)

##### timing analysis
![image](https://github.com/user-attachments/assets/b0fc252e-e46a-4e34-b8c8-3700b63af41a)
![image](https://github.com/user-attachments/assets/490c39e4-1736-4750-a9ba-7855c1f3244c)
![image](https://github.com/user-attachments/assets/d4512597-f076-45c4-b4e5-99f833431403)

##### using openroad
![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_13_31_23](https://github.com/user-attachments/assets/5307ce8d-6603-463e-8377-d2a60c28aeec)

![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_13_42_43](https://github.com/user-attachments/assets/db7e51e4-eb0a-4355-95d3-db212db0cbc4)
Fig: 
![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_14_56_47](https://github.com/user-attachments/assets/9da93d80-2416-4bbf-85ff-4154dde9c5bd)
![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_14_56_47](https://github.com/user-attachments/assets/65d8a9e0-f1ee-4ac9-9250-f8d8908245fe)
Fig: commands
- Results
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_14_57_01](https://github.com/user-attachments/assets/5c3c50c8-d575-4bc6-9c49-7e60335f79d6)
    Fig: hold slack
  - ![VirtualBox_vsdworkshop_nasscom_rohan_20_08_2024_15_01_04](https://github.com/user-attachments/assets/ae63cbff-7dfb-444d-9179-e7423eba594c)
    Fig: setup slack
```

hold: -0.1354   slack (VIOLATED)
setup : 5.2541   slack (MET)

lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0

set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]


hold:  0.1407   slack (MET) 
setup : 5.2886   slack (MET)

% report_clock_skew -hold
Clock clk
Latency      CRPR       Skew
_38295_/CLK ^
   1.31
_37393_/CLK ^
   0.82      0.00       0.48

```
Now that our slack requirements are met, we can proceed to routing

##### code openroad
```
% openroad
OpenROAD 0.9.0 1415572a73
This program is licensed under the BSD-3 license. See the LICENSE file for details.
Components of this program may be licensed under more restrictive licenses which must be honored.
% read_lef /openLANE_flow/designs/picorv32a/runs/20-08_02-38/tmp/merged.lef
Notice 0: Reading LEF file:  /openLANE_flow/designs/picorv32a/runs/20-08_02-38/tmp/merged.lef
Notice 0:     Created 13 technology layers
Notice 0:     Created 25 technology vias
Notice 0:     Created 443 library cells
Notice 0: Finished LEF file:  /openLANE_flow/designs/picorv32a/runs/20-08_02-38/tmp/merged.lef
% read_def /openLANE_flow/designs/picorv32a/runs/20-08_02-38/results/cts/picorv32a.cts.def
Notice 0: 
Reading DEF file: /openLANE_flow/designs/picorv32a/runs/20-08_02-38/results/cts/picorv32a.cts.def
Notice 0: Design: picorv32a
Notice 0:     Created 409 pins.
Notice 0:     Created 29412 components and 168779 component-terminals.
Notice 0:     Created 21072 nets and 70765 connections.
Notice 0: Finished DEF file: /openLANE_flow/designs/picorv32a/runs/20-08_02-38/results/cts/picorv32a.cts.def
% write_db pico_cts1.db
% read_db pico_cts1.db
% read_verilog /openLANE_flow/designs/picorv32a/runs/20-08_02-38/results/synthesis/picorv32a.synthesis_cts.v
% read_liberty $::env(LIB_SYNTH_COMPLETE)
1
% link_design picorv32a
[WARNING ORD-1000] LEF master sky130_fd_sc_hd__tapvpwrvgnd_1 has no liberty cell.
% 

```
