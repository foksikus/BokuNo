# BokuNo

A System for loading custom plugins and extending the capabilities of the Ragnarok-Online Client.

# Controller Support Plugin

A gamepad/controller plugin for Ragnarok Online that enables full controller support with customizable button mappings.

## Features

- **Full Gamepad Support**: Play Ragnarok Online with Xbox-style controllers
- **Movement Control**: Left thumbstick for character movement
- **Camera Control**: Right thumbstick for camera rotation
- **Customizable Button Mappings**: Configure any button to perform different actions
- **Skill Casting**: Use skills with configurable skill IDs and levels
- **Item Usage**: Quick-use items from your inventory
- **Target Selection**: Cycle through nearby enemies and auto-target closest mob
- **Attack Commands**: Attack selected targets with a button press

## Installation

1. **Copy Core DLL**: Place the `core` (renamed to `ddraw.dll`) into the root directory of your Ragnarok Online installation
   ```
   C:\Games\YourRagnarokFolder\ddraw.dll
   ```

2. **Copy Plugin Folder**: Copy the entire `plugins` folder containing both `controller_support_plugin.dll` and `config_gamepad.json` into the Ragnarok root directory
   ```
   C:\Games\YourRagnarokFolder\plugins\
       └── controller_support_plugin.dll
       └── config_gamepad.json
   ```

3. **Launch Game**: Start Ragnarok Online normally. The controller support will load automatically.

## Configuration

Edit `config_gamepad.json` to customize your button mappings. The configuration file uses a simple JSON structure:

```json
{
  "Buttons": {
    "BUTTON_NAME": {
      "action": "ActionType",
      "skill_id": 123,
      "item_id": 456,
      "level": 10
    }
  }
}
```

### Available Buttons

- `A_BUTTON`
- `B_BUTTON`
- `X_BUTTON`
- `Y_BUTTON`
- `RIGHT_SHOULDER` (RB/R1)
- `LEFT_SHOULDER` (LB/L1)
- `RIGHT_THUMB` (Right stick click/R3)
- `LEFT_THUMB` (Left stick click/L3)

### Available Actions

#### `Attack`
Attacks the currently selected target. If no target is selected, automatically selects the closest enemy.

**Parameters**: None

**Example**:
```json
"A_BUTTON": {
  "action": "Attack"
}
```

#### `UseSkill`
Casts a skill on yourself or a target (depending on skill type).
Casts on the currently selected target. If no target is selected, automatically selects the closest enemy.

**Parameters**:
- `skill_id` (required): The numeric ID of the skill
- `level` (required): The skill level to cast

**Example**:
```json
"B_BUTTON": {
  "action": "UseSkill",
  "skill_id": 50,
  "level": 10
}
```

*note: Ground skills are not supported yet.*

#### `UseItem`
Uses an item from your inventory.

**Parameters**:
- `item_id` (required): The numeric ID of the item

**Example**:
```json
"X_BUTTON": {
  "action": "UseItem",
  "item_id": 601
}
```

#### `NextTarget`
Cycles through nearby valid targets within range of 7. 

**Parameters**: None

**Example**:
```json
"RIGHT_SHOULDER": {
  "action": "NextTarget"
}
```

#### `CenterCamera`
Resets the camera angle to 0 degrees (default view).

**Parameters**: None

**Example**:
```json
"RIGHT_THUMB": {
  "action": "CenterCamera"
}
```

## Default Configuration Example

```json
{
  "Buttons": {
    "A_BUTTON": {
      "action": "Attack"
    },
    "B_BUTTON": {
      "action": "UseSkill",
      "skill_id": 50,
      "level": 10
    },
    "X_BUTTON": {
      "action": "UseItem",
      "item_id": 601
    },
    "Y_BUTTON": {
      "action": "UseSkill",
      "skill_id": 1013,
      "level": 1
    },
    "RIGHT_SHOULDER": {
      "action": "NextTarget"
    },
    "RIGHT_THUMB": {
      "action": "CenterCamera"
    }
  }
}
```

## Controls

- **Left Thumbstick**: Move your character
- **Right Thumbstick**: Rotate camera
- **Buttons**: As configured in `config_gamepad.json`

## Known Issues

- **Target Selection Icon**: The target selection indicator on monsters only works reliably if you manually click on a monster first with your mouse
- **Setup Application**: The `opensetup.exe` in the Ragnarok root directory will not open while `ddraw.dll` is present. Temporarily rename or remove `ddraw.dll` if you need to access game setup options
- **Ground skills not working**: Ground skills are **not** supported yet.



## Troubleshooting

1. **Controller not detected**: Ensure your controller is connected before launching Ragnarok Online
2. **Buttons not responding**: Verify your `config_gamepad.json` syntax is valid JSON
3. **Skills not casting**: Double-check skill IDs and ensure you meet the skill requirements (SP, items, etc.)
4. **Need to access game settings**: Temporarily rename `ddraw.dll` to something else, run `opensetup.exe`, then rename it back

## Notes
- Skills are automatically categorized as self-cast or target-cast based on skill ID
- Target range for cycling is currently set to 7 cells
- The only controller used for testing was an Xbox-Controller. It's likely that other controller types **won't** work.
- **BokuNo** will **only** work on **MyRO**. 