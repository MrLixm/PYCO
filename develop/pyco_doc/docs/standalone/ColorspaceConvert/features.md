# :material-collapse-all-outline: Features

## :material-image-move: Inputs and Outputs

!!! success ""

    **List of Input formats supported**  
    
    - .exr
    - .png
    - .jpg
    - .jpeg
    - .tiff
    - .hdr
    
    !!! warning
        Single-channel exrs are not supported.

!!! success ""
    
    **List of Output formats supported**
    
    Format               | Bitdepth
        --------------- | -----
        .exr   | 16 Half, 32 Float
        .jpg   | 8 Int
        .png   | 8 Int, 16 Int

!!! question "What is the behaviour of the export checkable circles ?"

    - **Export in a new folder:** The file will be placed in a new folder named "ACEScg" located at the same
     location of the original file if no path is given.
     
        Else the output files will be placed in the given folder path.
     
    - **Export at the same location:** a new file prefixed with the target colorspace or the ODT/Tf will be created.

!!! danger

    All outputs are cropped to RGBA (if alpha supported) channels.
     
    So if you input multi-channel exrs and output exrs, you will lose all your other channels.

!!! warning "Compression"
    
    When choosing the compression amount remember that for jpg **100 means less compression** while it is the **inverse**
    for exrs.

!!! warning "Importing folders"
    When drag&dropping a folder, all the files inside it and its sub-directories will be added!
    
## :material-image-search: IDT

IDTs allow to specify to which colorspace your file primaries belongs too but also which transfer-function is applied.

!!! info "Conversion"

    If the Input colorspace is the same as the Output one, no conversion at all will happens. 
    
    So it doesn't matter your orignal file primaries, if you just want to switch file format for example you can just 
    use the same colorspace for IDT and Target Cs.*(ex: IDT: sRGB-Lin ; OutCs: sRGB/rec709)* 


​    
## :material-chart-bell-curve-cumulative: ODT/Transfer Functions

!!! info "Availability"

    - The ODT / Transfer Function dropdown is only available when the Output format is set to a integer format (.jpg or .png) 
    - ACES ODTs (*prefixed with (ACES)*) are only available when the Target ColorSpace is set to **ACEScg** 

## :material-animation-play: Converter

Depending on your export options and your input file size, the converting process can become very slow. 
Applying an ACES ODT is the slowest operation.

Colorspaces conversion are processed with a Bradford chromatic adaptation.

## :material-keyboard: Shortcuts

!!! info ""

    ++ctrl+a++ : Select all file in the list
    
    ++delete++ : remove a file (no undo)
    
    ++backspace++ :  remove a file (no undo)
    
    You can also use the directionnal arrow to navigate in the list and shift to select items.

## Logging

You can find the log file here: `yourdocumentspath/PYCO/ColorSpaceConverter/log_file.log`
You can also open it by clicking on the "log" Icon in the UI.