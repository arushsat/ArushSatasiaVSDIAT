# ArushSatasiaVSDIAT Terminal All Days

# Day 1 - getting to run_synthesis

open new regular terminal (add patches):

bash <(curl -s https://raw.githubusercontent.com/ZimengXiong/bASICs-openlane-apple-silicon-vm/refs/heads/main/patch-2/patch-2.sh)


go to openalane launcher terminal -

./flow.tcl -interactive

package require openlane

prep -design designs/ci/picorv32a

run_synthesis



<img width="1283" height="752" alt="Screenshot 2025-07-16 at 8 54 41 PM" src="https://github.com/user-attachments/assets/9555e909-82e4-4b86-8245-9c44d4c14151" />



# Floor planning / floor placement aka Day 2:

## Floor planning

(still in openlane launcher terminal)

run_floorplan



stay there and run (magic -T $env(PDK_ROOT)/$env(PDK)/libs.tech/magic/$env(PDK).tech lef read $env(RUN_DIR)/tmp/merged.nom.lef def read $env(RUN_DIR)/results/floorplan/picorv32.def &
) or open new OPENLANE LAUNCHER terminal:

cd designs/ci/picorv32a/runs/RUN_2025.07.20_21.02.52/results/floorplan

magic -T /home/beaver/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def

This is what you should see:

<img width="1272" height="657" alt="Screenshot 2025-07-20 at 4 59 37 PM" src="https://github.com/user-attachments/assets/293b0c46-db92-4bf9-9c60-97bf099e3fd1" />

## Placement:

go back to first openlane launcher terminal

run_placement

magic -T $env(PDK_ROOT)/$env(PDK)/libs.tech/magic/$env(PDK).tech lef read $env(RUN_DIR)/tmp/merged.nom.lef def read $env(RUN_DIR)/results/placement/picorv32.def &

This is what you should see:

<img width="1278" height="660" alt="Screenshot 2025-07-20 at 4 58 14 PM" src="https://github.com/user-attachments/assets/53ebdb71-df7f-4d65-abad-e6498e18c5fc" />


# Day 3

## Making changes in the openlane flow
heres an example of how to change the pin configurations. Currently the pins are equidistant.

open new normal terminal:
cd Desktop/work/tools/openlane_working_dir/openlane/configuration
less floorplan.tcl
<img width="847" height="580" alt="Screenshot 2025-07-20 at 5 42 58 PM" src="https://github.com/user-attachments/assets/6050bbdd-fcf0-4fa3-a537-b9bd697c0c0b" />

Now we will choose which variable we want to change, so in this case it is ::env(FP_IO_MODE) for the pin configuration.

so now that we have the variable, we go to the terminal where we ran run_floorplan.

paste and run:

set ::env(FP_IO_MODE) 2

then we will have to run_floorplan again, and run the same magic command as above to view it in magic. 

we will then see that the pins are no longer equidistant and they are stacked:

<img width="970" height="636" alt="Screenshot 2025-07-20 at 5 48 55 PM" src="https://github.com/user-attachments/assets/e773498a-ee90-400c-a95d-dc2f23cea01f" />

## Getting and viewing standard cell design

open new terminal

cd Desktop/work/tools/openlane_working_dir/openlane

git clone https://github.com/nickson-jose/vsdstdcelldesign.git

open a launcher:

cd vsdstdcelldesign

magic -T sky130A.tech sky130_inv.mag &

You should see this:

<img width="1276" height="731" alt="Screenshot 2025-07-20 at 7 53 19 PM" src="https://github.com/user-attachments/assets/4d9b82d5-6d3f-46a9-bccb-bc632f50a31a" />



