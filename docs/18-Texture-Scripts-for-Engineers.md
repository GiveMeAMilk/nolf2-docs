# Texture Scripts for Engineers

This document describes the structure of texture scripts and the small scripting language used to build them.

## Script Header

The header has three fields that must be specified in this order:

1. `UserParams`
2. `Input`
3. `Output`

`UserParams` is a comma-delimited list of parameter names that the script can access through game code. The current limit is six, although it may be increased in the future.

The `Input` field specifies the type of vector that the matrix will be multiplied by in order to obtain the output values. These can be one of the following:

| Input | Description |
| --- | --- |
| `UV` | The UV coordinates of the vertex for that channel. Anything beyond what is provided is `0`, so for 2 texture coordinates, the third and fourth multiplied components are `0`. |
| `WSPos` | The position of the vertex in world space. The fourth parameter is `1`. |
| `WSNormal` | The normal of the vertex in world space. This is only applicable for vertices that specify a normal, currently only environment-mapped polygons. |
| `WSReflection` | The vector from the camera to the vertex reflected over the normal. The same constraints that apply to the normal apply here as well. |
| `CSPos` | The same values as above, but provided in camera space instead of world space. |
| `CSNormal` | Camera-space normal. |
| `CSReflection` | Camera-space reflection vector. |

The `Output` field specifies how the product of the matrix and input should be used. It can be one of the following values:

| Output | Description |
| --- | --- |
| `TexCoord2` | UV texture coordinates |
| `TexCoord3` | UVW texture coordinates |
| `TexCoord3Proj` | `U/W V/W` texture coordinates |
| `TexCoord4Proj` | `U/X V/X W/X` texture coordinates |

## Script Body

The body of the script must be enclosed within the words `BeginScript` and `EndScript`. Inside that block is a list of semicolon-delimited assignments.

The operations supported by the language are listed below:

| Operator | Meaning |
| --- | --- |
| `+` | Addition |
| `-` | Subtraction or negation |
| `*` | Multiplication |
| `/` | Division |
| `%` | Bind/modulo, maps left to `0..right` |
| `<` | Minimum, returns the smaller of two parameters |
| `>` | Maximum, returns the larger of two parameters |
| `=` | Assignment |

The language also supports the following functions:

- `sin`
- `cos`
- `tan`

## Available Variables

Inside the script body, the script has access to a number of variables.

### User variables

These are the variables named in `UserParams`, and they can be referenced by those exact names.

### Matrix variables

The script can access matrix elements through variables named `MatRC`, where `R` is the row and `C` is the column. Both range from `0` to `3`.

Examples:

- `Mat00` is the upper-left element.
- `Mat03` is the upper-right element.

### Special variables

The script also has access to these built-in values:

- `Time`: Total number of seconds the script has been running.
- `Elapsed`: Number of seconds since the last update.

### Level offset variables

The preprocessor is allowed to shift the level as close to the origin as possible, so any parameter that depends on level coordinates must compensate for that offset.

The following variables are provided for that purpose:

- `LevelOffsetX`
- `LevelOffsetY`
- `LevelOffsetZ`

For example, if a user parameter represents a center point to rotate about, the script could compensate like this:

```text
Mat03 = RotationX + LevelOffsetX;
```

## Performance Notes

The fewer operations a script performs, the faster it will execute. Try to reduce terms as much as possible by:

- doing math on constants by hand
- caching temporary results
- reusing unused matrix elements for intermediate values when appropriate

Most of the complexity in these scripts comes from the underlying matrix math, so it is helpful to keep a good linear algebra reference nearby.

## Example Script

Below is a sample script, with the original comments preserved, to illustrate the structure described above.

```text
#########################################
# Warble
#
# This script causes the UV coordinates to
# warble around as if underwater based upon
# the user parameters.
##########################################

# Our parameters:
# XFreq, YFreq How many cycles per second for X and Y
# XScale, YScale The amount to offset for each X and Y
UserParams XFreq, YFreq, XScale, YScale;

# We want to take the original UV coordinates in as parameters for our script
Input UV;

# We are going to output 2 texture coordinates, a U and a V
Output TexCoord2;

# Here is our actual script block
BeginScript

# Now set up the appropriate matrix components to warble
Mat01 = cos((Time * XScale) % (2 * 3.14159)) * XScale;
Mat10 = sin((Time * YScale) % (2 * 3.14159)) * YScale;

EndScript
```
