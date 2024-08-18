# VSD_NASSCOM_SoC_Design_Program

docker
pwd
ls -ltr
flow.tcl -interactive 
package require openlane 0.9
prep -design picorv32a
run_synthesis

task 1: Flop ratio = 1613/14876 = 0.10842968539930088733530518956709 = 10.84% 

run_floorplan

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &


run_placement

~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-08_03-33/results/placement$ magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

set ::env(FP_IO_MODE) 2
run_floorplan 
