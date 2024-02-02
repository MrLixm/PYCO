
# :material-code-not-equal-variant: Development

!!! quote ""

    :material-github: **Public Github repository:** <https://github.com/MrLixm/Colorspace_Converter>
    
    * _Master:_ Public realeased branch.
    
    * _Develop:_ Active development branch.

## :material-pencil: Creating the project  
   
### :material-language-python: Python version 3.6.8

VirtualEnvironment:
``` py
$ pip install PySide2==5.13.1
$ pip install colour-science==0.3.15
$ pip install 'colour-science[optional]'
$ pip install fbs==0.8.6
$ pip install "..\oiio-2.0.5-cp36-none-win_amd64.whl"
```

The oiio Python wheel can be downloaded here: <https://github.com/fredrikaverpil/oiio-python/releases>

### :material-microsoft-windows: Install Windows 10 SDK

<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/>

### :material-bug: Fix Scipy lib not found Issue:

(On windows at least)

Scipy cause problem when freezing, to fix:

- Go to the package location: `venvColour\Lib\site-packages\scipy`
- Create a new folder `/extra-dll`
- Copy the content of `/.libs` in `/extra-dll`

**Shared under CC BY-SA 4.0 license.**
BY – Credit must be given to the creator
SA – Adaptations must be shared under the same terms
<https://creativecommons.org/licenses/by-sa/4.0/>