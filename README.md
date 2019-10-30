# klayout_lvs
A KLayout Layout-Versus-Schematic (LVS) debugger

# Installation
## Requirements
1. KLayout
2. All my scripts were written for Python 3.5 (since KLayout uses an internally compiled version of Python3.5, you're more or less stuck with this).
3. Numpy. I used version 1.15.3, but my commands are pretty basic so I'm pretty sure previous versions should work as well.
4. NetworkX: http://networkx.github.io/. I used this for my graph algorithms. You can install this using ```pip install networkx```.

Note that KLayout runs Python through its own internal installation of Python3.5. You can find this in its local setup. On my laptop, that's at C://Users/ahadr/AppData/Roaming/KLayout/lib/Python35.
Since installing old source code versions of Python can be difficult, you can actually just install NetworkX on whatever installation of Python you currently have (3.5+, I've used 3.8 successfully).
You can then copy the NetworkX files from your Python repository (for me, located at C:\Users\ahadr\AppData\Roaming\Python\Python37\site-packages) and the decorator class (for me, located at
C:\Program Files (x86)\Python37-32\Lib\site-packages), to the KLayout local folder for Python 3.5 mentioned above.

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

# Setting up a File to Run LVS
Layout versus Schematic works by first defining a schematic (like a circuit netlist, essentially a list of nets and polygons connected to those nets), and then
checking that the actual layout (i.e. wiring) doesn't short two nets together. You can denote a polygon's "net" via User Properties in KLayout: see below.
!(User Properties Tutorial)[./user_properties_image.png "User Properties Tutorial"]
Essentially, you denote a max of two properties:
* "NET": "net_name"
* "DIR": "SRC" or "SINK" (or you can leave this one out to imply "SINK")
Sources ("SRC") are reserved for pads or other regions where power/signals will be inputted, and the code checked that no two sources are shorted. Frankly, this
could also potentially just be removed assuming people assigned their net names correctly, but this was a check to make sure any auto-generated polygons
were properly placed on separate nets. Sinks ("SINK") is meant for everything else - the code doesn't give any errors if two sinks are connected, so if you're
confident in your net naming you can just omit the "DIR" key-value pair to make everything a "SINK".

You can edit User Properties manually by double clicking any polygon in KLayout (Editor). To date, I still haven't found a way to do it using our MATLAB KLayout
library, but this can be a project for future iterations.

## Miscellaneous
Here are some helpful resources I found while creating this repository:
1.  Installing custom keyboard shortcuts in KLayout: https://www.klayout.de/forum/discussion/4/how-to-install-custom-keyboard-shortcuts. In essence, you can go to File > Setup > Customize Menu. One of my top changes was setting Cntl+S so it actually saves the file.
2.  You can actually change the font of the code editor! Papyrus is nice :D
3.  