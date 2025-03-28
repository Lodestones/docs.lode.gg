# ILateScatterManager
This instance can be obtained by calling `IObserverAPI#getLateScatterManager()`.
```java
/**
 * Checks if late scatter is enabled.
 *
 * @return True if late scatter is enabled, false otherwise
 */
boolean isEnabled();

/**
 * Sets whether late scatter is enabled.
 *
 * @param value True to enable, false to disable
 */
void setEnabled(boolean value);

/**
 * Gets the game mode assigned to players on late scatter.
 *
 * @return The game mode
 */
GameMode getGamemode();

/**
 * Sets the game mode assigned to players on late scatter.
 *
 * @param gamemode The game mode to set
 */
void setGamemode(GameMode gamemode);

/**
 * Gets the items that late scattered players will receive.
 *
 * @return An array of {@link ItemStack} given on late scatter
 */
ItemStack[] getItems();

/**
 * Sets the items that late scattered players will receive.
 *
 * @param contents The array of {@link ItemStack} to give
 */
void setItems(ItemStack[] contents);

/**
 * Sets the translation message shown to late scattered players.
 *
 * @param translation The translation key or message
 */
void setTranslation(String translation);

/**
 * Gets the translation message shown to late scattered players.
 *
 * @return The translation key or message
 */
String getTranslation();
```
