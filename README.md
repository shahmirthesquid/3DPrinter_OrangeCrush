# 3DPrinter_OrangeCrush
Fully custom 3D printer built off the original V1 ender 3 frame

![image](front%20pic%2020241005_152819.jpg)


## Start G-Code

```
M117 Getting the bed up to temp!
M140 S{material_bed_temperature_layer_0}      ; Set Heat Bed temperature
M104 S170; Set Extruder temp to 170
M190 S{material_bed_temperature_layer_0}      ; Wait for Heat Bed temperature

; Ender 3 Custom Start G-code
G92 E0 ; Reset Extruder
M117 Homing axes
G28 ; Home all axes
G29 ; Probe Bl Touch
M106 P1 S255; Set mobo fan to max
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
M104 S{material_print_temperature_layer_0}
M109 S{material_print_temperature_layer_0}
M117 Purging

G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
M117 Printing...
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
```

## End G-Code

```
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positionning

G1 X0 Y{machine_depth} ;Present print
;G1 E-10 F1200 ;Retract filament
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

M84 X Y E ;Disable all steppers but Z
```

