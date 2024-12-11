![Alt text](https://github.com/xdityagr/ConfigX/blob/main/assets/banner1.png?raw=true "Banner Image")

# ConfigX Documentation
 
- Introducing **ConfigX**, the flexible, powerful and intuitive way of managing data. It is mainly a configuration tool for applications, that takes care of your app settings with ease and precision, but there are endless use cases ConfigX can be used to help manage data.


- Whether you're building a simple application or a large-scale system, **ConfigX** has you covered, offering a range of tools to manage configurations in a scalable, maintainable, and secure way.


- It can also be used like a Mini DBMS. 

***What ConfigX does, is blazing fast and soooo simple, that even your grandma could manage an app with it (if she wanted to). 🚀***


## 🛠️ Getting Started : 

Here’s a quick overview of the key methods in **ConfigX** to get you started:

```python
import ConfigX
confx = ConfigX()
```

### `confx.set_debug_mode(<[developer (default), deployed]>)` :

This method controls the level of debugging in **ConfigX** while developing applications.

- `developer`: Throws detailed exceptions; ideal for when you want to be precise and catch every error.

- `deployed`: Returns default values for missing keys, Basically safely manages data when application is actually deployed; Auto logging is enabled;

### `confx.resolve(<query>)`

This is the heart of **ConfigX**. Use this method resolve different **Keypath Managed Queries** to manipulate your data (create, update, delete, or retrieve).

# **🔑 Keypaths & ConfigXQL  :**

## **Keypaths**

- Keypaths refer to a structured way of referencing hierarchical data. Keypaths allow you to navigate through complex nested data structures like dictionaries, lists, and other objects, pointing to a specific value or a collection of values within those structures.

- Keypaths provide a way to identify and manage data without directly manipulating the underlying data structure. You can use them to access or modify values, create new values, or perform other operations such as deletion or updates. They are often used in configuration systems, data storage, and even UI frameworks where data is represented in a nested, tree-like format.

- ConfigX uses keypaths rigorously in each query; 

- Why Keypaths? : 

    ***Imagine your settings file is like a box inside a box inside another box:***

    ```python
    data = {'fridge': {'shelf': {'item': 'cake', 'quantity': 1},    'temperature': -2}}
    ```  

    Now, instead of fumbling through boxes like:  
    **"Where's that cake again?"**  

    You simply use a *keypath*, like a magical treasure map:  
    ```python
    keypath = 'fridge.shelf.item'
    # keypath = 'cake'
    ```  
    **Result?** You instantly find your `'cake'` 🍰 without breaking a sweat.

    Or change things up:  
    ```python
    keypath = 'fridge.temperature=-5'
    # keypath = -5

    ```  
    **Boom!** The fridge is now colder ❄️ and your ice cream stays frosty. Hence, As seen in this example it is *so easy* to access and play with values.

## **ConfigXQL :**
ConfigX uses a custom structured query language, called ConfigXQL (Yes, that's a play on SQL XD).
Don't worry, you don't need to spend hours learning this language. It's really natural, meaning it closely follows common sense and how you'd intuitively express your intentions, making it simple to understand and remember.

### Overview of ConfigXQL  :

- **Natural Syntax**: ConfigXQL is designed to feel natural and intuitive, like speaking plain English. You don’t need to memorize complex syntax.
- **Easy Setup**: It works with hierarchical keypath-based settings, so managing configurations is just a matter of referencing paths.
- **Flexible Data Handling**: You can use it to work with different data types like integers, strings, lists, dates, sets, and even complex objects!
- It works by using **Dot Notation's** to access paths. 

### 1. **Create a New Setting:**

```python
confx.resolve('appSettings')
```

Creates a new `appSettings` root. It's like adding a new folder to organize your settings.

### 2. **Create a Branch:**

```python
confx.resolve('appSettings.uisettings')
```

Adds a sub-branch, `uisettings`, under `appSettings`. It’s like adding a subfolder within a folder. Simple, yet effective.

### 3. **CRUD Operations on values:**

#### (i) **Create a New Value:**

```python
confx.resolve('appSettings.uisettings.userId:INT')
```

Creates a `userId` value with an `INT` type under `uisettings`. It’s like reserving a spot for something important.

```python
confx.resolve('appSettings.uisettings.isLoggedIn:BOOL=false')
```

Creates an `isLoggedIn` value with a default `false`. Every app needs to know if the user is logged in, right?

```python
confx.resolve('appSettings.uisettings.*[theme:STR="dark", keyboard-shortcuts:STR="ctrl+w"]')
```

Adds multiple settings in one go. Like batch processing, but without the stress.

#### (ii) **Updating Values:**

```python
confx.resolve('appSettings.uisettings.userId:STR="aditya"')
```

Updates `userId` to `"aditya"`. Simple, clean, and ready for the next phase.

```python
confx.resolve('appSettings.uisettings.userId="rohan"')
```

Here’s an update to `userId` again. Maybe it's time for a change; flexibility is key.

#### (iii) **Handle Dynamic Values:**

```python
confx.resolve('appSettings.uisettings.exampleSetting="exampleValue"')
```

Creates a value where the type is not predefined. It's flexible—just like your workflow.

#### (iv) **Get Values:**

- **Safe Retrieval:**

```python
confx.resolve('appSettings.uisettings.theme!')
```

This returns the value safely. If it doesn’t exist, you won’t get a nasty error; instead, you'll get an empty value.

- **Unsafe Retrieval:**

```python
confx.resolve('appSettings.uisettings.theme')
```

Retrieves the value directly. If it’s missing, expect an error. Use this method when you’re sure the value is critical.

#### (v) **Delete Values:**

```python
confx.resolve('appSettings.uisettings.theme-')
```

Deletes the `theme` setting. Because sometimes, it's just better to start fresh.

#### (vi) **Fallback/Reset:**

```python
confx.resolve('appSettings.!uisettings')
```

Resets the entire `uisettings` section to its default values. A nice reset button for when things go a little off-track.

---

# Features : 
## 🔄 1. Batch Transactions

You’ve got a lot to do, and sometimes you need to handle multiple changes at once. **ConfigX** lets you do that effortlessly.

### **Way 1:**

```python
confx.resolve('appSettings.theme=dark', 'appSettings.shortcuts=enabled')
```

Batch update multiple settings in one line. It’s quick and efficient, perfect for bulk operations.

### **Way 2:** (Much safer)

```python
with confx.transaction():
    confx.resolve('appSettings.theme=dark')
    confx.resolve('appSettings.shortcuts=enabled')
```

Wrap operations in a transaction for atomicity. Either all changes succeed, or none of them do. It’s like a safety net for your configurations.

---

## 2. 🛡️ Schema Validation : 

**ConfigX** doesn’t just let you manage settings—it ensures they’re correct, too. Schema validation ensures your configuration matches expected formats.

```python
schema = {
    "appSettings": {
        "uiSettings": {
            "theme": "STR",
        },
        "userInfo": {
         "userId": "INT",
         "userName": "STR" 
        }
    }
}
confx.validate(schema)
```

Validates your configuration structure against a schema. It’s like an extra layer of security to ensure everything is in order.

---

## 3. 🔒 Encryption : 

For sensitive data like passwords or API keys, **ConfigX** offers seamless encryption support.

```python
confx.resolve('appSettings.auth.password:ENCRYPTED="my_password"')
```

Anything marked as `ENCRYPTED` is automatically encrypted. Privacy is a priority, always.

---

## 📚 Supported Data Types

**ConfigX** supports a wide range of data types to cover virtually every use case:

- **INT**: Integer values
- **STR**: String values
- **LIST**: Lists of items
- **DICT**: Dictionaries for key-value pairs
- **NULL**: Represents null values
- **ENCRYPTED**: For sensitive, encrypted data
- **SET**: A collection of unique items
- **TUPLE**: Immutable ordered collections
- **Datetime**: Handle date and time with ease
- **UUID**: Universally unique identifiers
- **Path**: File paths (via `pathlib`)
- **GeoJSON**: For geospatial data
- **Color**: Color codes (because why not?)
- **Email**: For storing email addresses
- **Regex**: Regular expressions for pattern matching
- **IP Address**: Network-related data
- **Enum**: Predefined choices for consistency
- **Numpy Arrays**: For data science aficionados
- **Pandas DataFrames**: Because who doesn’t love pandas?
- **Custom Objects**: Create your own custom types

---

## ⚙️ How It All Fits Together

Here’s a quick example of how everything ties in:

```python
from configx import ConfigX
from datetime import datetime

confx = ConfigX()

# Create settings
confx.resolve('appSettings.theme:STR=light')

# Update settings dynamically
confx.resolve('appSettings.theme=dark')

# Encrypt sensitive data
confx.resolve('appSettings.auth.password:SENSITIVE="super_secret_password"')

# Batch operations
with confx.transaction():
    confx.resolve('appSettings.language=english')
    confx.resolve('appSettings.region=US')

# Validate schema
schema = {
    "appSettings": {
        "theme": "STR",
        "auth": {
            "password": "ENCRYPTED"
        }
    }
}
confx.validate(schema)
```

---

## 💡 Conclusion

- **ConfigX** is a versatile tool that brings power and precision to configuration management.
- Whether you need simple key-value pairs or complex data structures, **ConfigX** has you covered.
- With built-in validation, encryption, and batch processing, managing your app’s settings has never been easier or more secure.

---

## Stay Tuned
ConfigX is still in it's development phase, stay tuned for it's release! 🚀

For questions or feedback, please contact:
- **Email**: adityagaur.home@gmail.com


Made with ♥️ in India by [Aditya Gaur](https://github.com/xdityagr)
