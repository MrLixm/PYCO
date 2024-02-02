# :material-collapse-all-outline: Features



## Context menu

By default the application is copied to your Documents location in a PYCO/EXRTools folder.

If modifying the installer settings to uninstall the keys doesn't work you can open the registery editor and delete the PYCO keys in 
`HKEY_CLASSES_ROOT\SystemFileAssociations\.exr`

## Command Line Interface

This section describe the feature of the CLI application.

Structure:
```bash
"pathto/EXRTools.exe" command arguments [Options]
```

## :material-view-list-outline: Command list


### :material-numeric-1-box: exr-swap-resize command

Resize an exr to the given resolution (1:1 ratio). The input exr is renamed wil the `OLD_` prefix and the resized version is 
renamed like the original. 

```bash
"pathto/EXRTools.exe" exr-swap-resize EXR_FILE RESOLUTION [Options]
```

**Arguments:**

- (str)EXR_FILE is the path to the exr.

- (int)RESOLUTION is the resolution in pixels to resize the map to. ex: `2048`

**Options:**

#### `--revert` 

Revert the resize operation by deleting the resize result and renaming the original image (remove OLD_ prefix)

#### `--auto_close` 

Command shelf self close at the end of the process if specified. (instead of asking the user to press a key to close)

!!! warning

    These methods will crop any input to RGBA only.



### :material-numeric-2-box: exr-resize command

Resize an exr to the given resolution (1:1 ratio).

```bash
"pathto/EXRTools.exe" exr-resize EXR_FILE RESOLUTION [Options]
```

**Arguments:**

- (str)EXR_FILE is the path to the exr.

- (int)RESOLUTION is the resolution in pixels to resize the map to. ex: `2048`

**Options:**

#### `--out_path` 

Specify an output path for the converted exr (with filename.exr). By default the resized version is created at the
same location of the original.

#### `--suffix` 

Specify the suffix on the file name when --out_path is not specified. The default one is based on the resolution.


#### `--auto_close` 

Command shelf self close at the end of the process if specified. (instead of asking the user to press a key to close)

!!! warning

    These methods will crop any input to RGBA only.


### :material-numeric-3-box: exr-to-mpart command

Convert a multi-channel exr to a multi-part one

```bash
"pathto/EXRTools.exe" exr-to-mpart EXR_FILE [Options]
```

**Arguments:**

- (str)EXR_FILE is the path to the exr.

**Options:**

#### `--out_path` 

Specify an output path for the converted exr (with filename.exr). By default the multi-part version is created at the
same location of the original.

#### `--write_mode` 

Specify a write mode for the exr, which is by default `scanlines`.

!!! info ""

    Write modes available are : 
    
    `scanlines` 
    
    `tiles:tiles_width,tile_height ` tiles size must be specified after a colon, separated by a comma. 
    
    `image` write the whole image at once (very slow)

#### `--suffix` 

Specify the suffix on the file name when --out_path is not specified. The default one is `_mpart`


#### `--auto_close` 

Command shelf self close at the end of the process if specified. (instead of asking the user to press a key to close)

!!! info

    The more you have layers(AOV/light group) in your original exr, the more time it will take to convert it to a multi-part exr.



### :material-numeric-4-box: exr-info command

Return useful informations about the exr

```bash
"pathto/EXRTools.exe" exr-info EXR_FILE [Options]
```

**Arguments:**

- (str)EXR_FILE is the path to the exr.

**Options:**

#### `--metadata`

Also display extra attribute in the file (metadata)

#### `--obly_metadata`

Display ONLY the extra attribute of the file (metadata)



### :material-numeric-5-box: exr-recompress command

Resize an exr to the given resolution (1:1 ratio).

```bash
"pathto/EXRTools.exe" exr-recompress EXR_FILE COMPRESSION [Options]
```

**Arguments:**

- (str)EXR_FILE is the path to the exr.

- (str)COMPRESSION is the compression method to use.

    Method available are `none, rle, zip, zips, piz, pxr24, b44, b44a, dwaa, dwab`
    
    If you are using `dwaa` or `dwab` you can specify the compression level after a colon. ex: `dwaa:30`
    
    `b44, b44a, pxr24` are made for HALF-Float images. `b44a` is supported for flat images (uniform colors)

**Options:**

#### `--out_path` 

Specify an output path for the converted exr (with filename.exr). By default the resized version is created at the
same location of the original.

#### `--write_mode` 

Specify a write mode for the exr, which is by default `scanlines`.

!!! info ""

    Write modes available are : 
    
    `scanlines` 
    
    `tiles:tiles_width,tile_height ` tiles size must be specified after a colon, separated by a comma. 
    
    `image` write the whole image at once (very slow)


#### `--suffix` 

Specify the suffix on the file name when --out_path is not specified. The default one is based on the compression method.


#### `--auto_close` 

Command shelf self close at the end of the process if specified. (instead of asking the user to press a key to close)

!!! info

    If you submit a multi-part exr all the parts are going to be recompressed to the same given compression.


!!! bug "Known Issues"

    If some erros happens during the process, the script will try to delete the potential created file but will fail.