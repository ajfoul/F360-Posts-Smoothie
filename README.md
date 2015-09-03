# F360-Posts-Smoothie
Smoothieware laser post processor for Fusion360

Includes two gcode files based on the same part:

1. "rev-38643-modified.g" from revision 38643 of post provided by Autodesk with my modifications to make it work on my Smoothie driven K40 laser cutter.

2. "rev-39203.g" from revision 39203 of post by Autodesk as-is

Update 09.03.15:

Uploaded file smoothie-WLPC-AUG15.cps which now works with F360's WLPC (waterjet/laser/plasma cutter) CAM feature.

To use this post you need to put it in either post directory (generic or personal) and enable WLPC CAM in F360 by going to Prefrences>Preview.

You will also need to change a few of default settings each time you create an operation:

1. Select "Laser Cutting" under Type in the Tool tab. Also set an appropriate Kerf. I use 0.7mm on my machine for most stock, but each machine will be different and you may need to tweak this to get the most accurate cut for your machine and particular stock.
2. Select "Center" for Sideways Compensation in the Passes tab.
3. Disable (uncheck) "Lead-in (Entry)" and "Lead-out (Exit)" in the Linking tab.

Setting the Sideways Compensation to center disables "in-controller compensation" which Smoothie does not currently support.  You will get a warning on each operation when you do this, but you should still get usable code.  The Autodesk engineer who has been helping me get this post working is also implementing "in-computer compensation" for the September 2015 F360 update.  That should resolve this issue by having F360 do the compensation, as the name implies, on your computer which will result in better cuts.

The Smoothie post assumes that, if you have a laser PSU with seperate inputs for intensity and fire, you have set up a switch in config that looks something like the snippet below. Please note that this is for a Azteeg X5 mini board and the pin assignments might be different for the board you are using.

```
# Laser module configuration
laser_module_enable                          true            # Whether to activate the laser module at all. All configuration is ignored if false.
laser_module_pin                             1.23             # pin will be PWMed to control the laser 
laser_module_max_power                       1.0              # this is the maximum duty cycle that will be applied to the laser
laser_module_tickle_power                    0.0              # this duty cycle for travel moves to keep the laser active without actually burning

laser_module_pwm_period                      20               # sets the pwm frequency as the period in microseconds

switch.laserfire.enable                      true             #
switch.laserfire.output_pin                  0.26!^           # connect to laser PSU fire (!^ if to active low, !v if to active high)
switch.laserfire.output_type                 digital          #
switch.laserfire.input_on_command            M3               # fire laser
switch.laserfire.input_off_command           M5               # laser off
```
