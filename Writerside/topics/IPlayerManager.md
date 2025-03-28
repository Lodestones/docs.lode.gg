# IPlayerManager
This instance can be obtained by calling `IObserverAPI#getPlayerManager()`.
```java
/**
 * Gets the player data for an online player.
 *
 * @param player The online {@link Player}
 * @return The {@link IPlayerData} associated with the player
 */
IPlayerData getPlayerData(Player player);

/**
 * Gets the player data for an offline player using their UUID.
 *
 * @param uniqueId The UUID of the player
 * @return The {@link IOfflinePlayerData} associated with the player
 */
IOfflinePlayerData getPlayerData(UUID uniqueId);

/**
 * Saves the data of a specific player.
 *
 * @param playerData The {@link IPlayerData} to save
 */
void save(IPlayerData playerData);

/**
 * Saves all player data currently in memory.
 */
void save();
```
