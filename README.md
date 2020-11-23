# openlane_sky130
# repository for openlane workshop


# Introduction

A workshop on basic Physical Design was conducted by VLSI System design in order to impart the following knowledge to students and industry professionals alike:
1. The ability to build and configure their own SoCs.
2. Create own definitions of GPIO.
3. To understand different decision making processes.
 
The workshop was run over a period of 5 days with a day-wise coverage as given below:
Day 1: To study various components of RISC-V microprocessor based SoC and review RISC-V picoSoC.
Day 2: To understand importance of good vs bad floorplan and introduction to library cells using open-source tool.
Day 3: To design and characterize ,one library cell using open-source Layout tool and spice simulator.
Day 4: To do pre-layout static timing analysis and understand the importance of good clock tree.
Day 5: To understand full-chip integration steps and implement E31 RISCV design using open-source tool-chain.

The workshop was conducted under controlled environment with uniform access levels provided to each and every participant.

# Scope

The scope of the workshop is limited to the RAVEN SoC, of the open-source Picorv32 processor, designed by Clifford Wolf.
All licensed tools are out of coverage.

# Objective

The objective of this course was to familiarize the participants with the different aspects of the Physical Design Flow, such as, Synthesis, Floorplanning, Placement, CTS, Routing and STA, and, also to provide a viable open-source alternative to the commercial softwares used in the industry.

# Assumptions

   1. All the required tools are pre-installed.
   2. The tools have the necessary permissions for a successful execution.
   3. All inputs for each stage are available and sourced as per requirement.

# Timelines

The timeline of the workshop is as follows:
Categories	  |    Initiation Date/Time	 | Completion Date/Time
----------------------------------------------------------------
Day 01 Challenge 	| 17th November 2020	 |   18th November 2020
Day 02 Challenge  |	18th November 2020	 |   19th November 2020
Day 03 Challenge	| 19th November 2020	 |   20th November 2020
Day 04 Challenge	| 20th November 2020	 |   21st November 2020
Day 05 Challenge	| 21st November 2020	 |   22nd November 2020



# Comprehensive Technical Report
# [DAY 1 CHALLENGE:]
[Concepts Implemented:]

  Introduction to QFN-48 package, chips, pads, core, die, IP
  Introduction to RISC-V Architecture, picorv32 and picoSoC, RAVEN full chip and RAVEN SoC
  Introduction to open-source EDA Tools
  
[Task:]
  1. Check installations of the open source EDA tools.
  2. Clone git repository for lab work.
  3. Find area of Layout.
  4. Run synthesis using qflow.
  
[Tools Used:]
  1. Yosys
  2. STA
  3. qflow

[Methodology:]

  1. Check installations of the open source EDA tools
  
     a. Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal.
     b. Now type the command "yosys".
     c. The terminal will change to "yosys>".
     d. Exit from "Yosys" and type "which sta"
     e. Observe the path displayed for sta installation.
     f. Similarly run the gui for qflow.
     
  2. Clone git repository for lab work
  
     a. Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal.
     b. Type the following command in the current working directory:
        git clone https://github.com/kunalg123/vsdflow.git
     c. Successful cloning will yield the message "Resolving deltas: 100% (110/110), done.".
        ![I1](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY1%20D1SK4%20MCQ5.JPG)
     d. Now enter the vsdflow directory created in the above step and then run the below command:
        ./vsdflow spi_slave_design_details.csv
     e. On successful completion of run, list the files of "outdir_spi_slave" directory and then pipeline it to get the count of files. The first column of the output will           give the count of files out of which one is a directory.
        ls -ltr outdir_spi_slave | wc
        ![I2](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY1%20D1SK4%20MCQ6.JPG)
  3. Find area of Layout
  
     a. Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal.
     b. Type the below commands in the terminal:
        cd outdir_spi_slave
        qflow display spi_slave
     c. It will open 2 windows "layout1" and "tkcon".
     d. On "tkcon" window, type "box". This will display the area of the layout.
        ![I3](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY1%20D1SK4%20MCQ7.JPG)
 4. Run synthesis using qflow
 
    a. Click on VSD IAT, Go to "Lab Instances". Then under "Links", click on the "link" icon. Click bottom left, System tools > LXTerminal.
    b. Create a directory called my_picorv32 under vsdflow directory.
       cd vsdflow
       mkdir my_picorv32
    c. Change into my_picorv32 directory and further create three sub-directories: source, synthesis and layout.
       cd my_picorv32
       mkdir source synthesis layout
    d. Copy the picorv32 netlist file into the source directory and then run the qflow gui.
       cp ~/vsdflow/verilog/picorv32.v source/.
       qflow gui &
    e. Set the below options in gui and then click on "Set Stop":
       Technology = osu018
       Verilog source file : picorv32.v
       Verilog module : picorv32
    f. Then run labs till synthesis and then obtain the % ratio of flip flop/total logic.
       ![I4](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY1%20D1SK4%20MCQ8_2.JPG)

# [DAY 2 CHALLENGE:]
[Concepts Implemented:]

  Utilization factor, Aspect Ratio, Pre-placed cells, De-Coupling Capacitors, Power Planning, Pin and Logical Cell Blockage Placements
  Library Binding and Placement
  Cell Design and Characterization Flows
  General Timing Characterization Parameters
  
[Task:]
  1. Find area of the placed chip.
  
[Tools Used:]
  1. qflow

[Methodology:]

  1. Find area of the placed chip
  
     a. Run the placement stage by setting the necessary options and performing the pin groupings.
     b. Post completion of the placement stage, change to my_picorv32 folder and type the below command:
        qflow display picorv32 &
     c. This will open layout and tkcon window In the layout window, select whole chip using below steps:
        Take cursor to bottom left and left-click.
        Take cursor to top right and right-click.
        Press Shift+i
     d. This will select the whole layout Now in tkcon window, type "box".
     e. You will get the area of the chip in microns.
        ![I5](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY2%20D2SK4%20MCQ5.JPG)

# [DAY 3 CHALLENGE:]
[Concepts Implemented:]

  SPICE Deck creation and, static and dynamic simulation for inverter, switching threshold
  Stick Diagram, Euler's path, abstract layouts
  Fn dimension derivation, layouts, scripting
  CMOS Fabrication Process
  
[Task:]
  1. Clone git repository for lab work.
  2. Obtain the widths of the CMOS transistors.
  3. Obtain DC Transfer characteristics for different transistor widths and find switching threshold.
  4. Obtain Transient analysis and calculate the rise time.
  5. Obtain pulsewidth from transient analysis.
  6. Analysis of Layout and obtain area of design.
  7. Obtain intersection of rising and falling waveform.
  
[Tools Used:]
  1. NGSPICE
  2. Magic
  3. leafpad

[Methodology:]

  1. Clone git repository for lab work
  
     a. Go to labs and open terminal and type the below command
        git clone https://github.com/kunalg123/ngspice_labs.git
     b. This will create a new folder called "ngspice_labs" in the current location.
  
  2. Obtain the widths of the CMOS transistors
  
     a. Open the terminal and change directory to "ngspice_labs".
     b. Display the inv.tran file.
        cat inv.spice
     c. Obtain the widths of the PMOS and NMOS transistors.
     d. From the above widths obtain the Wp/Wn ratio.
        ![I6](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK1%20MCQ5.JPG)
  
  3. Obtain DC Transfer characteristics for different transistor widths and find switching threshold
  
     a. Go to labs and open terminal. Change directory to "ngspice_labs" and run the below commands:
        ngspice inv.spice
     b. In the newly opened terminal, as a result of the above command, run the below commands:
        run
        setplot dc1
        plot out in
     c. This will open a plot with CMOS VTC and Blue 45 degree line.
     d. Click on the intersection point of the VTC and the line and note the value of X0.
     e. Now close the windows and in the terminal, edit the width of the PMOS device to 0.75u and rerun the above steps to obtain new X0.
        ![I7](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK1%20MCQ10.JPG)
     f. You will observe the shift in the switching threshold (X0) values.
  
  4. Obtain Transient analysis and calculate the rise time
  
     a. Go to labs, open terminal. Change directory to "ngspice_labs".
     b. Open file called "inv_tran.spice" using below command. Edit the PMOS width to 0.75u. Then save and close:
        leafpad inv_tran.spice
     c. Run the below command:
        ngspice inv.spice
     d. In the newly opened terminal, as a result of the above command, run the below commands:
        run
        setplot tran1
        plot out in
     e. Calculate the rise delay.
        ![I8](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK1%20MCQ11.JPG)
   
  5. Obtain pulsewidth from transient analysis
  
     a. Go to labs, open terminal. Change directory to "ngspice_labs".
     b. Run the below command:
        ngspice fn_prelayout.spice
     d. In the newly opened terminal, as a result of the above command, run the below commands:
        run
        setplot tran1
        plot out 1.25
     e. Calculate the value of X0 at the intersection of the middle rising waveform and blue line.
     f. Calculate the value of X0 at the intersection of horizontal blue line and middle falling waveform.
     g. Obtain the pulsewidth by calculating the difference between the X0 values of steps e and f.
        ![I9](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK2%20MCQ3.JPG)
  
  6. Analysis of Layout and obtain area of design
  
     a. Go to labs, open terminal. Change directory to "ngspice_labs".
     b. Run the below command:
        magic -T min2.tech
     d. It will open Magic layout and tkcon windows.
     e. In the tkcon terminal, run the below commands:
        source draw_fn.tcl
     e. Find the number of nsubstrate contacts and polysilicon strips.
        ![I10](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK3%20MCQ3.JPG)
     f. Close the windows and at the terminal, type the below command:
        magic -T min2.tech fn_postlayout.mag &
     g. Find the area of the design.
        ![I11](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY3%20D3SK3%20MCQ4.JPG)
  
  7. Obtain intersection of rising and falling waveform
  
     a. Go to labs, open terminal. Change directory to "ngspice_labs", type the below command:
        magic -T min2.tech fn_postlayout.mag &
     b. Follow the steps as mentioned in lecture of D3SK3 - Lesson 4.
     c. Find the value of X0 at intersection rising & falling waveform and intersection of horizontal blue line.
  

# [DAY 4 CHALLENGE:]
[Concepts Implemented:]

  Timing modelling using delay tables
  Timing analysis with ideal clocks - setup, jitter and uncertainity
  Clock Tree Synthesis and Signal Integrity - H-Tree Algorithm, Cross-talk and Net Shielding
  Timing Analysis with real clocks - setup and hold
  
[Task:]
  1. Clone git repository for lab work.
  2. Find load and rise delay for different load values, different slew parameters.
  3. Read values of different delay tables.
  4. Create SDC and conf files and perform sta. 
  5. Obtain different parameters from the reports.
  
[Tools Used:]
  1. leafpad
  2. sta
  3. NGSPICE

[Methodology:]

  1. Clone git repository for lab work
  
     a. Go to labs and open terminal and type the below command
        git clone https://github.com/kunalg123/ngspice_labs.git
     b. This will create a new folder called "ngspice_labs" in the current location.
  
  2. Find load and rise delay for different load values, different slew parameters
  
     a. Open the terminal and change directory to "ngspice_labs".
     b. Display the inv.tran file.
        cat inv.spice
     c. Obtain the input rise slew and fall slew.
     d. Run the below command in the terminal:
        ngspice inv_tran.spice
     e. Obtain the output load and rise delay.
     f. Modify to output load to 20fF in inv_tran.spice. Run ngspice and obtain the new values.
     g. Close the windows. Open below file using "leafpad" or "less" or "vim":
        /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
     h. Obtain the following values from the file:
        slew_upper_threshold_pct_fall, output_threshold_pct_rise.
        ![I12](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY4%20D4SK2%20MCQ7.JPG)
  
  3. Read values of different delay tables
  
     a. Open the terminal and change directory to "ngspice_labs".
     b. Open below file using "leafpad" or "less" or "vim":
        /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
     c. Look for line number 43 and find out what are the 2 variables of "delay_template_5x5".
     d. Look for line number 2943 and find out the delay table below line number 2943 is for which cell.
     e. Look for line number 2983 and find out which delay template is used for INVX1.
        ![I13](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY4%20D4SK2%20MCQ10.JPG)
  
  4. Create SDC and conf files and perform sta
  
     a. Open the terminal and change directory to "my_picorv32".
     b. Create picorv32.sdc file in leafpad and type the following commands in it and then save and close the file:
        create_clock -name clk -period 2.5 -waveform {0 1.25} [get_ports clk]
     c. Create "prelayout_sta.conf" file in leafpad and type the following commands in it and then save and close the file:
        read_liberty /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib
        read_verilog synthesis/picorv32.rtlnopwr.v
        link_design picorv32
        read_sdc picorv32.sdc
        report_checks
     d. Run the below command and note the slack:
        sta prelayout_sta.conf
        ![I14](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY4%20D4SK2%20MCQ11.JPG)
  
  5. Obtain different parameters from the reports.
  
     a. In the sta terminal obtained from task 4, type below command:
        report_checks -digits 4
     b. Obtain the following values from this report:
        data arrival time, data required time.
     c. Run the following commands at the sta terminal:
        set_propagated_clock [all_clocks]
        report_checks
     d. Obtain slack value after clock propagation, launch clock network delay, capture clock network delay.
     e. Type below command in sta terminal:
        report_checks -path_delay min -digits 4
     f. Find out library hold time and hold slack
        ![I15](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY4%20D4SK4%20MCQ5.JPG)
  

# [DAY 5 CHALLENGE:]
[Concepts Implemented:]

  Routing and DRCs - Lee's Maze Algorithm
  Introduction to SPEF - Different Representations of Parasitics
  PnR Tutorials
  
[Task:]
  1. Obtain Prelayout and Postlayout frequencies.
  
[Tools Used:]
  1. qflow
  2. leafpad

[Methodology:]

  1. Obtain Pre-layout and Post-layout frequencies
  
     a. Open Day 5 labs. Open the terminal and type the following commands:
        cd vsdflow/my_picorv32
        qflow route picorv32
        qflow sta picorv32
        qflow backanno picorv32
        leafpad log/sta.log
     b. Obtain Pre-layout frequency
        ![I16](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY5%20D5SK2%20MCQ1.JPG)
     c. Obtain Post-layout frequency and calculate the drop:
        log/post_sta.log
        ![I17](https://github.com/renu883/openlane_sky130/blob/main/Images/DAY5%20D5SK2%20MCQ2.JPG)

# Conclusion

We were able to verify the correctness of the installations. We were also able to successfully execute the PD flow, obtain different parameters and obtain the different voltage characteristics.

# Appendix (Softwares Used)

Software  | Description
------------------------
yosys | Yosys is a framework for Verilog RTL synthesis. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains. Yosys can be adapted to perform any synthesis job by combining the existing passes (algorithms) using synthesis scripts and adding additional passes as needed by extending the Yosys C++ code base.

qflow | Qflow is a complete tool chain for synthesizing digital circuits starting from verilog source and ending in physical layout for a specific target fabrication process.

sta | Open source tool for static timing analysis

NGSPICE | ngspice is the open source spice simulator for electric and electronic circuits.

Magic | Magic is a venerable VLSI layout tool, written in the 1980's at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl.

leafpad | Leafpad is an open source text editor for Linux, BSD, and Maemo. Created with the focus of being a lightweight text editor with minimal dependencies, it is designed to be simple and easy-to-compile.

  
  
