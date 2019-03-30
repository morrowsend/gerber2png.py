# gerber2png

Originally forked from [dgnoner's work](https://github.com/dgonner/gerber2png.py).

### Converts Gerber files from KiCad to PNG files for Fab Modules 

For makers visiting a fablab that uses fabmodules for PCB manufacturing.
The toolchain is expecting you to use Cadsoft Eagle for your PCB designs.
Eagle has a png export that plays nice with the fabmodules png2rml.

Unfortunately, KiCad users a left stranded. This project hopes to help
those using it to generate the right files to mill your PCB with fabmodules.

Export your pcb design from KiCad to the industry standard Gerber format.
gerber2png then takes your gerber files and greates two png files from it.
One png is for milling the traces, the other one is for the holes and outline.

### CLI usage

For now, the script has to be in the same folder as the gerber files exported from KiCad with the configuration below. The project name has to be specified with `-i`. The other options are optional:

```
python gerber2png.py -h

Gerber2PNG.py ver. 2.1  march 2019

usage: gerber2png.py [-h] [--project_name PROJECT_NAME]
                     [--input_path INPUT_PATH] [--border_mm BORDER_MM]
                     [--ppi PPI] [--step STEP]

optional arguments:
  -h, --help            show this help message and exit
  --project_name PROJECT_NAME, -n PROJECT_NAME
                        Kicad Project Name
  --input_path INPUT_PATH, -i INPUT_PATH
                        Input Path
  --border_mm BORDER_MM, -b BORDER_MM
                        Border in mm
  --ppi PPI, -p PPI     ppi
  --step STEP, -s STEP  step
```

Example:

```
python gerber2png.py -n Example -i Example/

Gerber2PNG.py ver. 2.1  march 2019

Searching directory: Example/
Project name: Example
...
```

**WARNING**
As for now, filled zones (a common GND) or drills don't work that well.

#### KiCad Settings for Gerber export

Originally written for Build (2013-jul-07)-stable of Pcbnew. Checked for Kicad 5 in March 2019.

* Use the "Set the origin point for the grid" tool to set the origin in the lower left point of the pcb edge.
* Use the "Place the origin point for drill and place files" tools to to set the origin in the lower left point of the pcb edge.
* Open the Export dialog via File > Plot
* Plot format: Gerber
* Set the output directory, usually "plots/". Say yes to relative path.
* Mark the copper and mechanical layers you want to export. Usually F.Cu, B.Cu and Edge.Cuts.
* Enable "Use Auxilliary axis as origin"
* Enable "Use proper filename extensions"
* Press Plot to generate the gerber files.
* Next, press "Generate drill file".
* Set the output directory, usually "plots/". Say yes to relative path.
* Drill units: Inches.
* Zeros format: Keep zeros
* Drill map file format: Gerber
* Enable "Mirror y axis"
* Drill origin: Auxiliary axis
* Press Drill file to generate the drill file.