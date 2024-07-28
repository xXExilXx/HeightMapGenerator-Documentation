# HeightMapGenerator Documentation

## Overview

`HeightMapGenerator` is a Unity library for generating heightmaps using Perlin noise. It allows for highly configurable heightmap creation, including options for seamless textures and various scaling parameters. The generated heightmap can be used in Unity for terrain generation or other graphical applications.

## Features

- **Customizable Heightmap Generation**: Configure parameters for Perlin noise and heightmap appearance.
- **Texture Creation**: Generate a `Texture2D` from heightmap data.
- **Seamless Tiling**: Option to generate seamless textures.
- **Texture Saving**: Save the generated texture directly within the Unity project (editor-only).

## Usage

### HeightMapConfig Class

The `HeightMapConfig` class allows you to set parameters for heightmap generation.

**Properties:**

- **PerlinXScale**: Scale factor for the X-axis Perlin noise. Default is `0.05f`.
- **PerlinYScale**: Scale factor for the Y-axis Perlin noise. Default is `0.05f`.
- **PerlinOctaves**: Number of octaves for Perlin noise. Default is `6`.
- **PerlinPersistance**: Persistence of the noise. Default is `0.5f`.
- **PerlinHeightScale**: Scaling factor for height values. Default is `0.5f`.
- **PerlinOffsetX**: X-axis offset for Perlin noise. Default is `0`.
- **PerlinOffsetY**: Y-axis offset for Perlin noise. Default is `0`.
- **AlphaToggle**: Whether to use alpha channel in the texture. Default is `false`.
- **SeamlessToggle**: Whether to generate a seamless texture. Default is `false`.
- **MapToggle**: Whether to map color values to a normalized range. Default is `false`.
- **Brightness**: Brightness adjustment for the texture. Default is `0.5f`.
- **Contrast**: Contrast adjustment for the texture. Default is `0.5f`.
- **Seed**: Random seed for Perlin noise. Default is `123456789`.

### GenerateTexture Method

Generates a `Texture2D` based on the specified configuration.

```csharp
public static Texture2D GenerateTexture(HeightMapConfig config)
```

**Parameters:**
- `config`: An instance of `HeightMapConfig` with settings for generating the heightmap.

**Returns:**
- `Texture2D`: The generated heightmap texture.

**Example Usage:**

```csharp
var config = new HeightMapGenerator.HeightMapConfig
{
    PerlinXScale = 0.1f,
    PerlinYScale = 0.1f,
    PerlinOctaves = 4,
    PerlinPersistance = 0.6f,
    PerlinHeightScale = 0.8f,
    AlphaToggle = true,
    Brightness = 0.7f,
    Contrast = 1.2f,
    Seed = 987654321
};

Texture2D heightmap = HeightMapGenerator.GenerateTexture(config);
```

### GenerateHeightData Method

Generates height data as a 2D array and calculates the minimum and maximum color values.

```csharp
public static float[,] GenerateHeightData(HeightMapConfig config, out float minColour, out float maxColour)
```

**Parameters:**
- `config`: An instance of `HeightMapConfig` with settings for heightmap generation.
- `minColour`: Output parameter for the minimum color value.
- `maxColour`: Output parameter for the maximum color value.

**Returns:**
- `float[,]`: 2D array of height values.

**Example Usage:**

```csharp
float minColour, maxColour;
float[,] heightData = HeightMapGenerator.GenerateHeightData(config, out minColour, out maxColour);
```

### SaveTexture Method (Editor Only)

Saves the generated texture to the Unity project. This method is available only in the Unity Editor.

```csharp
public static void SaveTexture(Texture2D texture, string filename)
```

**Parameters:**
- `texture`: The `Texture2D` object to save.
- `filename`: The name of the saved texture asset (without extension).

**Example Usage:**

```csharp
#if UNITY_EDITOR
HeightMapGenerator.SaveTexture(heightmap, "MyGeneratedHeightmap");
#endif
```

**Note**: This method will create a directory at `Assets/HeightMapGenerator/HeightMaps/` if it does not already exist and save the texture as a PNG file.

## Utility Methods

The library relies on methods that should be defined in a `Utility` class:

- **FractalBrownianMotion**: Generates fractal noise based on Perlin noise parameters.
- **Map**: Maps a value from one range to another.

Ensure these methods are implemented in your `Utility` class for proper functionality.

## Troubleshooting

- **Texture Issues**: If the texture does not appear correctly, check the configuration settings, including scales and offsets. Ensure that the `FractalBrownianMotion` method is properly implemented.
- **Editor-Specific Code**: Confirm that the `UNITY_EDITOR` symbol is defined for any editor-specific code to function correctly.

## License

This library is distributed under the [MIT License](https://opensource.org/licenses/MIT), allowing modification and redistribution.

---