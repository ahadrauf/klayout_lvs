# klayout_lvs
A KLayout Layout-Versus-Schematic (LVS) debugger

# Installation
## Requirements
1. KLayout
2. All my scripts were written with Python 3.5. Most of the things should still work with Python 2, but I give no guarantees (plus, you may get the annoying parentheses on print statements since they'll not functions in Python 2).
3. Numpy. I used version 1.15.3, but my commands are pretty basic so I'm pretty sure previous versions should work as well.

There are (at least on Windows) two places where you can find KLayout scripting information.
1. The local Python scripting folder - on my laptop, that's at C://Users/Ahad Rauf/KLayout/pymacros. That's the folder where you should clone this repository. It's also the folder that gets displayed when you open KLayout > Macros (one of the headers) > Macro Development > Python (on the left side, next to RBA and DRC) > hover over [Local]
2. The actual place where KLayout is installed on your laptop - for me, that's at C://Users/Ahad Rauf/AppData/Roaming/KLayout. AppData is a hidden folder, so you might need to enable hidden folder viewing on your Windows file system. To find this folder generically, run the Python script below:
```python
import sys
print(sys.path)
```
This will display the list of folder locations that KLayout searches when looking for the `pya` directory. You should see one folder with lots of DLL's, like klayout_pya.dll. That's the one.

The annoying thing about trying to learn KLayout scripting is that it's pretty horribly documented - there are pages explaining basic stuff, but all the source code is in .dll files, which you don't often find convenient readers for. One good reader is Dependency Walker (http://www.dependencywalker.com/), which you can use to analyze the project layout.

A more convenient way, in practice, was to just call Python's `help()` method inside a Python KLayout script. The script went something like this:
```python
import pya
app = pya.Application.instance()
help(app)
```
This script prints pya.Application's documentation to the console. I've copied the documentation for some of KLayout's common modules in the klayout_api folder, for your convenience.