# ITranslationManager
This instance can be obtained by calling `IObserverAPI#getTranslationManager()`.
```java
/**
 * Translates a message using the given path key.
 *
 * @param path The path to the translation key
 * @return The {@link Translation} for the specified path
 */
Translation translate(String path);
```
