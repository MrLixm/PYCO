# :material-collapse-all-outline: Features


Structure:
```bash
"pathto/pointerGamutCLI.exe" command arguments [Options]
```

## :material-view-list-outline: Command list

### :material-numeric-1-box: createpgmap command

Create a map that show out of PG pixels as explain in the Home page.

```bash
"pathto/pointerGamutCLI.exe" createpgmap INPUT_FILE_PATH OUTPUT_FILE_PATH [Options]
```

**Arguments:**

INPUT_FILE_PATH is the path to the image to generate the map from

OUTPUT_FILE_PATH is the desired path (with the filename.ext) to the map that is going to be generated

**Options:(which are all optional except the colorspace one)**

#### `--colorspace=string` 
colorspace primaries of the file

!!!info ""

    This argument should specify the colorspace primaries of your file.
    In case you also use the `--linearize` option it also precise which transfer function
    is used on your file.
    
    Examples of colorspaces available:
    
    - ACEScg, sRGB, BT709, ADOBE_WIDE_GAMUT, ADOBE_RGB_1998, ACES2065-1
    
    The whole list is available here: <https://colour.readthedocs.io/en/develop/generated/colour.RGB_COLOURSPACES.html#colour.RGB_COLOURSPACES>


####`--linearize` 
linearized the input based on the colorspace specified. 

!!! info ""

    **The tool awaits for linear data**, if you input an image with a transfer function applied, the linearize option 
    will invert this transfer function to get linear data (the transfer function is determined by the colorspace
    argument you submitted).
    This is an internal operation that **doesn't affect the original file**.
    
    For example if you input a .jpg/.png you should use this option.

#### `--out_map_type=string` 
Choose the type of map to output (heat, add) 

!!! info ""

    *[default=heat]*

    **Heat** will output a black map with pixels gamut that are not in the PG with a red color
    
    **Add** will just adds the above map onto the original file (that has been multiplied by 0.65 so this is 
    normal if it looks darker) 

#### `--tolerance=number` 
How far from the pointer gamut you authorize the pixel values to be. 

!!! info ""

    *[default=0]*
    
    The range of this parameters is 0-1, but keep it very low. Something like is 0.08 is a good value if you want 
    some margin.
    
#### `--layername=string` 
Which layer you want to analyse, no matter if it is a multi-layer or a multi-part exr just enter
the name of the layer you are interested (for this tool the albedo)


#### ``--help`` 
display the help


### :material-numeric-2-box: querylayers command

Display all the channel of all the layer in the file (useful for multi-layers exr)

Return the layer index + the channels it holds. You can get 2 result:

- "multi-layer" exr contains only one "layer"(subimage) but multiples channel. 

- multi-part exr contains multiples subimages with each can contains multiple channels too

If both case just get the name of the albedo channel for creating the pg map. 


```bash
"pathto/pointerGamutCLI.exe" querylayers FILE_PATH
```

**Arguments:**

FILE_PATH is the path of the file to query info from


## :material-image-move: Inputs and Outputs

!!! success ""

    :material-import: **List of Input formats supported**  
    
    - .exr
    - .png
    - .jpg
    - .jpeg
    - .tiff
    - .hdr
    - .tx
    
    !!! warning
        Single-channel maps are not supported.
        
        
    
!!! success ""
    
    :material-export: **Output**
    
    This app has been made to output 8bit int jpg, trying to output an other format is possible but might not work.
    
