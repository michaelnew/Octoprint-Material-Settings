# OctoPrint-Material-Settings

This plugin allows you to change your bed and print temperatures from within Octoprint without having to reslice.

It will look for specific heating commands sent to the printer (`M104`, `M109`, `M190`, and `M140`) and replace them with values that you've set from within Octoprint.

## Installation

Open Octoprint's [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager)
and use **...from URL** with this:

    https://github.com/mikenew12/OctoPrint-Material-Settings/archive/master.zip

## Configuration

In `Settings` -> `Material Settings`, set the temperature values you'd like the plugin to look for and replace. For example, setting the `Bed Key Temperature` to `51` ˚C will cause the plugin to replace any `M190 S51` or `M140 S51` command with a new temperature that you've set in the plugin UI. Same principle for the hotend temperature. Trailing zeros should not cause problems if your gcode has commands like `M190 S51.00000`.

So if your GCode has this at the beginning:

    M140 S51
    M109 S201

And under the Matrial Settings tab you've set the bed temp to be 62 and the print temp to be 205 (say you're printing PLA), then as those commands are sent to the printer they will become `M140 S62` and `M109 S205`. You could then switch to ABS and change the bed temp to 100 and the print temp to 240 and print the obejct again without ever having to reslice.

Note that this will also work when setting temps in the GCode Scripts from within OctoPrint. So you can leave temperature commands out of your slicer's generated code entirely and use a gcode startup script to set them.

Any other temperature value will not be replaced, so you could, for example, have a warmup routing that heats the bed to 40 ˚C, auto-levels, wipes the nozzle, etc., and then has an `M190 S51` command that gets replaces with whatever temperature you've set in the plugin. The point of this plugin is to be able to adjust your bed and nozzle temperatures without reslicing so you can change materials or tweak your temps whenever you like.
