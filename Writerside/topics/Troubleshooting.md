# Troubleshooting

This guide helps you resolve common issues with Amplifier. If you're experiencing problems, check this page first before seeking additional support.

## Quick Diagnostic Checklist

Before diving into specific issues, run through this checklist:

- [ ] Is Simple Voice Chat installed and working?
- [ ] Is Amplifier properly loaded (check server startup logs)?
- [ ] Are all dependencies installed (Java 17+, Paper/Spigot 1.21+)?
- [ ] Is the configuration file valid (no syntax errors)?
- [ ] Are permissions set up correctly?
- [ ] Is the storage backend (if using external) accessible?

## Common Issues

### Voice Chat Not Working

**Symptoms**:
- Players cannot hear each other
- Voice chat appears disabled
- No voice indicators

**Solutions**:

1. **Check Simple Voice Chat Installation**
   ```bash
   # Verify Simple Voice Chat is loaded
   /plugins
   # Look for "voicechat" in the list
   ```

2. **Verify Amplifier Integration**
   ```
   [Amplifier] INFO: Amplifier plugin has been enabled!
   [Amplifier] INFO: Voice chat service found and registered
   ```

3. **Check Voice Chat Status**
   ```bash
   # Check if voice chat is enabled globally
   /setglobalvoicedistance 48
   ```

4. **Enable Debug Mode**
   ```yaml
   voice-chat:
     debug: true
   ```
   Then restart the server and check logs for detailed information.

### Database Connection Issues

**Symptoms**:
- Players lose voice settings on restart
- Database connection errors in logs
- Plugin fails to start

**Solutions**:

#### MySQL Issues

1. **Connection Refused**
   ```
   [Amplifier] ERROR: Could not connect to MySQL database
   ```
   
   **Fix**:
   - Verify MySQL server is running
   - Check connection URL and credentials
   - Ensure database exists
   - Test connection manually:
     ```bash
     mysql -h localhost -u username -p database_name
     ```

2. **Authentication Failed**
   ```
   [Amplifier] ERROR: Access denied for user 'username'@'host'
   ```
   
   **Fix**:
   - Verify username and password
   - Check user permissions
   - Create dedicated user:
     ```sql
     CREATE USER 'amplifier'@'localhost' IDENTIFIED BY 'password';
     GRANT ALL PRIVILEGES ON amplifier.* TO 'amplifier'@'localhost';
     FLUSH PRIVILEGES;
     ```

3. **SSL Issues**
   ```
   [Amplifier] ERROR: SSL connection error
   ```
   
   **Fix**:
   ```yaml
   mysql:
     url: "jdbc:mysql://localhost:3306/amplifier?useSSL=false&allowPublicKeyRetrieval=true"
   ```

#### MongoDB Issues

1. **Connection Failed**
   ```
   [Amplifier] ERROR: Could not connect to MongoDB
   ```
   
   **Fix**:
   - Verify MongoDB server is running
   - Check connection URI
   - Test connection:
     ```bash
     mongo mongodb://localhost:27017/amplifier
     ```

2. **Authentication Issues**
   ```
   [Amplifier] ERROR: Authentication failed
   ```
   
   **Fix**:
   - Verify username/password in URI
   - Check authentication database
   - Create user if needed:
     ```javascript
     use admin
     db.createUser({
       user: "amplifier",
       pwd: "password",
       roles: [{ role: "readWrite", db: "amplifier" }]
     })
     ```

### Redis Connection Issues

**Symptoms**:
- Cross-server broadcasting not working
- Redis connection errors
- Server startup failures

**Solutions**:

1. **Connection Refused**
   ```
   [Amplifier] ERROR: Redis connection failed
   ```
   
   **Fix**:
   - Verify Redis server is running
   - Check Redis URI and port
   - Test connection:
     ```bash
     redis-cli ping
     ```

2. **Authentication Failed**
   ```
   [Amplifier] ERROR: Redis authentication failed
   ```
   
   **Fix**:
   - Verify password in configuration
   - Check Redis authentication settings
   - Test with password:
     ```bash
     redis-cli -a password ping
     ```

3. **Network Issues**
   ```
   [Amplifier] ERROR: Redis network timeout
   ```
   
   **Fix**:
   - Check firewall settings
   - Verify network connectivity
   - Use correct host/IP address

### Permission Issues

**Symptoms**:
- Commands not working
- "Permission denied" messages
- Players cannot use voice features

**Solutions**:

1. **Check Permission Setup**
   ```bash
   # Test permissions
   /lp user <player> permission check lodestone.amplifier.commands.startbroadcasting
   ```

2. **Common Permission Groups**
   ```bash
   # Admin permissions
   /lp group admin permission set lodestone.amplifier.commands.* true
   
   # Moderator permissions
   /lp group moderator permission set lodestone.amplifier.commands.mutevoicechat true
   /lp group moderator permission set lodestone.amplifier.commands.unmutevoicechat true
   /lp group moderator permission set lodestone.amplifier.commands.setdeafened true
   
   # Trusted player permissions
   /lp group trusted permission set lodestone.amplifier.commands.startbroadcasting true
   /lp group trusted permission set lodestone.amplifier.commands.stopbroadcasting true
   ```

3. **Bypass Permission**
   ```bash
   # Grant bypass for testing
   /lp user <player> permission set lodestone.amplifier.bypass true
   ```

### Performance Issues

**Symptoms**:
- High server lag
- Voice chat delays
- Memory usage spikes

**Solutions**:

1. **Optimize Connection Pools**
   ```yaml
   # For small servers
   mysql:
     pool-size: 5
   
   # For medium servers
   mysql:
     pool-size: 10
   
   # For large servers
   mysql:
     pool-size: 20
   ```

2. **Reduce Voice Distance**
   ```yaml
   voice-chat:
     max-distance: 32  # Reduce from default 48
   ```

3. **Disable Debug Mode**
   ```yaml
   voice-chat:
     debug: false  # Disable in production
   ```

4. **Use Local Storage for Small Servers**
   ```yaml
   storage:
     type: "LOCAL"  # Simpler, no network overhead
   ```

### Configuration Issues

**Symptoms**:
- Plugin fails to start
- Configuration errors in logs
- Settings not applying

**Solutions**:

1. **Invalid YAML Syntax**
   ```
   [Amplifier] ERROR: Invalid configuration file
   ```
   
   **Fix**:
   - Check YAML syntax with online validator
   - Look for missing quotes, indentation issues
   - Backup and regenerate config if needed

2. **Configuration Version Mismatch**
   ```
   [Amplifier] WARNING: Configuration version mismatch
   ```
   
   **Fix**:
   - Delete config.yml and restart server
   - Plugin will generate new default configuration

3. **Missing Required Fields**
   ```
   [Amplifier] ERROR: Missing required configuration field
   ```
   
   **Fix**:
   - Check configuration documentation
   - Ensure all required fields are present
   - Use default configuration as template

## Debugging Steps

### Enable Debug Mode

1. **Edit Configuration**
   ```yaml
   voice-chat:
     debug: true
   ```

2. **Restart Server**
   ```bash
   /restart
   ```

3. **Check Logs**
   ```bash
   # Look for debug messages
   tail -f logs/latest.log | grep Amplifier
   ```

### Test Voice Chat

1. **Basic Test**
   ```bash
   # Test global voice distance
   /setglobalvoicedistance 48
   
   # Test player voice settings
   /setvoicedistance 32 <player>
   /setvolume 1.0 <player>
   ```

2. **Broadcasting Test**
   ```bash
   # Test broadcasting
   /startbroadcasting <player>
   
   # Verify broadcasting status
   # Player should be heard by all players
   
   # Stop broadcasting
   /stopbroadcasting <player>
   ```

3. **Mute Test**
   ```bash
   # Test mute functionality
   /mutevoicechat <player>
   
   # Verify player cannot be heard
   
   # Unmute player
   /unmutevoicechat <player>
   ```

### Database Testing

1. **MySQL Test**
   ```bash
   # Test connection
   mysql -h localhost -u username -p database_name -e "SELECT 1;"
   
   # Check tables
   mysql -h localhost -u username -p database_name -e "SHOW TABLES;"
   ```

2. **MongoDB Test**
   ```bash
   # Test connection
   mongo mongodb://localhost:27017/amplifier --eval "db.runCommand('ping')"
   
   # Check collections
   mongo mongodb://localhost:27017/amplifier --eval "db.getCollectionNames()"
   ```

3. **Redis Test**
   ```bash
   # Test connection
   redis-cli ping
   
   # Test with password
   redis-cli -a password ping
   ```

## Log Analysis

### Common Log Messages

| Message | Meaning | Action |
|---------|---------|--------|
| `[Amplifier] INFO: Plugin enabled` | Plugin loaded successfully | None needed |
| `[Amplifier] ERROR: Voice chat service not found` | Simple Voice Chat missing | Install Simple Voice Chat |
| `[Amplifier] ERROR: Database connection failed` | Storage backend issue | Check database configuration |
| `[Amplifier] ERROR: Redis connection failed` | Redis connectivity issue | Check Redis server |
| `[Amplifier] DEBUG: Voice packet processed` | Normal operation | None needed |
| `[Amplifier] WARNING: Configuration outdated` | Config needs update | Regenerate configuration |

### Log Locations

- **Server Logs**: `logs/latest.log`
- **Amplifier Logs**: `logs/Amplifier/` (if debug enabled)
- **Error Logs**: `logs/error.log`

### Log Filtering

```bash
# Filter Amplifier messages
grep "Amplifier" logs/latest.log

# Filter errors only
grep "ERROR.*Amplifier" logs/latest.log

# Filter debug messages
grep "DEBUG.*Amplifier" logs/latest.log

# Real-time monitoring
tail -f logs/latest.log | grep Amplifier
```

## Recovery Procedures

### Reset Player Data

If player voice settings are corrupted:

1. **Backup Current Data**
   ```bash
   cp plugins/Amplifier/data.yml plugins/Amplifier/data.yml.backup
   ```

2. **Clear Player Data**
   ```bash
   # For local storage
   rm plugins/Amplifier/data.yml
   
   # For MySQL
   mysql -u username -p database_name -e "DELETE FROM voice_players;"
   
   # For MongoDB
   mongo database_name --eval "db.voice_players.deleteMany({})"
   ```

3. **Restart Server**
   ```bash
   /restart
   ```

### Reset Configuration

If configuration is corrupted:

1. **Backup Current Config**
   ```bash
   cp plugins/Amplifier/config.yml plugins/Amplifier/config.yml.backup
   ```

2. **Delete Configuration**
   ```bash
   rm plugins/Amplifier/config.yml
   ```

3. **Restart Server**
   ```bash
   /restart
   # Plugin will generate new default configuration
   ```

### Database Recovery

1. **MySQL Recovery**
   ```sql
   -- Check database integrity
   CHECK TABLE voice_players;
   
   -- Repair if needed
   REPAIR TABLE voice_players;
   
   -- Reset auto-increment
   ALTER TABLE voice_players AUTO_INCREMENT = 1;
   ```

2. **MongoDB Recovery**
   ```javascript
   // Check database integrity
   db.runCommand({dbStats: 1})
   
   // Repair database
   db.repairDatabase()
   ```

## Getting Help

If you're still experiencing issues after trying these solutions:

1. **Gather Information**:
   - Server version and type
   - Amplifier version
   - Simple Voice Chat version
   - Java version
   - Relevant log entries
   - Configuration file (remove sensitive data)

2. **Check Known Issues**:
   - Review GitHub issues
   - Check Discord server
   - Search documentation

3. **Contact Support**:
   - Create detailed bug report
   - Include all gathered information
   - Describe exact steps to reproduce
   - Mention what you've already tried

## Prevention

### Regular Maintenance

1. **Backup Configuration**
   ```bash
   # Create backup script
   cp plugins/Amplifier/config.yml plugins/Amplifier/config.yml.$(date +%Y%m%d)
   ```

2. **Monitor Logs**
   ```bash
   # Set up log monitoring
   tail -f logs/latest.log | grep -E "(ERROR|WARN).*Amplifier"
   ```

3. **Test Regularly**
   ```bash
   # Test voice chat functionality
   /setglobalvoicedistance 48
   /startbroadcasting <testplayer>
   /stopbroadcasting <testplayer>
   ```

### Best Practices

1. **Use Appropriate Storage**
   - Local for single servers
   - MySQL for small networks
   - MongoDB for large networks

2. **Secure Connections**
   - Use SSL for database connections
   - Use strong passwords
   - Restrict network access

3. **Monitor Performance**
   - Watch server TPS
   - Monitor memory usage
   - Check database performance

4. **Keep Updated**
   - Update Amplifier regularly
   - Update Simple Voice Chat
   - Update server software 