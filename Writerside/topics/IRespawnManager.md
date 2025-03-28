# IRespawnManager
This instance can be obtained by calling `IObserverAPI#getRespawnManager()`.
```java
/**
 * Respawns the given player using the specified respawn data.
 *
 * @param player The player to respawn
 * @param respawnData The {@link RespawnData} containing respawn settings
 */
void respawnPlayer(Player player, RespawnData respawnData);

/**
 * Checks if the respawn system is enabled.
 *
 * @return True if enabled, false otherwise
 */
boolean isEnabled();

/**
 * Sets whether the respawn system is enabled.
 *
 * @param enabled True to enable, false to disable
 */
void setEnabled(boolean enabled);
```
