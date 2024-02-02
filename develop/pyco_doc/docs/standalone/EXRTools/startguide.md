# :material-book-open-page-variant: START GUIDE

!!! success "Get the app"

    :material-download: Download the app here: <https://gum.co/exrtools>


## :material-arrow-down-bold-circle: Installation

Just unzip the file you downloaded and put the folder anywhere you want.

To install the Right-click context-menu follow the steps bellow.
Be carefull as you need to have the administrator rights on your pc to install it. (it needs to create keys in the registery editor)

### :material-cog: Settings (for the context-menu)
Next to the ...INSTALLER.exe you will find an `installer_settings.json`. This file will be used by the installer to determine some settings.
You can modify it to change the default behavior of the installer.(Json file can be easily opened in any text editor)

Options:

!!! info ""

    - auto_close: `true` or `false` 

    `true` to make the app auto close the command shell once finished
    
!!! info ""
 
    - auto_run_reg: `true` or `false` 
    
    `true` to auto run the registery file once this one has been created

!!! info ""

    - install_path: `null` or `string`
     
    `null` to have the default installation path in your documents
    
    else you can enter a custom path as: `"E:/Softwares/Tools"` for exemple.
    
    Think to use `/` or `\\` and not `\` in the path !

!!! info ""

    - remove_keys:`true` or `false` 
    
    Kind of "uninstall", it will remove the keys from the registery so the context menus will be deleted
    
!!! warning 
    be sur that you exactly natch the case as wrote in the documentation above. All lines except the last one must end with 
    a comma `,`
    
    default text should looks like this:
    
    ```json
    {
        "auto_close" : true,
        "auto_run_reg" : true,
        "install_path": null,
        "remove_keys": false
    }
    ```
    
### :material-progress-download: Installer

When you have modified your settings as you want or the default ones are just good you can run the INSTALLER.exe file.

- If you didn't set `auto_run_reg` to false:

    The registry editor will ask you if it can modify stuff, say yes. 
    
    !!! note ""
    
        Actually if you didn't set by default the reg file to be opened with the registery editor it will be probably
        opened in the text editor.
        
        To solve this go to `Documents/PYCO/EXRTools` right click on the .reg file and choose to open with the registery editor
         
         
    
    Then a warning message that you can also confirm.
    
    Finally you have a success message to confirm addition of the keys.

- If you set `auto_run_reg` to false:

    The default installation directory will be in your `Documents/PYCO/EXRTools` folder (if you didn't change it)

    Inside you will find a .reg file that you can choose to run or to modify (see [development](development.md)).
    
Aaand you'r good, then right click on any exr to see if the context menus appear.


## :material-gesture-tap: Utilisation

### Right click context menu

I think the right click menu is pretty explicit in what it does.

If you still have some doubts on what it does you can read the [home page](home.md) 



### Command line interface

This application is Command Line based, it means if you try to just open the .exe, nothing will happens.
You need to execute the app from a command prompt by calling commands.

- Open the Windows command prompt (win+r type *cmd* and hits enter)

- First you need to get the path to the .exe so go where you saved the app, shift+rightclick on it -> copy as path

- Go back in the command prompt, paste the path (shift+inser)(the path must start and end with `""`)

```bash
"L:\apps\EXRTools.exe"
```

- Enter the command you want to use (see [features](features.md)), for this quick example we are going to use `exr-resize`

```bash
"L:\apps\EXRTools.exe" exr-resize
```

- Get the path of the image you want to resize, and paste it after the command
 (as always with a space in between)
 
```bash
"L:\apps\EXRTools.exe" exr-resize "L:\texture\randomTexture.exr"
```

- Now just enter the resolution you want to resize to

```bash
"L:\apps\EXRTools.exe" exr-resize "L:\texture\randomTexture.exr" 1024
```

- You can press Enter as all the required arguments are given, but for this exemple we are going to add the option
`--suffix`.

```bash
"L:\apps\EXRTools.exe" exr-resize "L:\texture\randomTexture.exr" 1024 --suffix=_resize1024
```

- Press enter and wait for the converter to finish

