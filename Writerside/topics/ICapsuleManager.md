# ICapsuleManager
This instance can be obtained by calling `IObserverAPI#getCapsuleManager()`.
```java
/**
 * Sets the capsules for the capsule manager
 * @param capsules The capsules
 */
void setCapsules(List<Capsule> capsules);

/**
 * Sets the capsule locations for the capsule manager
 * @param capsules The capsule locations
 */
void setCapsuleLocations(List<Location> capsules);

/**
 * Sets the capsule type for the capsule manager
 * @param capsuleType The capsule type
 */
void setCapsuleType(CapsuleType capsuleType);

/**
 * Checks if a player is in a capsule
 * @param player The player to check
 * @return True if the player is in a capsule
 */
boolean hasCapsule(Player player);

/**
 * Gets the capsule type
 * @return The capsule type
 */
CapsuleType getCapsuleType();

/**
 * Gets the capsule locations
 * @return The capsule locations
 */
List<Capsule> getCapsules();

/**
 * Removes a player from a capsule
 * @param player The player to remove
 */
void removePlayerFromCapsule(Player player);

/**
 * Sends all players to their capsules
 */
void sendPlayersToCapsules(@Nullable Player executor);

/**
 * Releases all players from their capsules
 */
void release();

/**
 * Saves the capsules to the configuration
 */
void save();

/**
 * Swaps the capsules of two players
 * @param player1 The first player
 * @param player2 The second player
 */
void swapCapsules(Player player1, Player player2);

/**
 * Reloads the capsules
 */
void reload();

/**
 * Sends a player to a capsule
 * @param player The player
 * @param capsule The capsule
 */
void sendPlayerToCapsule(Player player, Capsule capsule);
```