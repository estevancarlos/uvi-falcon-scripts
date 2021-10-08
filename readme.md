# Falcon UI Design Tutorial and Example

UVI Falcon is a sound design tool marketed as a "Hybrid Instrument". It offers 16 oscillators, 90+ effects, modulation sources, and MIDI processors with scripting. This includes the ability to design a user interface for custom scripted Falcon programs.

**About this tutorial**
I am an educator and technologist focused sound design and UI design. Some information in this tutorial may be incorrect and will be updated as I continue through this learning process. The tutorial assumes your broad knowledge with scripting and modest knowledge of graphic software.

## Lua language and API

Falcon uses Lua language and specifically the Lua 5.1. UVI's API is available here https://www.uvi.net/uviscript/index.html. It is a high level language, cross-platform, and often embedded to use in applications. Learn more here https://www.lua.org/manual/5.1/.

## The User Interface
The API supports user interface widgets such as knobs, sliders, buttons, audio meters, and more. These widgets have an default graphical representation and can also be customized.

### A default UI Widget
The construction of a knob requires the use of the knob class. It takes a series of parameters. You can observe below a local variable is created, `filterKnob`. A new knob widget is created and associated with the variable name.

This widget, and others, take the following parameters:
- string name - The name of the widget
- number def - Initial value
- number min - Minimum output value
- number max - Maximum output value
- bool integer - Integer or float output. True is an integer


```
local filterKnob = Knob("filterKnob", 0.8, 0.0, 10.0, true)
filterKnob.x = 50
filterKnob.y = 50
```

### Customizing the graphics of the widget

Some widgets offer the option of a custom user interface graphic. It requires the use of the `setStripImage` method. It takes two parameters. The first is the location of a graphic file. The second is the amount of "frames"  in the graphic. Observe that this requires the colon syntax.

`filterKnob:setStripImage("resources/min_knob_strip.png", 15)`

### Graphic Frames
I am using the term "frame" to describe each graphic state of a UI widget. UVI does not document any of this. As such I will use the term frame.

The `setStripImage` method is designed to load a graphic image that contains multiple frames of UI widget. For example, a button widget may contain an off state and an on state. This means a single graphic may contain two frames--the visual depiction of the on state and a separate frame for the off state. More complicated widgets can contain many frames. The second parameter `setStripImage` method is the amount of frames within the single graphic. This is why the method uses the term "strip". It's like a comic/animatiom strip.

### Creating Graphics
The graphic strip needs to be constructed vertically. This means each frame is positioned after each other going downward. Each frame needs to be the exact dimension. For example, if the first frame is 200x200px, then all others must conform to the same. Here are a few points:

- All frames are the same dimension
- There is no space between the frames. Leaving any pixel space will create jumpy UI animation
- Frames are positioned vertically, downward
- You have to specify the amount of frames. If done so incorrectly, the UI animation will not work
- Transparent PNGs are supported. This means you can layer graphics over each other.
