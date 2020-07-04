# PYCO Image Colorspace Converter

Quickly switch colorspaces and file format for your textures, hdris, ...

![Main](screens/visu_script_global_wide.jpg)

!!! success "Get the app"
    :material-download: Download the app here: <https://gum.co/pycocs>

## :material-information-outline: About
This utility is targeted at VFX/Animation artists for use in converting input images to a designated target 
color space. It includes export options such as file format, bit depth, and others.

The app only works with 2d images for now. 

!!! bug "Known limitations & bugs"

    * Performance can become very bad with ACES ODTs.
    * Running the app as administrator on Windows will disable drag & drop
    
## :material-account-group: CONTRIBUTORS

**Development made possible thaks to**

- <a href=https://www.colour-science.org/> ColorScience Package </a>
- <a href=https://github.com/fredrikaverpil/oiio-python> Fredrik Averpil's and Sidney Guenther's work </a>
- <a href=https://materialdesignicons.com> Material Design Icons </a>
- <a href=https://sites.google.com/site/openimageio/home> OpenImage IO </a>

**Special Thanks to:**

- Documentation revision:
 <a href=https://www.jorgenhdri.com> Jørgen Herland </a>, 
 <a href=https://www.oddvisionary.studio/> kn9 </a>, 
 <a href=https://www.ceridwenproductions.com/> Douglas Bischoff </a> 

- Beta testing:
 <a href=https://mrlixm.github.io/PYCO/standalone/ColorspaceConvert/home/> Muhammed Hamed </a>,
 <a href=https://mrlixm.github.io/PYCO/standalone/ColorspaceConvert/home/> Valentin Nicolini  </a>,
 <a href=https://www.jorgenhdri.com> Jørgen Herland </a>,
 <a href=https://www.ceridwenproductions.com/> Douglas Bischoff </a>,  
 <a href=https://chrisbrejon.com/> Chris Brejon </a>
 
## :material-update: Upcoming Features

Some of these are simply ideas that might not never be realised.

!!! note ""

    - .tx Output
    - mipmapping for output support
    - RGB single color-converter
    - Demoisaicing RAW files
    - Image primaries plotting on CIE Diagram
    - Options to create a scaled version version of the output (4k to 2k for exemple)
    - Precise manually the transferfunction/primaries/whitepoint instead of using the IDT