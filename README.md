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
