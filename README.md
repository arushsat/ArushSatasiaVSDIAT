# ArushSatasiaVSDIAT Terminal All Days

# Day 1 - getting to run_synthesis

new terminal- add patches-

bash <(curl -s https://raw.githubusercontent.com/ZimengXiong/bASICs-openlane-apple-silicon-vm/refs/heads/main/patch-2/patch-2.sh)


go to openalane launcher

./flow.tcl -interactive
package require openlane
prep -design designs/ci/picorv32a
run_synthesis



<img width="1283" height="752" alt="Screenshot 2025-07-16 at 8 54 41 PM" src="https://github.com/user-attachments/assets/9555e909-82e4-4b86-8245-9c44d4c14151" />



# Floor planning / floor placement aka Day 2:
(My VM quit running so I only have commands for this day)

run_floorplan

new terminal:
cd Desktop/work/tools/openlane_working_dir/openlane/designs/ci/picorv32a/runs/RUN_2025.07.20_21.02.52/results/floorplan

magic -T /home/beaver/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.def

for placement:

go back to launcher terminal
run_placement

to view in magic:

magic -T /home/beaver/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32.placement.def
