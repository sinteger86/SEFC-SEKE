# Configuration Section
The configuration is based on adding 2 files (in my case, as I used a RP2040Zero to drive the servo):

## Servo Board (RP2040Zero)
Filename: rp2040.cfg
Include position at printer.cfg: Any place.
Description: This file create the servo and led pins that are used by the macros

## Cutter macro
Filename: tip-cutter.cfg
Include position at printer.cfg: Before the mmu configuration
Description: This file contains the macros that will perform the filament purge and cut. 


## Example:
[include tip-cutter.cfg]
[include mmu/base/*.cfg]
[include mmu/optional/client_macros.cfg]
[include rp2040.cfg]
[include mainsail.cfg]

# Happy-Hare configuration:
on "mmu_macro_vars.cfg":
    variable_user_post_load_extension     : 'MCPURGE'	; Executed after default logic but before restoring toolhead position

on "mmu_parameters.cfg":
    post_form_tip_macro: MCCUTTIP			# Called immediately after tip forming

"Fake" tip forming:
variable_cooling_tube_position  : 30		; Start of cooling tube. DragonST:35, DragonHF:30, Mosquito:30, Revo:35, RapidoHF:27
variable_cooling_tube_length    : 1		; Movement length. DragonST:15, DragonHF:10, Mosquito:20, Revo:10, RapidoHF:10
variable_initial_cooling_speed  : 2.2		; Inital slow movement (mm/s) to solidify tip and cool string if formed
variable_final_cooling_speed    : 30		; Fast movement (mm/s) Too fast: tip deformation on eject, Too Slow: long string/no seperation
variable_cooling_moves          : 1		; Number of back and forth cooling moves to make (2-4 is a good start)
