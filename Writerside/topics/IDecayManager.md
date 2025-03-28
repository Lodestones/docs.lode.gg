# IDecayManager
This instance can be obtained by calling `IObserverAPI#getDecayManager()`.
```java
/**
 * Marks a block for decay using world coordinates.
 *
 * @param world The world the block is in
 * @param x The X-coordinate of the block
 * @param y The Y-coordinate of the block
 * @param z The Z-coordinate of the block
 */
void markBlockForDecay(World world, int x, int y, int z);

/**
 * Marks a block for decay at a specific location.
 *
 * @param location The location of the block
 */
void markBlockForDecay(Location location);

/**
 * Marks a block for decay.
 *
 * @param block The block to mark
 */
void markBlockForDecay(Block block);

/**
 * Unmarks a block from decay using world coordinates.
 *
 * @param world The world the block is in
 * @param x The X-coordinate of the block
 * @param y The Y-coordinate of the block
 * @param z The Z-coordinate of the block
 */
void unmarkBlockForDecay(World world, int x, int y, int z);

/**
 * Unmarks a block from decay at a specific location.
 *
 * @param location The location of the block
 */
void unmarkBlockForDecay(Location location);

/**
 * Unmarks a block from decay.
 *
 * @param block The block to unmark
 */
void unmarkBlockForDecay(Block block);

/**
 * Checks if a block is marked for decay using world coordinates.
 *
 * @param world The world the block is in
 * @param x The X-coordinate of the block
 * @param y The Y-coordinate of the block
 * @param z The Z-coordinate of the block
 * @return True if the block is marked for decay, false otherwise
 */
boolean isMarkedForDecay(World world, int x, int y, int z);

/**
 * Checks if a block is marked for decay at a specific location.
 *
 * @param location The location of the block
 * @return True if the block is marked for decay, false otherwise
 */
boolean isMarkedForDecay(Location location);
```