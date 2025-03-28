# IPedestalManager
This instance can be obtained by calling `IObserverAPI#getPedestalManager()`.
```java
/**
 * Gets all registered pedestals and their configurations.
 *
 * @return A map of pedestal IDs to their {@link PedestalConfig}
 */
Map<String, PedestalConfig> getPedestals();

/**
 * Sets the number of uses a player has for a specific pedestal.
 *
 * @param id The pedestal ID
 * @param player The UUID of the player
 * @param uses The number of uses to set
 */
void setPedestalUses(String id, UUID player, int uses);

/**
 * Shows a specific pedestal to a player.
 *
 * @param id The pedestal ID
 * @param player The UUID of the player
 */
void showPedestalToPlayer(String id, UUID player);

/**
 * Hides a specific pedestal from a player.
 *
 * @param id The pedestal ID
 * @param player The UUID of the player
 */
void hidePedestalFromPlayer(String id, UUID player);

/**
 * Registers a new pedestal with the given configuration.
 *
 * @param id The pedestal ID
 * @param recipe The {@link PedestalConfig} to register
 */
void register(String id, PedestalConfig recipe);

/**
 * Unregisters a pedestal by its ID.
 *
 * @param id The pedestal ID
 * @return True if the pedestal was successfully unregistered, false otherwise
 */
boolean unregister(String id);

/**
 * Reloads all pedestal configurations.
 */
void reload();

/**
 * Saves all pedestal configurations.
 */
void save();
```
