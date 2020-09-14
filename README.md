# configur8r
A simple YAML configuration class.

## Overview
Configur8r provides a simple class for loading, modifying, and saving configuration settings to and from various common configuration file formats including:
- YAML
- JSON
- CONF

The Config class provides an abstraction which allows the developer to simply modify values in whatever file-type is preferred, while maintaining consistent syntax across configuration types.  As a byproduct of this abstraction, a configuration may be converted from one type to another with relative ease, so long as the general structure of the configuration file does not extend beyond the complexity of a <code>plain object</code>.  
 
Internally, and upon all file saves, 
+ configuration keys are normalized into a camelCase/PascalCase, 
+ all common namespace separators('/ \\ , : ;') are normalized to dot('.')s, 
+ repeated separators are collapsed to a single instance of a dot,
+ and namespace keys (eg: <code>'org.orgName.platform.setting'</code>) are processed into <code>plain object</code>s (eg: <code>{ org: { orgName: { platform: { setting: 42} } } };</code>).

## Usage:
```javascript
// FIRST: require the class.
const Config = require("configur8r")

// NEXT: initialize your config object
var config = new Config('path/to/config/file.(yaml|json|conf)')

// Use chain-settings to more easily and readably set key-value pairs
config.set('settingName', 'value')
      .set('sectionName.settingName', 'Some other Value')
      .set(['section0', 'setting1'], 'A Random Value')

// Get the setting value with the same syntax, regardless of file-type.
let settingValue = config.get('settingName')

```
