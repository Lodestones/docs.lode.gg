# Commands Reference

This page provides a complete reference for all Amplifier commands, including usage, permissions, and examples.

## Command Overview

All Amplifier commands use the `lodestone.amplifier.commands.*` permission prefix. Commands can be executed by players or console operators with the appropriate permissions.

## Broadcasting Commands

### `/startbroadcasting [player]`

Starts voice broadcasting for a player, allowing their voice to be heard by all players on the server.

**Permission**: `lodestone.amplifier.commands.startbroadcasting`

**Usage**:
- `/startbroadcasting` - Start broadcasting for yourself
- `/startbroadcasting <player>` - Start broadcasting for another player

**Examples**:
```bash
/startbroadcasting
/startbroadcasting Notch
```

**Messages**:
- Success: "You are now broadcasting." or "<player> is now broadcasting."
- Already broadcasting: "You are already broadcasting." or "This player is already broadcasting."

### `/stopbroadcasting [player]`

Stops voice broadcasting for a player, returning to normal voice chat range.

**Permission**: `lodestone.amplifier.commands.stopbroadcasting`

**Usage**:
- `/stopbroadcasting` - Stop broadcasting for yourself
- `/stopbroadcasting <player>` - Stop broadcasting for another player

**Examples**:
```bash
/stopbroadcasting
/stopbroadcasting Notch
```

**Messages**:
- Success: "You are no longer broadcasting." or "<player> is no longer broadcasting."
- Not broadcasting: "You are not broadcasting." or "This player is not broadcasting."

## Voice Settings Commands

### `/setvoicedistance <distance> [player]`

Sets the voice chat distance for a player. Distance determines how far other players can hear the target player.

**Permission**: `lodestone.amplifier.commands.setvoicedistance`

**Parameters**:
- `distance` (float): Voice distance in blocks (0.0 to unlimited)
- `player` (optional): Target player (defaults to command sender)

**Usage**:
- `/setvoicedistance <distance>` - Set your own voice distance
- `/setvoicedistance <distance> <player>` - Set another player's voice distance

**Examples**:
```bash
/setvoicedistance 32
/setvoicedistance 64 Notch
/setvoicedistance -1  # Unlimited distance
```

**Messages**:
- Success: "Your voice distance has been set to <distance>." or "<player>'s voice distance has been set to <distance>."

### `/setvolume <volume> [player]`

Sets the voice volume for a player. Volume affects how loud the player's voice appears to others.

**Permission**: `lodestone.amplifier.commands.setvolume`

**Parameters**:
- `volume` (float): Voice volume multiplier (0.0 to 5.0)
- `player` (optional): Target player (defaults to command sender)

**Usage**:
- `/setvolume <volume>` - Set your own voice volume
- `/setvolume <volume> <player>` - Set another player's voice volume

**Examples**:
```bash
/setvolume 1.0
/setvolume 1.5 Notch
/setvolume 0.5  # Half volume
/setvolume 2.0  # Double volume
```

**Messages**:
- Success: "Your voice volume has been set to <volume>." or "<player>'s voice volume has been set to <volume>."

### `/setpitch <pitch> [player]`

Sets the voice pitch for a player. Pitch affects the tone of the player's voice.

**Permission**: `lodestone.amplifier.commands.setpitch`

**Parameters**:
- `pitch` (float): Voice pitch multiplier (0.1 to 5.0)
- `player` (optional): Target player (defaults to command sender)

**Usage**:
- `/setpitch <pitch>` - Set your own voice pitch
- `/setpitch <pitch> <player>` - Set another player's voice pitch

**Examples**:
```bash
/setpitch 1.0
/setpitch 1.5 Notch
/setpitch 0.8  # Lower pitch
/setpitch 1.3  # Higher pitch
```

**Messages**:
- Success: "Your voice pitch has been set to <pitch>." or "<player>'s voice pitch has been set to <pitch>."

## Mute Commands

### `/mutevoicechat [player]`

Mutes a player's voice, preventing them from being heard by others.

**Permission**: `lodestone.amplifier.commands.mutevoicechat`

**Usage**:
- `/mutevoicechat` - Mute yourself (console only)
- `/mutevoicechat <player>` - Mute another player

**Examples**:
```bash
/mutevoicechat Notch
```

**Messages**:
- Success: "You have been muted." or "<player> has been muted."
- Already muted: "You are already muted." or "This player is already muted."

### `/unmutevoicechat [player]`

Unmutes a player's voice, allowing them to be heard again.

**Permission**: `lodestone.amplifier.commands.unmutevoicechat`

**Usage**:
- `/unmutevoicechat` - Unmute yourself (console only)
- `/unmutevoicechat <player>` - Unmute another player

**Examples**:
```bash
/unmutevoicechat Notch
```

**Messages**:
- Success: "You have been unmuted." or "<player> has been unmuted."
- Not muted: "You are not muted." or "This player is not muted."

## Global Commands

### `/setglobalvoicedistance <distance>`

Sets the global voice chat distance for all players on the server.

**Permission**: `lodestone.amplifier.commands.setglobalvoicedistance`

**Parameters**:
- `distance` (float): Global voice distance in blocks

**Usage**:
```bash
/setglobalvoicedistance 48
/setglobalvoicedistance 64
```

**Messages**:
- Success: "Global voice distance has been set to <distance>."

### `/muteglobalvoicechat`

Mutes all voice chat on the server, preventing any player from being heard.

**Permission**: `lodestone.amplifier.commands.muteglobalvoicechat`

**Usage**:
```bash
/muteglobalvoicechat
```

**Messages**:
- Success: "Global voice chat has been muted."

### `/unmuteglobalvoicechat`

Unmutes all voice chat on the server, allowing players to be heard again.

**Permission**: `lodestone.amplifier.commands.unmuteglobalvoicechat`

**Usage**:
```bash
/unmuteglobalvoicechat
```

**Messages**:
- Success: "Global voice chat has been unmuted."

## Special Commands

### `/setdeafened <true/false> [player]`

Sets a player as deafened, preventing them from hearing other players' voices.

**Permission**: `lodestone.amplifier.commands.setdeafened`

**Parameters**:
- `true/false` (boolean): Whether the player should be deafened
- `player` (optional): Target player (defaults to command sender)

**Usage**:
- `/setdeafened true` - Deafen yourself
- `/setdeafened false` - Undeafen yourself
- `/setdeafened true <player>` - Deafen another player
- `/setdeafened false <player>` - Undeafen another player

**Examples**:
```bash
/setdeafened true
/setdeafened false Notch
```

**Messages**:
- Success: "You are now deafened." / "You are no longer deafened." or "<player> is now deafened." / "<player> is no longer deafened."

### `/setreverb <true/false> [player]`

Enables or disables reverb effects for a player's voice.

**Permission**: `lodestone.amplifier.commands.setreverb`

**Parameters**:
- `true/false` (boolean): Whether reverb should be enabled
- `player` (optional): Target player (defaults to command sender)

**Usage**:
- `/setreverb true` - Enable reverb for yourself
- `/setreverb false` - Disable reverb for yourself
- `/setreverb true <player>` - Enable reverb for another player
- `/setreverb false <player>` - Disable reverb for another player

**Examples**:
```bash
/setreverb true
/setreverb false Notch
```

**Messages**:
- Success: "Reverb has been enabled." / "Reverb has been disabled." or "<player>'s reverb has been enabled." / "<player>'s reverb has been disabled."

## Administrative Commands

### `/reloadamplifier`

Reloads the Amplifier configuration file without restarting the server.

**Permission**: `lodestone.amplifier.commands.reload`

**Usage**:
```bash
/reloadamplifier
```

**Messages**:
- Success: "Amplifier configuration has been reloaded."
- Error: "Failed to reload configuration. Check console for details."

## Permission Reference

### Basic Permissions

| Permission | Description |
|------------|-------------|
| `lodestone.amplifier.bypass` | Bypass all voice chat restrictions |
| `lodestone.amplifier.commands.*` | Access to all Amplifier commands |

### Command Permissions

| Permission | Commands |
|------------|----------|
| `lodestone.amplifier.commands.startbroadcasting` | `/startbroadcasting` |
| `lodestone.amplifier.commands.stopbroadcasting` | `/stopbroadcasting` |
| `lodestone.amplifier.commands.setvoicedistance` | `/setvoicedistance` |
| `lodestone.amplifier.commands.setvolume` | `/setvolume` |
| `lodestone.amplifier.commands.setpitch` | `/setpitch` |
| `lodestone.amplifier.commands.mutevoicechat` | `/mutevoicechat` |
| `lodestone.amplifier.commands.unmutevoicechat` | `/unmutevoicechat` |
| `lodestone.amplifier.commands.setglobalvoicedistance` | `/setglobalvoicedistance` |
| `lodestone.amplifier.commands.setdeafened` | `/setdeafened` |
| `lodestone.amplifier.commands.muteglobalvoicechat` | `/muteglobalvoicechat` |
| `lodestone.amplifier.commands.unmuteglobalvoicechat` | `/unmuteglobalvoicechat` |
| `lodestone.amplifier.commands.setreverb` | `/setreverb` |
| `lodestone.amplifier.commands.reload` | `/reloadamplifier` |

## Usage Examples

### Basic Voice Management

```bash
# Set up a player with custom voice settings
/setvoicedistance 32 Notch
/setvolume 1.5 Notch
/setpitch 1.2 Notch

# Enable broadcasting for announcements
/startbroadcasting Notch

# Disable broadcasting when done
/stopbroadcasting Notch
```

### Moderator Actions

```bash
# Mute a disruptive player
/mutevoicechat DisruptivePlayer

# Deafen a player temporarily
/setdeafened true DisruptivePlayer

# Restore player's voice
/unmutevoicechat DisruptivePlayer
/setdeafened false DisruptivePlayer
```

### Server Administration

```bash
# Set global voice distance
/setglobalvoicedistance 64

# Mute all voice chat during maintenance
/muteglobalvoicechat

# Restore voice chat
/unmuteglobalvoicechat

# Reload configuration after changes
/reloadamplifier
```

### Special Effects

```bash
# Give a player echo effect
/setreverb true EchoPlayer

# Remove echo effect
/setreverb false EchoPlayer
```

## Error Messages

### Common Error Messages

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "You don't have permission to use this command." | Missing permission | Grant the required permission |
| "This command can only be used by players." | Console tried to use player-only command | Use a player account or specify target player |
| "Player not found." | Target player is not online | Ensure player is online or use UUID |
| "Invalid distance value." | Distance is outside valid range | Use a value between 0 and maximum |
| "Invalid volume value." | Volume is outside valid range | Use a value between 0.0 and 5.0 |
| "Invalid pitch value." | Pitch is outside valid range | Use a value between 0.1 and 5.0 |

### Troubleshooting

1. **Permission Denied**: Check that the player has the required permission
2. **Player Not Found**: Ensure the target player is online
3. **Invalid Values**: Use values within the specified ranges
4. **Configuration Errors**: Use `/reloadamplifier` to reload after config changes

## Integration with Permission Plugins

### LuckPerms Example

```bash
# Grant all Amplifier permissions to admins
/lp group admin permission set lodestone.amplifier.commands.* true

# Grant specific permissions to moderators
/lp group moderator permission set lodestone.amplifier.commands.mutevoicechat true
/lp group moderator permission set lodestone.amplifier.commands.unmutevoicechat true
/lp group moderator permission set lodestone.amplifier.commands.setdeafened true

# Grant broadcasting permission to trusted players
/lp group trusted permission set lodestone.amplifier.commands.startbroadcasting true
/lp group trusted permission set lodestone.amplifier.commands.stopbroadcasting true
```

### EssentialsX Example

```bash
# Add permissions to groups
/pex group admin add lodestone.amplifier.commands.*
/pex group moderator add lodestone.amplifier.commands.mutevoicechat
/pex group moderator add lodestone.amplifier.commands.unmutevoicechat
/pex group moderator add lodestone.amplifier.commands.setdeafened
``` 