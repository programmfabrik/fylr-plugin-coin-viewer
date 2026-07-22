# Coin Viewer

Adds an interactive 3D coin viewer to the fylr detail sidebar.

The viewer renders a coin with WebGL and uses normal maps to show surface relief.
You can change the light direction and intensity to bring out fine detail.
You can also zoom, rotate, flip between the two sides, pick a custom surface colour, show a measurement grid and switch to fullscreen.

## Usage

1. Upload a JSON file with coin data to a record in easydb
2. Open the record in detail view
3. Click the coin icon button in the detail sidebar to open the viewer
4. Use the interactive controls:
   - **Drag**: Move the coin or adjust light direction (toggle mode)
   - **Scroll/Pinch**: Zoom in/out
   - **Rotate buttons**: Rotate clockwise/counter-clockwise
   - **Flip button**: Show the other side of the coin
   - **Color picker**: Change the coin surface color
   - **Grid button**: Toggle measurement grid
   - **Reset button**: Reset view, light, color and position
   - **Fullscreen button**: Toggle fullscreen mode

## Configuration

The plugin has no settings in the base configuration.
It reads its data from the assets of a record.

Attach a file with the extension `.json` to a record.
The viewer button appears in the detail sidebar as soon as such a file is present.
If a record has several JSON assets, the first valid one is used.

## File format

The JSON file holds the two sides of the coin under `processData`.
Each side needs an `albedo` image and a `normal` image, both base64 encoded.
The `userData` block holds the initial light and rotation settings.

```json
{
  "processData": {
    "coinSide0": {
      "albedo": "(base-64 image)",
      "normal": "(base-64 image)"
    },
    "coinSide1": {
      "albedo": "(base-64 image)",
      "normal": "(base-64 image)"
    }
  },
  "userData": {
    "coinSideData0": {
      "intensity": 1.5,
      "lightDirectionX": 0.57735002040863037,
      "lightDirectionY": -0.57735002040863037,
      "lightDirectionZ": -0.57735002040863037,
      "rotation": 0
    },
    "coinSideData1": {
      "intensity": 1.5,
      "lightDirectionX": 0.57735002040863037,
      "lightDirectionY": -0.57735002040863037,
      "lightDirectionZ": -0.57735002040863037,
      "rotation": 0
    },
    "coinSideRotation": "Vertical"
  }
}
```

If no attached JSON file matches this format, the viewer shows an error message instead.

### Data Fields

| Field | Description |
|-------|-------------|
| `processData.coinSideX.albedo` | Base64 encoded color/texture image for the coin side |
| `processData.coinSideX.normal` | Base64 encoded normal map for surface detail rendering |
| `userData.coinSideDataX.intensity` | Light intensity multiplier |
| `userData.coinSideDataX.lightDirectionX/Y/Z` | Initial light direction vector |
| `userData.coinSideDataX.rotation` | Initial rotation angle |
| `userData.coinSideRotation` | Flip orientation: "Vertical" or "Horizontal" |

