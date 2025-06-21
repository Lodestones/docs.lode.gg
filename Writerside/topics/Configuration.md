# Configuration

This page provides detailed information about all configuration options available in Amplifier.

## Configuration File Location

The main configuration file is located at:
```
plugins/Amplifier/config.yml
```

## Configuration Structure

### Basic Configuration

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
    # Database URL (e.g., jdbc:mysql://localhost:3306/amplifier)
    url: "jdbc:mysql://localhost:3306/amplifier"
    # Database username
    username: "root"
    # Database password
    password: "password"
    # Connection pool size
    pool-size: 10

  # MongoDB Configuration (only used if type is MONGODB)
  mongodb:
    # Connection URI (e.g., mongodb://localhost:27017)
    uri: "mongodb://localhost:27017"
    # Database name
    database: "amplifier"
    # Collection name
    collection: "voice_players"
    # Connection pool size
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
  # This is generated automatically by the plugin
  server-id: null
```

## Voice Chat Settings

### `voice-chat.max-distance`

**Type**: `float`  
**Default**: `48.0`  
**Range**: `0.0` to unlimited  
**Description**: The maximum distance in blocks that players can hear each other's voices.

**Examples**:
```yaml
voice-chat:
  max-distance: 32    # Short range voice chat
  max-distance: 48    # Default range
  max-distance: 64    # Long range voice chat
  max-distance: -1    # Unlimited distance
```

### `voice-chat.enabled`

**Type**: `boolean`  
**Default**: `true`  
**Description**: Whether voice chat is globally enabled. When disabled, only players with the `lodestone.amplifier.bypass` permission can speak.

**Examples**:
```yaml
voice-chat:
  enabled: true   # Voice chat is enabled for all players
  enabled: false  # Voice chat is disabled (bypass permission required)
```

### `voice-chat.debug`

**Type**: `boolean`  
**Default**: `false`  
**Description**: Enables debug logging for troubleshooting voice chat issues.

**Examples**:
```yaml
voice-chat:
  debug: false  # Normal logging
  debug: true   # Detailed debug logging
```

## Storage Configuration

### Storage Types

Amplifier supports three storage backends for player voice data:

#### Local Storage (Default)

**Type**: `LOCAL`  
**Description**: Stores data in local files. Best for small to medium servers.

```yaml
storage:
  type: "LOCAL"
```

**Pros**:
- No external dependencies
- Simple setup
- Good performance for small servers

**Cons**:
- Not suitable for multiple servers
- Data not shared between server instances

#### MySQL Storage

**Type**: `MYSQL`  
**Description**: Stores data in a MySQL database. Best for medium to large servers.

```yaml
storage:
  type: "MYSQL"
  mysql:
    url: "jdbc:mysql://localhost:3306/amplifier"
    username: "amplifier_user"
    password: "secure_password"
    pool-size: 10
```

**Configuration Options**:

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `url` | `string` | Required | JDBC connection URL |
| `username` | `string` | Required | Database username |
| `password` | `string` | Required | Database password |
| `pool-size` | `int` | `10` | Connection pool size |

**URL Examples**:
```yaml
mysql:
  url: "jdbc:mysql://localhost:3306/amplifier"                    # Local database
  url: "jdbc:mysql://192.168.1.100:3306/amplifier"               # Remote database
  url: "jdbc:mysql://db.example.com:3306/amplifier?useSSL=false" # Remote with SSL disabled
```

**Pros**:
- Shared data across multiple servers
- ACID compliance
- Good performance
- Familiar technology

**Cons**:
- Requires MySQL server setup
- Additional maintenance

#### MongoDB Storage

**Type**: `MONGODB`  
**Description**: Stores data in a MongoDB database. Best for large scale deployments.

```yaml
storage:
  type: "MONGODB"
  mongodb:
    uri: "mongodb://localhost:27017"
    database: "amplifier"
    collection: "voice_players"
    pool-size: 10
```

**Configuration Options**:

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `uri` | `string` | Required | MongoDB connection URI |
| `database` | `string` | Required | Database name |
| `collection` | `string` | Required | Collection name |
| `pool-size` | `int` | `10` | Connection pool size |

**URI Examples**:
```yaml
mongodb:
  uri: "mongodb://localhost:27017"                                    # Local database
  uri: "mongodb://192.168.1.100:27017"                               # Remote database
  uri: "mongodb://user:pass@db.example.com:27017/amplifier"          # With authentication
  uri: "mongodb://user:pass@db1.example.com:27017,db2.example.com:27017/amplifier?replicaSet=rs0"  # Replica set
```

**Pros**:
- Excellent scalability
- Flexible schema
- Good for large datasets
- Built-in replication

**Cons**:
- Requires MongoDB setup
- Different query language
- More complex than MySQL

### Storage Recommendations

| Server Size | Recommended Storage | Reason |
|-------------|-------------------|---------|
| < 50 players | LOCAL | Simple, no external dependencies |
| 50-200 players | MySQL | Good balance of features and simplicity |
| > 200 players | MongoDB | Better scalability and performance |

## Redis Configuration

### Cross-Server Broadcasting

Redis enables voice broadcasting across multiple servers in a network.

### `redis.enabled`

**Type**: `boolean`  
**Default**: `false`  
**Description**: Whether to enable Redis for cross-server voice broadcasting.

```yaml
redis:
  enabled: true   # Enable cross-server broadcasting
  enabled: false  # Disable cross-server broadcasting
```

### `redis.uri`

**Type**: `string`  
**Default**: `"redis://localhost:6379"`  
**Description**: Redis connection URI.

**Examples**:
```yaml
redis:
  uri: "redis://localhost:6379"                    # Local Redis
  uri: "redis://192.168.1.100:6379"               # Remote Redis
  uri: "redis://user:pass@redis.example.com:6379" # With authentication
  uri: "rediss://redis.example.com:6380"          # SSL connection
```

### `redis.password`

**Type**: `string`  
**Default**: `""` (empty)  
**Description**: Redis password for authentication.

```yaml
redis:
  password: ""              # No password
  password: "my_password"   # With password
```

### `redis.channel`

**Type**: `string`  
**Default**: `"amplifier:voice"`  
**Description**: Redis channel name for voice broadcasting messages.

```yaml
redis:
  channel: "amplifier:voice"        # Default channel
  channel: "myserver:voice"         # Custom channel
  channel: "network:voice:lobby"    # Server-specific channel
```

### `redis.server-id`

**Type**: `string`  
**Default**: `null` (auto-generated)  
**Description**: Unique server identifier. Automatically generated if not specified.

```yaml
redis:
  server-id: null                    # Auto-generated
  server-id: "lobby-server"          # Custom server ID
  server-id: "survival-01"           # Descriptive server ID
```

## Configuration Examples

### Small Server (Local Storage)

```yaml
# Amplifier Plugin Configuration
version: 1

# Voice Chat Settings
voice-chat:
  max-distance: 32
  enabled: true
  debug: false

# Storage Settings
storage:
  type: "LOCAL"

# Redis Configuration (disabled for single server)
redis:
  enabled: false
```

### Medium Server (MySQL)

```yaml
# Amplifier Plugin Configuration
version: 1

# Voice Chat Settings
voice-chat:
  max-distance: 48
  enabled: true
  debug: false

# Storage Settings
storage:
  type: "MYSQL"
  mysql:
    url: "jdbc:mysql://localhost:3306/amplifier"
    username: "amplifier_user"
    password: "secure_password_123"
    pool-size: 15

# Redis Configuration (disabled)
redis:
  enabled: false
```

### Large Network (MongoDB + Redis)

```yaml
# Amplifier Plugin Configuration
version: 1

# Voice Chat Settings
voice-chat:
  max-distance: 64
  enabled: true
  debug: false

# Storage Settings
storage:
  type: "MONGODB"
  mongodb:
    uri: "mongodb://user:pass@db.example.com:27017"
    database: "amplifier"
    collection: "voice_players"
    pool-size: 20

# Redis Configuration for cross-server broadcasting
redis:
  enabled: true
  uri: "redis://user:pass@redis.example.com:6379"
  password: "redis_password"
  channel: "network:voice"
  server-id: "survival-01"
```

### Development Server (Debug Enabled)

```yaml
# Amplifier Plugin Configuration
version: 1

# Voice Chat Settings
voice-chat:
  max-distance: 48
  enabled: true
  debug: true  # Enable debug logging

# Storage Settings
storage:
  type: "LOCAL"

# Redis Configuration
redis:
  enabled: false
```

## Configuration Management

### Reloading Configuration

To reload the configuration without restarting the server:

```bash
/reloadamplifier
```

### Configuration Validation

Amplifier validates the configuration on startup and will show errors for invalid settings:

```
[Amplifier] ERROR: Invalid MySQL URL: jdbc:mysql://invalid-host:3306/amplifier
[Amplifier] ERROR: Redis connection failed: Connection refused
[Amplifier] ERROR: Invalid storage type: INVALID_TYPE
```

### Configuration Migration

When updating Amplifier, the configuration version is checked:

```
[Amplifier] WARNING: Configuration version mismatch. Expected: 2, Found: 1
[Amplifier] INFO: Configuration will be updated automatically
```

## Performance Tuning

### Connection Pool Sizes

**MySQL**:
```yaml
mysql:
  pool-size: 10   # Small server (< 50 players)
  pool-size: 15   # Medium server (50-200 players)
  pool-size: 25   # Large server (> 200 players)
```

**MongoDB**:
```yaml
mongodb:
  pool-size: 10   # Small server
  pool-size: 20   # Medium server
  pool-size: 30   # Large server
```

### Voice Distance Optimization

```yaml
voice-chat:
  max-distance: 32   # Dense player areas (spawn, cities)
  max-distance: 48   # Balanced gameplay
  max-distance: 64   # Open world exploration
  max-distance: 96   # Large open areas
```

### Debug Mode Impact

Enable debug mode only when troubleshooting:

```yaml
voice-chat:
  debug: false  # Production (better performance)
  debug: true   # Development/troubleshooting (more logging)
```

## Security Considerations

### Database Security

**MySQL**:
```yaml
mysql:
  username: "amplifier_user"           # Dedicated user
  password: "strong_password_123"      # Strong password
  url: "jdbc:mysql://localhost:3306/amplifier?useSSL=true"  # Enable SSL
```

**MongoDB**:
```yaml
mongodb:
  uri: "mongodb://user:pass@localhost:27017/amplifier?authSource=admin&ssl=true"
```

### Redis Security

```yaml
redis:
  password: "strong_redis_password"    # Always use passwords
  uri: "rediss://redis.example.com:6380"  # Use SSL when possible
```

### Network Security

- Use firewalls to restrict database access
- Use VPNs for remote database connections
- Regularly update passwords
- Monitor access logs

## Troubleshooting Configuration

### Common Issues

1. **Database Connection Failed**
   - Check database server is running
   - Verify connection credentials
   - Check network connectivity
   - Ensure database exists

2. **Redis Connection Failed**
   - Verify Redis server is running
   - Check authentication credentials
   - Test network connectivity
   - Verify Redis version compatibility

3. **Invalid Configuration**
   - Check YAML syntax
   - Verify all required fields are present
   - Ensure values are within valid ranges
   - Check for typos in option names

### Debug Configuration

```yaml
voice-chat:
  debug: true  # Enable detailed logging

storage:
  type: "MYSQL"
  mysql:
    url: "jdbc:mysql://localhost:3306/amplifier?useSSL=false&allowPublicKeyRetrieval=true"
    username: "root"
    password: "password"
    pool-size: 5

redis:
  enabled: true
  uri: "redis://localhost:6379"
  password: ""
  channel: "amplifier:voice"
  server-id: "test-server"
```

### Configuration Backup

Always backup your configuration before making changes:

```bash
cp plugins/Amplifier/config.yml plugins/Amplifier/config.yml.backup
```

### Configuration Validation Script

Create a simple validation script:

```bash
#!/bin/bash
# validate_config.sh

CONFIG_FILE="plugins/Amplifier/config.yml"

if [ ! -f "$CONFIG_FILE" ]; then
    echo "Configuration file not found: $CONFIG_FILE"
    exit 1
fi

# Check YAML syntax
if command -v python3 &> /dev/null; then
    python3 -c "import yaml; yaml.safe_load(open('$CONFIG_FILE'))" 2>/dev/null
    if [ $? -eq 0 ]; then
        echo "Configuration file syntax is valid"
    else
        echo "Configuration file has syntax errors"
        exit 1
    fi
else
    echo "Python3 not available, skipping syntax validation"
fi

echo "Configuration validation complete"
``` 