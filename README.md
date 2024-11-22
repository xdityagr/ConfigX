![Alt text](https://github.com/xdityagr/ConfigX/blob/main/assets/banner1.png?raw=true "Banner Image")

# ConfigX  
 
- **Config X** is a powerful, flexible, and easy-to-use settings manager built around the concept of **keypaths**.

- It is as powerful as a mini DBMS, but lightweight, simple to use and develop with. 

- Config X is made to ensure easy and quick configuration of applications such a creating a settings file, managing it's data, caching, & other important but simple implementations involving CRUD operations on data, etc. 

***What ConfigX does, is blazing fast and soooo simple, that even your grandma could manage a server with it (if she wanted to). 🚀***

---

## Introduction  
ConfigX is a powerful, flexible, and easy-to-use settings manager built around the concept of **keypaths**.  
A **keypath** is a dot-separated string representing the hierarchy of keys in a dictionary, enabling quick access and modifications.  

### What is a Keypath?  
Imagine your settings file is like a box inside a box inside *another* box:  

```python
data = {'fridge': {'shelf': {'item': 'cake', 'quantity': 1}, 'temperature': -2}}
```  

Now, instead of fumbling through boxes like:  
**"Where's that cake again?"**  

You simply use a *keypath*, like a magical treasure map:  
```python
keypath = 'fridge.shelf.item'
```  
**Result?** You instantly find your `'cake'` 🍰 without breaking a sweat.

Or change things up:  
```python
keypath = 'fridge.temperature=-5'
```  
**Boom!** The fridge is now colder ❄️ and your ice cream stays frosty.  

### Why ConfigX?

ConfigX is designed for **huge settings files** or **structured key-value data** in formats like JSON, YAML, or similar. Whether you're building an app with an overwhelming number of settings or managing complex nested data, ConfigX makes it **quick and easy** to access, modify, and organize your settings.

- **No more digging through massive files**: Simply reference settings with a **keypath** like a GPS for your data.
- **Save time**: Stop dealing with repetitive code to access deeply nested data. ConfigX does it for you with blazing speed.
- **Reduce complexity**: Instead of managing countless function calls or manually navigating through levels of data, ConfigX lets you manage everything through intuitive and simple keypath-based queries.

It's perfect for:

- **App settings**: Whether it’s themes, user preferences, or system configurations.
- **Huge configuration files**: Get access to deeply nested configurations with minimal code.
- **Key-value storage management**: Organize your settings just like a database without the hassle.

With ConfigX, your settings management becomes a breeze, saving you time and reducing complexity.
### Features

- **Keypath-based Access**: Access or modify settings with simple keypaths (e.g., `appearance.theme`).
- **Fast & Simple**: Blazing fast keypath resolution and updates.
- **Deeply Nested Structures**: Handle complex nested data with ease.
- **Data Type Enforcement**: Ensure correct data types for settings.
- **Backup & Restore**: Backup and restore specific settings or keypaths.
- **Observers & Callbacks**: Automatically trigger functions when settings change.
- **Auto Encryption**: Encrypt sensitive settings for extra security.
- **Lazy Loading**: Efficiently load large settings files when needed.
- **Import/Export/Merge**: Easily import, export, and merge settings.
- **Autocompletion**: CLI autocompletion for easier keypath access.
- **Version Control**: Track and revert changes to settings.

### Usage Example

```python
# Create an instance of ConfigX
ocs = ConfigX()

# Get the current theme
ocs.resolve('app.ui.theme')  # Output: 'dark'

# Change the theme
ocs.resolve('app.ui.theme=light')  # Output: 'light'

# Set user language preference
ocs.resolve('user.language=en')  # Output: 'en'

# Toggle dark mode
ocs.resolve('app.ui.darkMode=True')  # Output: True

# Backup the user language setting
ocs.backup('user.language')

```

## Stay Tuned
ConfigX is still in it's development phase, stay tuned for it's release! 🚀

## Contact

For questions or feedback, please contact:

- **Email**: adityagaur.home@gmail.com
- **GitHub**: [xdityagr](https://github.com/xdityagr)

**ConfigX** is coming soon! 
