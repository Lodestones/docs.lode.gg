# ICustomRecipesManager
This instance can be obtained by calling `IObserverAPI#getCustomRecipesManager()`.
```java
/**
 * Retrieves all recipes added through the manager.
 * 
 * @return A map of all added recipes, keyed by their {@link NamespacedKey}
 */
Map<NamespacedKey, Recipe> recipesAdded();

/**
 * Creates a new empty shaped recipe with the given ID and result.
 *
 * @param id The identifier for the recipe
 * @param result The resulting item of the recipe
 * @return A new {@link ShapedRecipe} instance
 */
ShapedRecipe newEmptyShaped(String id, ItemStack result);

/**
 * Creates a new empty shapeless recipe with the given ID and result.
 *
 * @param id The identifier for the recipe
 * @param result The resulting item of the recipe
 * @return A new {@link ShapelessRecipe} instance
 */
ShapelessRecipe newEmptyShapeless(String id, ItemStack result);

/**
 * Adds a shaped recipe to the recipe manager.
 *
 * @param recipe The shaped recipe to add
 * @throws RecipeAddException If the recipe could not be added
 */
void add(ShapedRecipe recipe) throws RecipeAddException;

/**
 * Adds a shapeless recipe to the recipe manager.
 *
 * @param recipe The shapeless recipe to add
 * @throws RecipeAddException If the recipe could not be added
 */
void add(ShapelessRecipe recipe) throws RecipeAddException;

/**
 * Removes a recipe by its ID.
 *
 * @param id The ID of the recipe to remove
 * @return True if the recipe was removed, false otherwise
 */
boolean remove(String id);

/**
 * Gets a recipe by its ID.
 *
 * @param id The ID of the recipe
 * @return The {@link Recipe} if found, or null otherwise
 */
@Nullable
Recipe get(String id);

/**
 * Reloads all recipes managed by the recipe manager.
 */
void reload();

/**
 * Saves all recipes managed by the recipe manager.
 */
void save();
```