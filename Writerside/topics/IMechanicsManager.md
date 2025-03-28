# IMechanicsManager
This instance can be obtained by calling `IObserverAPI#getMechanicsManager()`.

```java
/**
 * Gets the increased apple drop rate multiplier.
 *
 * @return The increased apple rate multiplier
 */
double increasedAppleRates();

/**
 * Checks if sleeping is allowed.
 *
 * @return True if sleeping is allowed, false otherwise
 */
boolean isSleepingAllowed();

/**
 * Checks if item enchanting is allowed.
 *
 * @return True if enchanting is allowed, false otherwise
 */
boolean canEnchantItems();

/**
 * Checks if anvils can be used.
 *
 * @return True if anvils can be used, false otherwise
 */
boolean canUseAnvils();

/**
 * Checks if ender chests can be used.
 *
 * @return True if ender chests can be used, false otherwise
 */
boolean canUseEnderChests();

/**
 * Checks if villagers can be bred.
 *
 * @return True if breeding villagers is allowed, false otherwise
 */
boolean canBreedVillagers();

/**
 * Checks if players can trade with villagers.
 *
 * @return True if trading is allowed, false otherwise
 */
boolean canTradeWithVillagers();

/**
 * Checks if respawn anchors can be used.
 *
 * @return True if respawn anchors can be used, false otherwise
 */
boolean canUseRespawnAnchors();

/**
 * Checks if bed bombing is allowed.
 *
 * @return True if bed bombing is allowed, false otherwise
 */
boolean canBedBomb();

/**
 * Checks if portal trapping is allowed.
 *
 * @return True if portal trapping is allowed, false otherwise
 */
boolean canPortalTrap();

/**
 * Checks if indirect PVP is allowed.
 *
 * @return True if indirect PVP is allowed, false otherwise
 */
boolean canIndirectPVP();

/**
 * Checks if global block decay is enabled.
 *
 * @return True if global block decay is enabled, false otherwise
 */
boolean shouldGlobalBlockDecay();

/**
 * Checks if spawners are unbreakable.
 *
 * @return True if spawners are unbreakable, false otherwise
 */
boolean isUnbreakableSpawners();

/**
 * Checks if better world border mechanics are enabled.
 *
 * @return True if better world borders are enabled, false otherwise
 */
boolean isBetterWorldBorder();

/**
 * Checks if world borders should be matched across dimensions.
 *
 * @return True if world borders should match, false otherwise
 */
boolean shouldMatchWorldBorders();

/**
 * Checks if potion brewing is allowed.
 *
 * @return True if potion brewing is allowed, false otherwise
 */
boolean canBrewPotions();

/**
 * Gets the combat logging manager.
 *
 * @return The {@link ICombatLoggingManager} instance
 */
IMechanicsManager.ICombatLoggingManager getCombatLoggingManager();

/**
 * Checks if entering the Nether is allowed.
 *
 * @return True if Nether is allowed, false otherwise
 */
boolean isNetherAllowed();

/**
 * Checks if entering the End is allowed.
 *
 * @return True if the End is allowed, false otherwise
 */
boolean isEndAllowed();

/**
 * Sets whether sleeping is allowed.
 *
 * @param sleepingAllowed True to allow sleeping, false to disallow
 */
void setSleepingAllowed(boolean sleepingAllowed);

/**
 * Sets whether item enchanting is allowed.
 *
 * @param enchantItems True to allow enchanting, false to disallow
 */
void setEnchantItems(boolean enchantItems);

/**
 * Sets whether anvils can be used.
 *
 * @param useAnvils True to allow anvils, false to disallow
 */
void setUseAnvils(boolean useAnvils);

/**
 * Sets whether ender chests can be used.
 *
 * @param useEnderChests True to allow, false to disallow
 */
void setUseEnderChests(boolean useEnderChests);

/**
 * Sets whether villagers can be bred.
 *
 * @param breedVillagers True to allow breeding, false to disallow
 */
void setBreedVillagers(boolean breedVillagers);

/**
 * Sets whether players can trade with villagers.
 *
 * @param tradeWithVillagers True to allow trading, false to disallow
 */
void setTradeWithVillagers(boolean tradeWithVillagers);

/**
 * Sets whether respawn anchors can be used.
 *
 * @param useRespawnAnchors True to allow, false to disallow
 */
void setUseRespawnAnchors(boolean useRespawnAnchors);

/**
 * Sets whether bed bombing is allowed.
 *
 * @param bedBomb True to allow, false to disallow
 */
void setBedBomb(boolean bedBomb);

/**
 * Sets whether portal trapping is allowed.
 *
 * @param portalTrap True to allow, false to disallow
 */
void setPortalTrap(boolean portalTrap);

/**
 * Sets whether indirect PVP is allowed.
 *
 * @param indirectPVP True to allow, false to disallow
 */
void setIndirectPVP(boolean indirectPVP);

/**
 * Sets whether global block decay should be enabled.
 *
 * @param globalBlockDecay True to enable, false to disable
 */
void setGlobalBlockDecay(boolean globalBlockDecay);

/**
 * Sets whether spawners are unbreakable.
 *
 * @param unbreakableSpawners True to make spawners unbreakable, false otherwise
 */
void setUnbreakableSpawners(boolean unbreakableSpawners);

/**
 * Sets whether better world borders should be enabled.
 *
 * @param betterWorldBorder True to enable, false to disable
 */
void setBetterWorldBorder(boolean betterWorldBorder);

/**
 * Sets whether world borders should be matched across dimensions.
 *
 * @param matchWorldBorders True to match, false to disable
 */
void setMatchWorldBorders(boolean matchWorldBorders);

/**
 * Sets whether potion brewing is allowed.
 *
 * @param brewPotions True to allow, false to disallow
 */
void setBrewPotions(boolean brewPotions);

/**
 * Sets whether entering the Nether is allowed.
 *
 * @param netherAllowed True to allow, false to disallow
 */
void setNetherAllowed(boolean netherAllowed);

/**
 * Sets whether entering the End is allowed.
 *
 * @param endAllowed True to allow, false to disallow
 */
void setEndAllowed(boolean endAllowed);
```

---

# ICombatLoggingManager
This instance can be obtained via `IMechanicsManager#getCombatLoggingManager()`.

```java
/**
 * Determines if players can combat log.
 *
 * @return True if combat logging is possible, false otherwise
 */
boolean canCombatLog();

/**
 * Gets the combat timer duration in seconds.
 *
 * @return The combat timer
 */
int getCombatTimer();

/**
 * Gets the display type used to show the combat timer.
 *
 * @return The {@link DisplayType}
 */
DisplayType getDisplayType();

/**
 * Gets the raw display message shown while in combat.
 *
 * @return The display message
 */
String getDisplayMessage();

/**
 * Gets the translation key for the combat notification.
 *
 * @return The combat notification translation key
 */
String getCombatNotificationTranslation();
```
