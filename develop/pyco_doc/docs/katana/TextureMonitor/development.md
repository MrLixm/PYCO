# :material-file-code: Development

!!! success "Github repo"

    :material-github:  <https://github.com/MrLixm/Katana_Texture-Monitor>


### License

Unless you buy a specific license, this work is licensed by default under the
 `Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License`.
To view a copy of this license, visit <http://creativecommons.org/licenses/by-nc-sa/4.0/>.

Which can be resumed to:

- No commercial use 
- You must give appropriate credit and provide a link to the license.
- You can share, copy and redistribute the material in any medium or format under the same license.
- You must distribute your contributions under the same license as the original.

(*these restrictions might not apply if you bought a commercial license*)

!!! info "Abbreviations used"

    `r-e`: render-engine
    
    `re-tex`: render-engine textures
    
    `tpt`: texture processor tool (like `maketx.exe`)


## :material-expand-all-outline: Expanding Render-engine features

The tool can support any render-engine but is only shipped with `Redshift`, `3Delight` and `Arnold` 
, with the last two having limited render-engine texture baking features.

You can find the Render-engine modules in `Tabs\textureMonitor\script\render_engine`.

Each r-e is represented by a .py file to its name. Here is first how this file is structured, and then a tutorial
to modify it.


### :material-file-document: Render-engine File structure

You can add any function/variable in the file but you have to keep all the existing one 
(except `_find_retexture_processor()` which is only used locally).

!!! abstract "name (_variable_)"

    (str) Name of the render-engine, use the name you give to the file. (ex: `"Vray"`)

!!! abstract "re_tex_ext (_variable_)"

    (str) Name of the extension of the re-tex, with the dot (ex: `".tx"`).

!!! abstract "support_re_baking (_variable_)"

    (bool) Setting it to `True` will unlock feature for baking re-tex
    
!!! abstract "PATH_PATTERN (_variable_)"

    ((dict)(str:str)) This allow the tool to find children textures related to a filepath that use a token like <UDIM>.
    
    Read the docstring above, you will need to have a look at your r-e documentation to 
    know which token are supported.
    
    * The key is a python 
    <a href=https://www.datacamp.com/community/tutorials/python-regular-expression-tutorial#summary-table>
     regular expression.  </a>. (from the `re` module)
    
    * The value is a python <a href=https://docs.python.org/3/library/fnmatch.html>
     glob module expression </a>. (Unix shell-style wildcards)
     
    r-e such as Arnold allow to use rendertime-evaluated token (such as <shapeName> which make impossible to find
    exactly what children it refers to. Accordingly a "wide" match is performed with "*".

!!! abstract "re_textool (_variable_)"

    (str) Path to the re-tex processing tool, ex: `"C:\\Redshift\\bin\\redshiftTextureProcessor.exe"`
    
    In the template I used a function to be sure the path exists and to return a different path 
    depending of the user setup.

!!! example "bake_retex (_function_)"

    _(optional if `re_tex_ext` is disabled)_
    
    Send a command with the file_path arg to the texture processor tool. You can then perform a simple check if 
    the texture.re_tex_ext exists and return False if not.
    
    This function will be used in a QThread

        Args:
            file_path(str):  file path to bake
        Returns:
            bool:
                rstex_path if success else False if error
        Raises:
            ValueError: if file_path arg is not a string

!!! example "get_re_texture_nodes (_function_)"

    _(required)_
    
    Iterate trough the node in the scene to find texture-Nodes. Each one is added in a dictionnary where the key
    is the katana node and the value is a list with `list[0]`=file path normalized and 
    `list[1]` = file path katana parameter.
    
        Returns:
            dict: Nodes3DAPI.ShadingNodeBase:[str, Parameter]

    
!!! example "return_retex_from_path (_function_)"

    _(required)_
    
    From a given filepath (no matter if it exists or not) return what could be the potential path of the re-tex one.
    
    If you check that the re-tex didn't exists you can just return an empty string.(the result is going to be pick
    later by an `os.path.exists()`)
    
    Ex: `D:\projects\textures\texture01.exr` will return `D:\projects\textures\texture01.tx` for Arnold


### :material-plus: Adding a render-engine

Duplicate the `__template.py` file and rename it with the name of your render-engine, starting by a capital letter.
(ex: `Vray`). It is recommended to have a look at the existing one (Redshift being fully completed).

* First step is to fill the variable as explained in the above section.

* For the `re_textool` variable you can if you want skip the function `_find_retexture_processor()` and directly assign
the path to the texture processor tool.

!!! note "bake_retex()" 

    is optionnal if you set `support_re_baking` variable to `False`.

    Else using the subprocess module you can call the tpt passing it the file_path argument.
    
    To know which command to send to the tpt you will need to read your r-e documentation

!!! note "get_re_texture_nodes()"

    It is the core function of the tool as it allow to pick up the texture nodes.

    The function is already built but you can of course re-write it as you wish as long as it returns the same
    dictionnary.
    
    If you want to keep it like this you can replace the `"___TO CHANGE___"` as follow:
    
    * First: name of the r-e shading node. ex: `ArnoldShadingNode`
    
    * Second: name of the type set on the shading node for texture nodes. 
    
        ex: `TextureSampler` for Redshift.
        
    * Third: python path of the parameter relative to the file path. _To get it you can just hover your mouse over
    the parameter in the interface._ You must add `.value` at its end. 
    
        ex: `parameters.tex0.value` for Redshift

!!! note "return_retex_from_path()"

    You should have nothing to touch in this function if your r-e doesn't doesn't anything fancy with the re-tex.
    
    For example 3Delight add the OCIO colorspace used in the path (original_name + OCIO + .tdl) so i had to use the
    glob module to return the existing tdl file. If the file didn't exists it just return an empty string.


## :material-expand-all-outline: Expanding features

I tried to make the code as much flexible as I could to incorporate other features.

As an example you can find the `TREEW_DATA` dict in `\constants.py` which allow to easily add an other column
to the tree widget.

Unfortunately for you who are reading this I didn't have time for now to make a detailed tutorial on how to use my code
 to expand features in the tool.
  
You can reach to me if you would like more detail about this:
 
 :material-email: monsieurlixm@gmail.com
 
 :material-linkedin: <a href=https://www.linkedin.com/in/liam-collod/> Liam Collod </a>
