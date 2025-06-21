# Server Owner Guide

This guide is designed for server owners and administrators who want to set up and manage Amplifier on their Minecraft server.

## Installation

### Prerequisites

1. **Minecraft Server**: Paper/Spigot 1.21+
2. **Java**: Version 17 or higher
3. **Simple Voice Chat**: Must be installed and configured

### Step-by-Step Installation

1. **Download Amplifier**
   - Get the latest release from the official repository
   - Ensure you download the correct version for your server

2. **Install Simple Voice Chat**
   - Download and install Simple Voice Chat plugin
   - Configure it according to the official documentation
   - Test that voice chat is working properly

3. **Install Amplifier**
   - Place the Amplifier JAR file in your `plugins` folder
   - Start your server
   - Amplifier will generate default configuration files

4. **Initial Configuration**
   - Stop your server
   - Edit `plugins/Amplifier/config.yml`
   - Configure basic settings (see Configuration section)
   - Restart your server

## Configuration

### Basic Configuration

The main configuration file is located at `plugins/Amplifier/config.yml`:

```yaml
# Amplifier Plugin Configuration
version: 1

# Voice Chat Settings
voice-chat:
  # Maximum distance for voice chat (in blocks)
  max-distance: 48
  # Whether if voice chat is enabled (if disabled, only those with "lodestone.amplifier.bypass" permission can still speak)
  enabled: true
  # Whether to enable debug mode
  debug: false

# Storage Settings
storage:
  # Storage type: LOCAL, MYSQL, or MONGODB
  type: "LOCAL"
  
  # MySQL Configuration (only used if type is MYSQL)
  mysql:
    url: "jdbc:mysql://localhost:3306/amplifier"
    username: "root"
    password: "password"
    pool-size: 10

  # MongoDB Configuration (only used if type is MONGODB)
  mongodb:
    uri: "mongodb://localhost:27017"
    database: "amplifier"
    collection: "voice_players"
    pool-size: 10

# Redis Configuration for cross-server broadcasting
redis:
  # Whether to enable Redis for cross-server broadcasting
  enabled: false
  # Redis connection URI (e.g., redis://localhost:6379)
  uri: "redis://localhost:6379"
  # Redis password (leave empty for no password)
  password: ""
  # Channel name for voice broadcasting
  channel: "amplifier:voice"
  # Server identifier (must be unique across all servers)
  server-id: null
```

### Voice Chat Settings

- **max-distance**: Default voice chat range in blocks (default: 48)
- **enabled**: Whether voice chat is globally enabled
- **debug**: Enable debug logging for troubleshooting

### Storage Configuration

#### Local Storage (Default)
```yaml
storage:
  type: "LOCAL"
```
Data is stored in local files. No additional setup required.

#### MySQL Storage
```yaml
storage:
  type: "MYSQL"
  mysql:
    url: "jdbc:mysql://localhost:3306/amplifier"
    username: "your_username"
    password: "your_password"
    pool-size: 10
```

#### MongoDB Storage
```yaml
storage:
  type: "MONGODB"
  mongodb:
    uri: "mongodb://localhost:27017"
    database: "amplifier"
    collection: "voice_players"
    pool-size: 10
```

### Redis Configuration (Cross-Server)

To enable cross-server voice broadcasting:

```yaml
redis:
  enabled: true
  uri: "redis://your-redis-server:6379"
  password: "your_redis_password"  # Leave empty if no password
  channel: "amplifier:voice"
  server-id: null  # Auto-generated if null
```

## Commands

### Available Commands

| Command | Permission | Description |
|---------|------------|-------------|
| `/startbroadcasting [player]` | `lodestone.amplifier.commands.startbroadcasting` | Start broadcasting voice |
| `/stopbroadcasting [player]` | `lodestone.amplifier.commands.stopbroadcasting` | Stop broadcasting voice |
| `/setvoicedistance <distance> [player]` | `lodestone.amplifier.commands.setvoicedistance` | Set voice distance |
| `/setvolume <volume> [player]` | `lodestone.amplifier.commands.setvolume` | Set voice volume |
| `/setpitch <pitch> [player]` | `lodestone.amplifier.commands.setpitch` | Set voice pitch |
| `/mutevoicechat [player]` | `lodestone.amplifier.commands.mutevoicechat` | Mute a player's voice |
| `/unmutevoicechat [player]` | `lodestone.amplifier.commands.unmutevoicechat` | Unmute a player's voice |
| `/setglobalvoicedistance <distance>` | `lodestone.amplifier.commands.setglobalvoicedistance` | Set global voice distance |
| `/setdeafened <true/false> [player]` | `lodestone.amplifier.commands.setdeafened` | Set player as deafened |
| `/muteglobalvoicechat` | `lodestone.amplifier.commands.muteglobalvoicechat` | Mute all voice chat |
| `/unmuteglobalvoicechat` | `lodestone.amplifier.commands.unmuteglobalvoicechat` | Unmute all voice chat |
| `/setreverb <true/false> [player]` | `lodestone.amplifier.commands.setreverb` | Enable/disable reverb |
| `/reloadamplifier` | `lodestone.amplifier.commands.reload` | Reload configuration |

### Permission Groups

#### Basic Permissions
- `lodestone.amplifier.bypass` - Bypass voice chat restrictions
- `lodestone.amplifier.commands.*` - Access to all commands

#### Command Permissions
- `lodestone.amplifier.commands.startbroadcasting`
- `lodestone.amplifier.commands.stopbroadcasting`
- `lodestone.amplifier.commands.setvoicedistance`
- `lodestone.amplifier.commands.setvolume`
- `lodestone.amplifier.commands.setpitch`
- `lodestone.amplifier.commands.mutevoicechat`
- `lodestone.amplifier.commands.unmutevoicechat`
- `lodestone.amplifier.commands.setglobalvoicedistance`
- `lodestone.amplifier.commands.setdeafened`
- `lodestone.amplifier.commands.muteglobalvoicechat`
- `lodestone.amplifier.commands.unmuteglobalvoicechat`
- `lodestone.amplifier.commands.setreverb`
- `lodestone.amplifier.commands.reload`

## Management

### Voice Chat Management

#### Enable/Disable Voice Chat
```yaml
voice-chat:
  enabled: true  # Set to false to disable globally
```

#### Set Global Voice Distance
```bash
/setglobalvoicedistance 64
```

#### Mute/Unmute Global Voice Chat
```bash
/muteglobalvoicechat
/unmuteglobalvoicechat
```

### Player Management

#### Individual Player Settings
- **Voice Distance**: `/setvoicedistance <distance> [player]`
- **Volume**: `/setvolume <volume> [player]`
- **Pitch**: `/setpitch <pitch> [player]`
- **Mute/Unmute**: `/mutevoicechat [player]` / `/unmutevoicechat [player]`
- **Deafen**: `/setdeafened <true/false> [player]`
- **Reverb**: `/setreverb <true/false> [player]`

#### Broadcasting
- **Start Broadcasting**: `/startbroadcasting [player]`
- **Stop Broadcasting**: `/stopbroadcasting [player]`

### Cross-Server Setup

1. **Install Redis** on a server accessible by all your Minecraft servers
2. **Configure Redis** in each server's `config.yml`:
   ```yaml
   redis:
     enabled: true
     uri: "redis://your-redis-server:6379"
     password: "your_password"
     channel: "amplifier:voice"
   ```
3. **Ensure unique server IDs** - Amplifier generates these automatically
4. **Restart all servers** to apply changes

## Troubleshooting

### Common Issues

#### Voice Chat Not Working
1. Ensure Simple Voice Chat is installed and working
2. Check that Amplifier is properly loaded
3. Verify voice chat is enabled in config
4. Check server logs for errors

#### Redis Connection Issues
1. Verify Redis server is running
2. Check network connectivity
3. Verify credentials and URI
4. Check firewall settings

#### Storage Issues
1. For MySQL: Verify database exists and credentials are correct
2. For MongoDB: Verify connection URI and database permissions
3. Check server logs for connection errors

### Debug Mode

Enable debug mode to get detailed logging:

```yaml
voice-chat:
  debug: true
```

### Logs

Check your server logs for Amplifier-related messages:
- `[Amplifier]` - General plugin messages
- `[Amplifier] ERROR` - Error messages
- `[Amplifier] DEBUG` - Debug messages (when enabled)

## Performance Optimization

### Storage Recommendations
- **Small servers (< 50 players)**: Use LOCAL storage
- **Medium servers (50-200 players)**: Use MySQL or MongoDB
- **Large servers (> 200 players)**: Use MySQL with proper indexing

### Redis Performance
- Use a dedicated Redis server for production
- Configure Redis persistence for data safety
- Monitor Redis memory usage

### General Tips
- Regularly restart servers to clear memory
- Monitor plugin performance with server monitoring tools
- Keep Amplifier updated to the latest version 