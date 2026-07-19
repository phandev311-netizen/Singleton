# Unity Singleton Collection

A lightweight collection of Singleton implementations for Unity projects.

This repository contains three different Singleton patterns, each designed for a different use case.

## Included Classes

- Singleton<T>
- SingletonBehaviour<T>
- SingletonSelfBehaviour<T>

---

# 1. Singleton<T>

A generic Singleton for **regular C# classes**.

### Features

- Lazy initialization
- Automatically creates the instance using `new T()`
- No Unity dependency
- Simple and lightweight

### Best For

- SaveData
- ConfigManager
- GameSettings
- Utility classes
- Cache classes

### Example

```csharp
public class SaveManager : Singleton<SaveManager>
{
    public int Gold = 100;
}
```

Access anywhere:

```csharp
SaveManager.Instance.Gold += 100;
```

---

# 2. SingletonBehaviour<T>

A Singleton designed for **MonoBehaviour**.

### Features

- Searches existing objects in the scene
- Automatically creates a GameObject if none exists
- Prevents multiple instances (logs an error)
- Easy global access

### Best For

- GameManager
- AudioManager
- UIManager
- PoolManager
- EffectManager

### Example

```csharp
public class AudioManager : SingletonBehaviour<AudioManager>
{
    public void PlayClick()
    {
        Debug.Log("Click");
    }
}
```

Usage

```csharp
AudioManager.Instance.PlayClick();
```

If there is no AudioManager in the scene, one will be created automatically.

---

# 3. SingletonSelfBehaviour<T>

A lightweight Singleton for MonoBehaviour.

### Features

- Searches an existing object in the scene
- Does NOT create a new object
- Reports an error if no instance exists

### Best For

Objects that **must already exist** in the scene.

Example:

```csharp
public class GameManager : SingletonSelfBehaviour<GameManager>
{

}
```

Usage

```csharp
GameManager.Instance.StartGame();
```

If GameManager doesn't exist in the scene, an error is logged.

---

# Comparison

| Feature | Singleton<T> | SingletonBehaviour<T> | SingletonSelfBehaviour<T> |
|----------|--------------|-----------------------|---------------------------|
| Regular C# Class | ✅ | ❌ | ❌ |
| MonoBehaviour | ❌ | ✅ | ✅ |
| Auto Create Instance | ✅ | ✅ | ❌ |
| Search Scene | ❌ | ✅ | ✅ |
| Uses `new T()` | ✅ | ❌ | ❌ |

---

# Which One Should I Use?

### Use **Singleton<T>**

When your class is NOT a MonoBehaviour.

Examples:

- SaveManager
- ConfigManager
- LocalizationManager

---

### Use **SingletonBehaviour<T>**

When you want a MonoBehaviour that automatically exists.

Examples:

- AudioManager
- UIManager
- PoolManager
- EffectManager

---

### Use **SingletonSelfBehaviour<T>**

When the object is manually placed in the scene and should never be auto-created.

Examples:

- GameManager
- LevelManager
- CameraManager

---

# Advantages

- Easy global access
- Reduces object references
- Cleaner code
- Lightweight
- Generic implementation

---

# Notes

These classes are intentionally kept simple.

Depending on your project, you may want to extend them with features such as:

- `DontDestroyOnLoad`
- Thread safety
- Duplicate instance destruction
- Scene persistence
- Better initialization order

---

# License

MIT License

Feel free to use, modify and improve these classes in your own Unity projects.
