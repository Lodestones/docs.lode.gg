# Events

### PreGameStateChangeEvent
This event is called whenever Observer's game state is about to change.<br />
You can cancel this event to prevent the game state from changing.
```java
    @EventHandler
    public void onPreGameStateChange(PreGameStateChangeEvent event) {
        GameState newState = event.getNewState();
        GameState oldState = event.getOldState();
        
        if (newState == GameState.LOBBY) {
            // Do something when the game state is about to change to LOBBY
        }
    }
```

## GameStateChangeEvent
This event is called whenever Observer's game state changes.<br />
It is important to note that you cannot cancel this event.
```java
    @EventHandler
    public void onGameStateChange(GameStateChangeEvent event) {
        @Nullable Player source = event.getSource(); // The player who changed the game state
        GameState newState = event.getNewState();
        GameState oldState = event.getOldState();
        
        if (newState == GameState.LOBBY) {
            // Do something when the game state changes to LOBBY
        }
    }
```

## PrePedestalCraftEvent
This event is called whenever a player is about to craft an item on a pedestal.<br />
You can cancel this event to prevent the player from crafting the item.
```java
    @EventHandler
    public void onPrePedestalCraft(PrePedestalCraftEvent event) {
        Player player = event.getPlayer(); // The player who is crafting the item
        String pedestalId = event.getPedestalId(); // The ID of the pedestal
        boolean isCancelled = event.isCancelled(); // Whether the event is cancelled
        
        if (pedestalId.equalsIgnoreCase("my_pedestal")) {
            // Do something when the player is about to craft an item on a pedestal with the ID "my_pedestal"
        }
    }
```

## PedestalCraftEvent
This event is called whenever a player crafts an item on a pedestal.<br />
```java
    @EventHandler
    public void onPedestalCraft(PedestalCraftEvent event) {
        Player player = event.getPlayer(); // The player who crafted the item
        String pedestalId = event.getPedestalId(); // The ID of the pedestal
        Result result = event.getResult(); // The result of the crafting
        ItemStack itemStack = event.getItem(); // The item that was crafted
        
        if (result == Result.SUCCESS) {
            player.sendMessage(Component.text("You crafted an item!"));
        }
    }
```

## PlayerEliminatedEvent
This event is called whenever a player is eliminated from the game.<br />
You can cancel this event to prevent the player from being eliminated.<br />
**IMPORTANT: To override a death event, you need to set the EventPriority to `LOWEST` or `LOW`.**
```java
    @EventHandler
    public void onPlayerEliminated(PlayerEliminatedEvent event) {
        Player player = event.getPlayer(); // The player who was eliminated
        @Nullable LivingEntity killer = event.getKiller(); // The entity that eliminated the player
        boolean isCancelled = event.isCancelled(); // Whether the event is cancelled
        Component message = event.getMessage(); // The message that will be broadcasted in chat
        PlayerDeathEvent deathEvent = event.getDeathEvent(); // The bukkit player death event
        List<ItemStack> drops = event.getDrops(); // The items that will be dropped
        
        if (source != null) {
            source.sendMessage(Component.text("You eliminated " + player.getName() + "!"));
        }
    }
```

## PlayerReviveEvent
This event is called whenever a player is revived.<br />
You can cancel this event to prevent the player from being revived.
```java
    @EventHandler
    public void onPlayerRevive(PlayerReviveEvent event) {
        Player player = event.getPlayer(); // The player who was revived
        boolean isCancelled = event.isCancelled(); // Whether the event is cancelled
        Location location = event.getLocation(); // The location where the player will be revived
        
        if (reviver != null) {
            reviver.sendMessage(Component.text("You revived " + player.getName() + "!"));
        }
    }
```