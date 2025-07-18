# ArushSatasiaVSDIAT Terminal All Days

Getting to the point at which we can run "run_synthesis":

./flow.tcl -interactive
package require openlane
prep -design designs/ci/picorv32a
run_synthesis


<img width="1283" height="752" alt="Screenshot 2025-07-16 at 8 54 41 PM" src="https://github.com/user-attachments/assets/9555e909-82e4-4b86-8245-9c44d4c14151" />



# Floor planning / floor placement aka Day 2:
(My VM quit running so I only have commands for this day)

Run this after running run_floorplan
magic -T /home/beaver/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def

for placement

run_placement

to view in magic:

magic -T /home/beaver/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.placement.def
