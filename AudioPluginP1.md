Note that for the tutorial, we want MIDI input and output so that’s why we do step #4

## Steps Taken
1. In Projucer click File > New Project
2. Give it a name
3. Check VST3 (and AU)
4. Check “Plug-in wants midi input and Plug-in produces midi output”
5. Click the “Save and Open in IDE button”

From here XCode opens

## Set up plug-in debugging

We can configure the host to enable step-through debugging of your plugin. To do this:

1. Go to your plug-in project in Xcode, click Product > Scheme > Edit Scheme
2. Under Run, from the Executable dropdown select Other... and locate the Plugin Host.app binary. 
3. Make sure Debug executable is ticked.

Now when you build and run your plugin within Xcode it will automatically launch the host, and when your plug-in is loaded inside the host you can set breakpoints and do step-through debugging.

## File Structure for a JUCE Plugin

A newly-created audio plug-in project contains two main classes"

* **PluginProcessor:** handles the audio and MIDI IO and processing logic
* **PluginEditor:** handles any on screen GUI controls or visualisations

When passing information between these two it is best to consider the processor as the parent of the editor. There is only one plug-in processor whereas you can create multiple editors.

Each editor has a reference to the processor such that it can edit or access information and parameters from the audio thread. It is the editor’s job to set and get information on this processor thread and not the other way around.

### PluginProcessor.cpp

The main function we will be editing in the PluginProcessor.cpp file is the `processBlock()` method.

* This receives and produces both audio and MIDI data to the plug-in output.

