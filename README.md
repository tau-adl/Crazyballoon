# Crazyballoon
Crazyflie modification to airship using balloon. Mainly Instructions on Installation &amp; Usage.

# Mechanics and Electronics

Design files for both ECAD &amp; MCAD can be found on this <a href="https://github.com/tau-adl/crazybal-design-files"> repository </a>.
Assembly and more can be found in the final project paper in this repo

# Crazyfile Firmware

In order to fly the airship, a modified version of the firmware is needed.

## Instructions ##

The modified firmware, along with enviroment setup can be found on this <a href=""> repository </a>.</br>


### Compilation ###

Checkout the <b>Flight-tests</b> branch. and complie using: 

'''
Make clean
Make all PLATFORM=cf2b
'''

To flash the cf using the radio:

''' 
Make cload
'''

### setting parameters ###
