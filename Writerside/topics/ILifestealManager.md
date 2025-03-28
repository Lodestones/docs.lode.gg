# ILifestealManager
This instance can be obtained by calling `IObserverAPI#getLifestealManager()`.
```java
/**
 * Sets whether lifesteal is enabled.
 *
 * @param value True to enable, false to disable
 */
void setEnabled(boolean value);

/**
 * Checks if lifesteal is enabled.
 *
 * @return True if enabled, false otherwise
 */
boolean isEnabled();

/**
 * Sets the custom name of the lifesteal item.
 *
 * @param itemName The name of the item
 */
void setItemName(String itemName);

/**
 * Gets the custom name of the lifesteal item.
 *
 * @return The item name
 */
String getItemName();

/**
 * Sets the custom model data value for the lifesteal item.
 *
 * @param modelData The model data
 */
void setModelData(int modelData);

/**
 * Gets the custom model data value for the lifesteal item.
 *
 * @return The model data
 */
int getModelData();

/**
 * Sets whether lifesteal hearts should be stackable.
 *
 * @param stackable True if stackable, false otherwise
 */
void setStackable(boolean stackable);

/**
 * Checks if lifesteal hearts are stackable.
 *
 * @return True if stackable, false otherwise
 */
boolean isStackable();

/**
 * Sets the type of lifesteal behavior.
 *
 * @param lifestealType The {@link LifestealType}
 */
void setLifestealType(LifestealType lifestealType);

/**
 * Gets the type of lifesteal behavior.
 *
 * @return The {@link LifestealType}
 */
LifestealType getLifestealType();

/**
 * Sets the maximum amount of health a player can reach via lifesteal.
 *
 * @param maxHealth The max health value
 */
void setMaxHealth(double maxHealth);

/**
 * Gets the maximum amount of health a player can reach via lifesteal.
 *
 * @return The max health value
 */
double getMaxHealth();

/**
 * Sets the minimum amount of health a player can have via lifesteal.
 *
 * @param minHealth The min health value
 */
void setMinHealth(double minHealth);

/**
 * Gets the minimum amount of health a player can have via lifesteal.
 *
 * @return The min health value
 */
double getMinHealth();

/**
 * Sets whether players are allowed to withdraw lifesteal hearts.
 *
 * @param canWithdraw True to allow withdrawing, false to disallow
 */
void setCanWithdraw(boolean canWithdraw);

/**
 * Checks if players are allowed to withdraw lifesteal hearts.
 *
 * @return True if withdrawal is allowed, false otherwise
 */
boolean canWithdraw();
```
