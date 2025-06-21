# Developer API

The Amplifier API provides comprehensive access to voice chat functionality for plugin developers. This guide covers all available API methods, events, and integration patterns.

## Getting Started

### Dependencies

Add the Amplifier API to your project:

```xml
<dependency>
    <groupId>gg.lode</groupId>
    <artifactId>Amplifier-API</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```

### Repository

```xml
<repository>
    <id>lode-repo</id>
    <url>https://repo.lode.gg/releases</url>
</repository>
```

### Basic Usage

```java
import gg.lode.amplifierapi.AmplifierAPI;
import gg.lode.amplifierapi.IAmplifierAPI;

public class MyPlugin extends JavaPlugin {
    
    @Override
    public void onEnable() {
        // Get the API instance
        IAmplifierAPI api = AmplifierAPI.getApi();
        
        if (api != null) {
            // API is available
            getLogger().info("Amplifier API loaded successfully!");
        } else {
            // Amplifier is not installed
            getLogger().warning("Amplifier is not installed!");
        }
    }
}
```

## Core API

### IAmplifierAPI

The main API interface providing access to all Amplifier functionality.

```java
public interface IAmplifierAPI {
    IVoiceManager getVoiceManager();
    float getVoiceDistance();
    void setVoiceDistance(float distance);
    VoicechatServerApi getVoicechatApi();
}
```

#### Methods

- **`getVoiceManager()`**: Returns the voice manager for player operations
- **`getVoiceDistance()`**: Gets the global voice chat distance
- **`setVoiceDistance(float distance)`**: Sets the global voice chat distance
- **`getVoicechatApi()`**: Returns the underlying Simple Voice Chat API

### IVoiceManager

Manages voice player data and operations.

```java
public interface IVoiceManager {
    void cleanup();
    CompletableFuture<IVoicePlayer> fetchOrCreateVoicePlayer(Player player);
    IVoicePlayer getVoicePlayer(UUID uniqueId);
    IVoicePlayer getVoicePlayer(Player player);
    boolean isEnabled();
    void setEnabled(boolean enabled);
    void playSound(Location location, byte[] data);
    void playSound(Location location, byte[] data, float volume);
    void playSound(Location location, byte[] data, float volume, float distance);
    void playSound(Location location, byte[] data, float volume, float pitch, float distance);
}
```

#### Methods

- **`cleanup()`**: Clean up resources when shutting down
- **`fetchOrCreateVoicePlayer(Player player)`**: Get or create a voice player asynchronously
- **`getVoicePlayer(UUID uniqueId)`**: Get voice player by UUID
- **`getVoicePlayer(Player player)`**: Get voice player by Player object
- **`isEnabled()`**: Check if voice chat is enabled
- **`setEnabled(boolean enabled)`**: Enable or disable voice chat
- **`playSound(...)`**: Play custom sounds at specific locations

## Voice Player Management

### IVoicePlayer

Represents a player's voice settings and state.

```java
public interface IVoicePlayer {
    @Nullable Set<UUID> getWhoCanHear();
    void resetWhoCanHear();
    void addWhoCanHear(UUID uuid);
    void removeWhoCanHear(UUID uuid);
    void setWhoCanHear(@Nullable Set<UUID> whoCanHear);
    
    UUID getUniqueId();
    
    void setPitch(float pitch);
    void setVolume(float volume);
    float getVolume();
    float getPitch();
    
    float getDistance();
    void setDistance(float distance);
    
    void setBroadcasting(boolean isBroadcasting);
    boolean isBroadcasting();
    
    boolean shouldReverb();
    void setShouldReverb(boolean shouldReverb);
    
    boolean isDeafened();
    void setDeafened(boolean deafened);
}
```

### Player Management Examples

#### Getting Player Voice Settings

```java
IAmplifierAPI api = AmplifierAPI.getApi();
IVoiceManager voiceManager = api.getVoiceManager();

Player player = Bukkit.getPlayer("PlayerName");
IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);

// Get current settings
float volume = voicePlayer.getVolume();
float pitch = voicePlayer.getPitch();
float distance = voicePlayer.getDistance();
boolean isBroadcasting = voicePlayer.isBroadcasting();
boolean isDeafened = voicePlayer.isDeafened();
```

#### Modifying Player Settings

```java
IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);

// Set voice properties
voicePlayer.setVolume(1.5f);  // 150% volume
voicePlayer.setPitch(1.2f);   // Higher pitch
voicePlayer.setDistance(64f); // 64 block range

// Enable/disable features
voicePlayer.setBroadcasting(true);  // Enable broadcasting
voicePlayer.setDeafened(false);     // Enable hearing
voicePlayer.setShouldReverb(true);  // Enable reverb effect
```

#### Managing Who Can Hear

```java
IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);

// Add specific players who can hear this player
voicePlayer.addWhoCanHear(targetPlayer.getUniqueId());

// Remove players from hearing list
voicePlayer.removeWhoCanHear(targetPlayer.getUniqueId());

// Set custom hearing list
Set<UUID> hearingList = new HashSet<>();
hearingList.add(player1.getUniqueId());
hearingList.add(player2.getUniqueId());
voicePlayer.setWhoCanHear(hearingList);

// Reset to default hearing
voicePlayer.resetWhoCanHear();
```

## Sound Playback

### Playing Custom Sounds

```java
IVoiceManager voiceManager = api.getVoiceManager();

// Basic sound playback
Location location = player.getLocation();
byte[] audioData = getAudioData(); // Your audio data
voiceManager.playSound(location, audioData);

// With custom volume
voiceManager.playSound(location, audioData, 1.5f);

// With custom volume and distance
voiceManager.playSound(location, audioData, 1.5f, 32f);

// With custom volume, pitch, and distance
voiceManager.playSound(location, audioData, 1.5f, 1.2f, 32f);
```

### Audio Data Format

The audio data should be in the format expected by Simple Voice Chat (typically Opus-encoded audio).

## Events

### PlayerMicrophoneEvent

Fired when a player speaks into their microphone.

```java
@EventHandler
public void onPlayerMicrophone(PlayerMicrophoneEvent event) {
    Player player = event.player();
    VoicechatConnection connection = event.connection();
    MicrophonePacketEvent originalEvent = event.event();
    
    // Handle microphone input
    if (player.hasPermission("myplugin.voice.modify")) {
        // Modify the voice data or cancel the event
        // event.setCancelled(true);
    }
}
```

### Event Registration

```java
@Override
public void onEnable() {
    // Register event listener
    Bukkit.getPluginManager().registerEvents(this, this);
}

@EventHandler
public void onPlayerMicrophone(PlayerMicrophoneEvent event) {
    // Handle the event
}
```

## Integration Examples

### Voice Chat Modifier Plugin

```java
public class VoiceModifierPlugin extends JavaPlugin {
    
    @Override
    public void onEnable() {
        IAmplifierAPI api = AmplifierAPI.getApi();
        if (api == null) {
            getLogger().severe("Amplifier is required!");
            getServer().getPluginManager().disablePlugin(this);
            return;
        }
        
        // Register events
        Bukkit.getPluginManager().registerEvents(this, this);
    }
    
    @EventHandler
    public void onPlayerMicrophone(PlayerMicrophoneEvent event) {
        Player player = event.player();
        IVoicePlayer voicePlayer = AmplifierAPI.getApi()
            .getVoiceManager()
            .getVoicePlayer(player);
        
        // Apply custom effects based on player permissions
        if (player.hasPermission("voicemodifier.echo")) {
            voicePlayer.setShouldReverb(true);
        }
        
        if (player.hasPermission("voicemodifier.loud")) {
            voicePlayer.setVolume(2.0f);
        }
    }
}
```

### Broadcasting System

```java
public class BroadcastingPlugin extends JavaPlugin {
    
    @Override
    public void onEnable() {
        // Register command
        getCommand("broadcast").setExecutor(this);
    }
    
    @Override
    public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
        if (!(sender instanceof Player player)) {
            sender.sendMessage("This command can only be used by players!");
            return true;
        }
        
        IAmplifierAPI api = AmplifierAPI.getApi();
        if (api == null) {
            sender.sendMessage("Amplifier is not available!");
            return true;
        }
        
        IVoicePlayer voicePlayer = api.getVoiceManager().getVoicePlayer(player);
        
        if (args.length > 0 && args[0].equalsIgnoreCase("start")) {
            voicePlayer.setBroadcasting(true);
            player.sendMessage("Broadcasting started!");
        } else if (args.length > 0 && args[0].equalsIgnoreCase("stop")) {
            voicePlayer.setBroadcasting(false);
            player.sendMessage("Broadcasting stopped!");
        }
        
        return true;
    }
}
```

### Voice Chat Manager

```java
public class VoiceChatManager {
    
    private final IAmplifierAPI api;
    private final IVoiceManager voiceManager;
    
    public VoiceChatManager() {
        this.api = AmplifierAPI.getApi();
        this.voiceManager = api.getVoiceManager();
    }
    
    public void mutePlayer(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setVolume(0.0f);
    }
    
    public void unmutePlayer(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setVolume(1.0f);
    }
    
    public void setPlayerDistance(Player player, float distance) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setDistance(distance);
    }
    
    public void enableBroadcasting(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setBroadcasting(true);
    }
    
    public void disableBroadcasting(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setBroadcasting(false);
    }
    
    public void deafenPlayer(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setDeafened(true);
    }
    
    public void undeafenPlayer(Player player) {
        IVoicePlayer voicePlayer = voiceManager.getVoicePlayer(player);
        voicePlayer.setDeafened(false);
    }
}
```

## Best Practices

### Error Handling

```java
public class SafeAmplifierAPI {
    
    public static IVoicePlayer getVoicePlayerSafely(Player player) {
        IAmplifierAPI api = AmplifierAPI.getApi();
        if (api == null) {
            throw new IllegalStateException("Amplifier API is not available");
        }
        
        IVoiceManager voiceManager = api.getVoiceManager();
        if (voiceManager == null) {
            throw new IllegalStateException("Voice manager is not available");
        }
        
        return voiceManager.getVoicePlayer(player);
    }
    
    public static void setPlayerVolume(Player player, float volume) {
        try {
            IVoicePlayer voicePlayer = getVoicePlayerSafely(player);
            voicePlayer.setVolume(Math.max(0.0f, Math.min(5.0f, volume))); // Clamp between 0-5
        } catch (Exception e) {
            player.sendMessage("Failed to set volume: " + e.getMessage());
        }
    }
}
```

### Async Operations

```java
public class AsyncVoiceManager {
    
    public static CompletableFuture<IVoicePlayer> getVoicePlayerAsync(Player player) {
        return CompletableFuture.supplyAsync(() -> {
            IAmplifierAPI api = AmplifierAPI.getApi();
            if (api == null) {
                throw new RuntimeException("Amplifier API not available");
            }
            return api.getVoiceManager().getVoicePlayer(player);
        });
    }
    
    public static void applyVoiceSettingsAsync(Player player, Consumer<IVoicePlayer> settings) {
        getVoicePlayerAsync(player).thenAccept(voicePlayer -> {
            settings.accept(voicePlayer);
        }).exceptionally(throwable -> {
            player.sendMessage("Failed to apply voice settings: " + throwable.getMessage());
            return null;
        });
    }
}
```

### Configuration Integration

```java
public class VoiceConfig {
    
    private final FileConfiguration config;
    
    public VoiceConfig(JavaPlugin plugin) {
        this.config = plugin.getConfig();
    }
    
    public float getDefaultVolume() {
        return (float) config.getDouble("voice.default-volume", 1.0);
    }
    
    public float getDefaultDistance() {
        return (float) config.getDouble("voice.default-distance", 48.0);
    }
    
    public boolean isBroadcastingEnabled() {
        return config.getBoolean("voice.broadcasting-enabled", true);
    }
    
    public void applyDefaultSettings(Player player) {
        IAmplifierAPI api = AmplifierAPI.getApi();
        if (api == null) return;
        
        IVoicePlayer voicePlayer = api.getVoiceManager().getVoicePlayer(player);
        voicePlayer.setVolume(getDefaultVolume());
        voicePlayer.setDistance(getDefaultDistance());
    }
}
```

## Troubleshooting

### Common Issues

1. **API is null**: Ensure Amplifier is installed and loaded before your plugin
2. **Voice player not found**: Use `fetchOrCreateVoicePlayer()` for new players
3. **Permission issues**: Check that your plugin has the necessary permissions
4. **Async operations**: Use `CompletableFuture` for database operations

### Debug Information

```java
public class DebugUtils {
    
    public static void logVoicePlayerInfo(Player player) {
        IAmplifierAPI api = AmplifierAPI.getApi();
        if (api == null) {
            System.out.println("Amplifier API not available");
            return;
        }
        
        IVoicePlayer voicePlayer = api.getVoiceManager().getVoicePlayer(player);
        System.out.println("Player: " + player.getName());
        System.out.println("Volume: " + voicePlayer.getVolume());
        System.out.println("Pitch: " + voicePlayer.getPitch());
        System.out.println("Distance: " + voicePlayer.getDistance());
        System.out.println("Broadcasting: " + voicePlayer.isBroadcasting());
        System.out.println("Deafened: " + voicePlayer.isDeafened());
    }
}
``` 