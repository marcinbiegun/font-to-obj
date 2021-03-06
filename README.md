# FontMeshExporter

A script for Batch conversion of single font characters to extruded OBJ models.

It works fine with all kinds of unholy Unicode symbols.

![font-to-obj](https://raw.githubusercontent.com/marcinbiegun/font-to-obj/master/docs/font-to-obj.png)

## Dependencies

* Inkscape 0.92.2 for creating vectors from fonts
* Blender 2.8 for creating 3d models from vectors

## How to run it

Tested on MacOS.

1. Install Inkscape and Blender, put the .app files inside `/Applications` directory.
2. Write your characters inside `chars.txt` file.
3. Run `ruby run.rb`.
4. Receive OBJs in `obj` directory.

## How it works

1. The `single_char_template.svg` file contains a single large font character image. You can edit this file to change the font.

2. Inkscape is used to convert the font character in the `.svg` file to a vector object.

```bash
/Applications/Inkscape.app/Contents/Resources/bin/inkscape -z -D --file=~./svg/Ux5D0_font.svg --export-plain-svg=./svg/Ux5D0_vector.svg --export-text-to-path
```

3. Blender is used via `blender_svg_to_obj.py` script, to import the vector character, convert it a mesh, run some corrections and export it as an `.obj` file

```bash
/Applications/blender.app/Contents/MacOS/blender -b -P blender_svg_to_obj.py -- --svg_import './svg/Ux5D0_vector.svg' --save './obj/Ux5D0.obj'
```

4. The `run.rb` performs this operation for each character found in
   `chars.txt` file
