# klayout_lvs
A KLayout Layout-Versus-Schematic (LVS) debugger

# Installation
## Requirements
1. KLayout
2. All my scripts were written with Python 3.5. Most of the things should still work with Python 2, but I give no guarantees (plus, you may get the annoying parentheses on print statements since they'll not functions in Python 2).
3. Numpy. I used version 1.15.3, but my commands are pretty basic so I'm pretty sure previous versions should work as well.
4. NetworkX: http://networkx.github.io/. I used this for my graph algorithms. You can install this using ```pip install networkx```.

## Cloning this repository
There are (at least on Windows) two places where you can find KLayout scripting information.
1. The local Python scripting folder - on my laptop, that's at C://Users/Ahad Rauf/KLayout/pymacros. That's the folder where you should clone this repository. It's also the folder that gets displayed when you open KLayout > Macros (one of the headers) > Macro Development > Python (on the left side, next to RBA and DRC) > hover over [Local]
2. The actual place where KLayout is installed on your laptop - for me, that's at C://Users/Ahad Rauf/AppData/Roaming/KLayout. AppData is a hidden folder, so you might need to enable hidden folder viewing on your Windows file system. To find this folder generically, run the Python script below:
```python
import sys
print(sys.path)
```
This will display the list of folder locations that KLayout searches when looking for the `pya` directory. You should see one folder with lots of DLL's, like klayout_pya.dll. That's the one.

Alternatively, if you can't find either of these locations, you can just take the ```lvs.lym``` file and copy it as mentioned in setup step 4 below. 

## Running the script
Wherever you choose the clone this repository, you can run it using the standard method in KLayout for running macros:
1. Open your GDS file (in either KLayout Viewer or Editor, it doesn't matter)
2. Go to Macros > Macro Development. A window should pop up.
3. Go to the Python tab on the left side (it should be next to Ruby and DRC).
4. You should be able to find your script under whichever file location you placed it under. If you weren't able to find either of the file locations above, you can create a new script by clicking the '+' sign on the left side of the window. I recommend putting it under the Local Pymacros branch, unless you plan on sharing this program with others on the same computer.
5. Double click your script to open it up. You can then run it on the active GDS file (the last file whose KLayout window you accessed) by clicking the green Run arrow at the top of the window.
6. Watch it run!

# Reading the Code
You can find the KLayout API here: https://www.klayout.de/doc-qt4/code/index.html

## Miscellaneous
Here are some helpful resources I found while creating this repository:
1.  Installing custom keyboard shortcuts in KLayout: https://www.klayout.de/forum/discussion/4/how-to-install-custom-keyboard-shortcuts. In essence, you can go to File > Setup > Customize Menu. One of my top changes was setting Cntl+S so it actually saves the file.
2.  You can actually change the font of the code editor! Papyrus is nice :D
3.  