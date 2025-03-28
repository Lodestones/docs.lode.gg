# IEliminationManager
This instance can be obtained by calling `IObserverAPI#getEliminationManager()`.
```java
/**
 * Checks if elimination is enabled.
 *
 * @return True if elimination is enabled, false otherwise
 */
boolean isEnabled();

/**
 * Sets whether elimination is enabled.
 *
 * @param enabled True to enable elimination, false to disable
 */
void setEnabled(boolean enabled);

/**
 * Gets the death message shown when a player is eliminated.
 *
 * @return The death message
 */
String getDeathMessage();

/**
 * Sets the death message shown when a player is eliminated.
 *
 * @param deathMessage The death message
 */
void setDeathMessage(String deathMessage);

/**
 * Gets the kick message shown when a player is kicked upon elimination.
 *
 * @return The kick message
 */
String getKickMessage();

/**
 * Sets the kick message shown when a player is kicked upon elimination.
 *
 * @param kickMessage The kick message
 */
void setKickMessage(String kickMessage);

/**
 * Checks if auto-kick is enabled upon player elimination.
 *
 * @return True if auto-kick is enabled, false otherwise
 */
boolean isAutoKickEnabled();

/**
 * Sets whether auto-kick should be enabled upon player elimination.
 *
 * @param autoKickEnabled True to enable auto-kick, false to disable
 */
void setAutoKickEnabled(boolean autoKickEnabled);

/**
 * Gets the permission node that allows a player to bypass auto-kick.
 *
 * @return The auto-kick bypass permission
 */
String getAutoKickBypass();

/**
 * Sets the permission node that allows a player to bypass auto-kick.
 *
 * @param autoKickBypass The auto-kick bypass permission
 */
void setAutoKickBypass(String autoKickBypass);

/**
 * Checks if a lightning strike should occur when a player is eliminated.
 *
 * @return True if lightning should strike, false otherwise
 */
boolean shouldLightningOnKill();

/**
 * Sets whether a lightning strike should occur when a player is eliminated.
 *
 * @param lightningOnKill True to enable lightning, false to disable
 */
void setLightningOnKill(boolean lightningOnKill);

/**
 * Gets the game mode that a player will be set to upon death.
 *
 * @return The game mode on death
 */
GameMode getGamemodeOnDeath();

/**
 * Sets the game mode that a player will be set to upon death.
 *
 * @param gamemode The game mode to set
 */
void setGamemodeOnDeath(GameMode gamemode);

/**
 * Checks if players should automatically respawn upon elimination.
 *
 * @return True if auto-respawn is enabled, false otherwise
 */
boolean isAutoRespawn();

/**
 * Sets whether players should automatically respawn upon elimination.
 *
 * @param autoRespawn True to enable auto-respawn, false to disable
 */
void setAutoRespawn(boolean autoRespawn);
```
