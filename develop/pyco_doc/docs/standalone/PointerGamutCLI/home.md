# Pointer's Gamut Checker CommandLineTool

!!! success "Get the app"

    :material-download: Download the app here: <https://gum.co/pgtool>


[*PG will be used as an acronym for Pointer's Gamut*]

!!! info ""

    This tool allow you to check if the gamut of pixels of a given image are in the 
    Pointer's Gamut or not.
    
    **Translation**: Check if your textures(diffuse reflectance i.e albedo only) are physically correct.

This is a command line tool, it means no interface to interact with. Please refer to the 
[startguide](startguide.md) for having an explanation of how to use it if you never used CLI(command line interface).

The outputted result is an image of the same size as the original with red pixel 
representing the out-of-gamut ones, and black for the one in the PG.

![Exemple](images/explorerExemple.png)

!!! question "What is the Pointer's Gamut ?"

    The Pointer’s gamut is (an approximation of) the gamut of real surface colors as can be seen by the human eye,
     based on the research by Michael R. Pointer (1980). What this means is that every color that can be reflected 
     by the surface of an object of any material is inside the Pointer’s gamut.
     
     Pointer’s gamut is defined for **diffuse reflection** (matte surface)
     
     -- from <https://www.tftcentral.co.uk/articles/pointers_gamut.htm>
     
     So what that it means for us 3d artist ? That using the PG you can tell if your albedo texture/aov is physically correct !
     
## :material-account-group: CONTRIBUTORS

**Development made possible thanks to**

- <a href=https://www.colour-science.org/> ColorScience Package </a>
- <a href=https://github.com/fredrikaverpil/oiio-python> Fredrik Averpil's and Sidney Guenther's work </a>
- <a href=https://materialdesignicons.com> Material Design Icons </a>
- <a href=https://sites.google.com/site/openimageio/home> OpenImage IO </a>
- <a href=https://www.docstring.fr/> Thibault Houdon Formations </a>
- <a href=https://chrisbrejon.com/> Chris Brejon </a> that introduce me the idea of this tool and provided me an awesome 
support and documentation.