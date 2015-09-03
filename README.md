# F360-Posts-Smoothie
Smoothieware laser post processor for Fusion360

Includes two gcode files based on the same part:

1.) "rev-38643-modified.g" from revision 38643 of post provided by Autodesk with my modifications to make it work on my Smoothie driven K40 laser cutter.

2.) "rev-39203.g" from revision 39203 of post by Autodesk as-is

Update 09.03.15:

Uploaded file smoothie-WLPC-AUG15.cps which now works with F360's WLPC (waterjet/laser/plasma cutter) CAM feature.

To use this post you need to put it in either post directory (generic or personal) and enable WLPC CAM in F360 by going to Prefrences>Preview.

You will also need to change a few of default settings each time you create an operation:

1.) Select "Laser Cutting" under Type in the Tool tab. Also set an appropriate Kerf. I use 0.7mm on my machine for most stock, but each machine will be different and you may need to tweak this to get the most accurate cut for your machine and particular stock.
2.) Select "Center" for Sideways Compensation in the Passes tab.
3.) Disable (uncheck) "Lead-in (Entry)" and "Lead-out (Exit)" in the Linking tab.

Setting the Sideways Compensation to center disables "in-controller compensation" which Smoothie does not currently support.  You will get a warning on each operation when you do this, but you should still get usable code.  The Autodesk engineer who has been helping me get this post working is also implementing "in-computer compensation" for the September 2015 F360 update.  That should resolve this issue by having F360 do the compensation, as the name implies, on your computer which will result in better cuts.