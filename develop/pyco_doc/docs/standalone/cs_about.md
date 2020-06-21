# About
This tool target an utilisation in the vfx/animation domain by providing options for converting input image into a 
desired colorspace with different export options such as the format, bitdepth, and such...

## Inputs and Outputs

!!! info "Lists of Inputs formats supported"
    
    - .exr
    - .png
    - .jpg
    - .jpeg
    - .tiff
    - .hdr

!!! question "What is the behavior of the export checkable circles ?"

    - **Export in a new folder:** The file will be placed in a new folder named "ACEScg" located at the same
     location of the original file. 
    - **Export at the same location:** a new file prefixed with the target colorspace or the ODT/Tf will be created.

!!! danger

    All outputs are cropped to RGBA (if alpha supported) channels.
     
    So if you input multi-channel exrs and output exrs, you will lose all your other channels.
    
## ODT/Transfer Functions

!!! info "Availability"

    - The ODT / Transfer Function dropdown is only available when the Output format is set to a integer format (.jpg or .png) 
    - ACES ODT (*prefixed with (ACES)*) are only available when the Target ColorSpace is set to **ACEScg** 

    
    
