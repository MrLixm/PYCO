# :material-book-open-page-variant: START GUIDE

!!! success "Get the app"

    :material-download: Download the app here: <https://gum.co/pgtool>


## :material-arrow-down-bold-circle: Installation

Just unzip the file you downloaded and put the folder anywhere you want.
The .exe is in the folder, there is a lot of file inside but compared to if i just packed everything into .exe, 
the current solution is much faster to run.

## :material-numeric-1-box: Tutorial: create a Pointer's Gamut heat map for an image

This application is Command Line based, it means if you try to just open the .exe, nothing will happens.
You need to execute the app from a command prompt by calling commands.

- Open the Windows command prompt (win+r type *cmd* and hits enter)

- First you need to get the path to the .exe so go where you saved the app, shift+rightclick on it -> copy as path

- Go back in the command prompt, paste the path (shift+inser)(the path must start and end with `""`)

```bash
"L:\apps\PointerGamutCLTool_v1.exe"
```

- Enter the command you want to use , in this case `createpgmap`

```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap
```

- Get the path of the image you want to analyse, and paste it after the command
 (as always with a space in between)
 
```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap "L:\texture\randomTexture.exr"
```

- Now enter the path of the output file (with also the name.ext)

```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap "L:\texture\randomTexture.exr" "L:\texture\texture_pgmap.jpg"
```

- Enter the colorspace of the file ` --colorspace=sRGB` (always with a space after the last argument wrote)

!!!info

    This argument should specify the colorspace of your file.
    
    Examples of colorspaces available:
    
    - ACEScg, sRGB, BT709, ADOBE_WIDE_GAMUT, ADOBE_RGB_1998, ACES_2065_1


- If your file is not linear add ``--linearize`` that will linearize your file based on the colorspace specified.

!!! info ""
    
    Please refer to the **features** page where this option is explained in detail.
    
    You can just assume: use this option for jpg/png/... , don't use it for .exr/...

- You can precise the tolerance amount you want by adding ``--tolerance=yourNumber`` which is by default 0.

!!! info ""

    The range of this parameters is 0-1, but keep it very low. Something like is 0.08 is a good value if you want 
    some margin.

## :material-numeric-2-box: Tutorial: create a Pointer's Gamut heat map from a multi-layer/part exr

Let's say that this time you have a multi-layer exr of one of your render and you would like to analyse the 
"albedo" AOV that it holds:

(We skip some steps as they are explained above.)

- This time instead of createpgmap we are going to use `querylayers` that will allow us to display all the channels of 
all the subimages that your exr has. (in case you don't know how your aov is called)

- Just after the path to the .exe add the path to the render/image

```bash
"L:\apps\PointerGamutCLTool_v1.exe" querylayers "L:\render\randomRender.exr"
```

- Hit enter and you will see all the channel for each subimage displayed. Depending on how you exr is made you can get two result.
In both case just pick the name of the albedo aov like if you see "albedoAov.G", the name is "albedoAov".

````bash
# Example with a render from Redshift ("multi-layer" exr)

SubImage Index: 0, Channels:('R', 'G', 'B', 'A', 'Z', 
'DiffuseFilter.R', 'DiffuseFilter.G', 'DiffuseFilter.B', 
'Emission.R', 'Emission.G', 'Emission.B', 
'GIRaw.R', 'GIRaw.G', 'GIRaw.B', 'SpecularLighting.R', 'SpecularLighting.G')

# Example of the 2nd type of result you can get: (multi-part exr with multiple subimages)

SubImage 0, Channels:('R', 'G', 'B', 'A')

SubImage 1, Channels:('depth.Z',)

SubImage 2, Channels:('albedo.R', 'albedo.G', 'albedo.B')

SubImage 3, Channels:('speculard.R', 'speculard.G', 'speculard.B')

SubImage 4, Channels:('sss.R', 'sss.G', 'sss.B')
 
````

So now you can pick the name of the layer you want to analyse (for the Pointer's Gamut we are only interested in 
the albedo AOV which is called `DiffuseFilter` by Redshift)

- Now we can do the same steps as the first part of the tutorial, let's add the `createpgmap` command 
, the input_file_path, the output_file_path and the colorspace .

```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap "L:\render\randomRender.exr" "L:\render\renderX_pgmap.jpg" --colorspace=ACEScg  
```

- The only difference is this time, add the `--layername` option with, as value, the name of your albedo aov that we 
pick before. (so for me it's DiffuseFilter)

```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap "L:\render\randomRender.exr" "L:\render\renderX_pgmap.jpg" --colorspace=ACEScg --layername=DiffuseFilter 
```

- Hit enter and you got your map


## Example of command:


```bash
"L:\apps\PointerGamutCLTool_v1.exe" createpgmap "L:\render\randomRender.exr" "L:\render\renderX_pgmap.jpg" --colorspace=ACEScg --layername=Albedo 
```

``` bash
"./script/pointerGamutCLI.exe" createpgmap "L:\megascans\td3nedtla_4K_Albedo.jpg" "L:\megascans\CLI_apple_01.jpg" --colorspace=sRGB --linearize --tolerance=0.1 --out_map_type=add  
```
