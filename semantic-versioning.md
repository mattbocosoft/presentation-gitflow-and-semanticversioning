##Semantic Versioning  

![semantic-versioning](images/semantic-versioning.png)  

Semantic Versioning is an attempt to, as it's name suggests, standardize the *meaning* as well as syntax of version numbers. The [main webpage of the Semantic Versioning project](http://semver.org) declares that the goal of the project is to deal with 'dependency hell'. Indeed, Semantic Versioning is a very popular versioning convention adopted by [CocoaPods](https://github.com/mattbocosoft/presentation-cocoapods) and allows product developers to be able to count on the backwards-compatibility of dependency updates.  

Semantic Versioning formalizes the versioning system that many products already use in an informal way. Organizations often increment the major number when the change 'feels' big, or the minor number when the change 'feels' minor, however this methodology is not exact; "Without compliance to some sort of formal specification, version numbers are essentially useless for dependency management". [Not everyone agrees](https://gist.github.com/jashkenas/cbd2b088e20279ae2c8e) with the practice of Semantic Versioning, arguing that Semantic Versioning "prioritize[s] a mechanistic understanding of a codebase over a human one".  

There are many unique methods of assigning versions to product releases, and each organization has it's own unique style. Here are some example  
1. OS X: Apple uses a two-component version number (e.g. 10.11) combined with a natural language name (e.g. "El Capitan").  
2. iOS uses a three-component version number much like Semantic Versioning, and may in fact be *using* Semantic Versioning    
3. Android uses [three different versions](https://en.wikipedia.org/wiki/Android_version_history) for each release, e.g. 4.4–4.4.4 Android KitKat (API level 19)  

###Beginning Development  

The initial version of a product or library using Semantic Versioning starts at 0.1.0. Since all changes are potentially break backwards-compatibility, it does make sense to increase the major version until release, so the product does not increase to 1.0.0 until the first public release. If the software is already in use, then the version number should already be at or above 1.0.0  

###Major  
The Major number should be incremented when backward-*incompatible* functionality is introduced in the release. This indicates to the consumers of the software or library that they need to be prepared to change their integration methods with the software or library.  

The release that corresponds to an increment in the major version may also include changes that are minor or patch level.  

The Minor and Patch numbers must be reset to 0 when the Minor number is incremented.  

###Minor  
The Minor number should be incremented when new backwards-compatible functionality is introduced in the release. This indicates to consumers of the software or library that they can safely upgrade to the latest Minor release without having to worry about backwards-compatibility issues.  

The release that corresponds to an increment in the minor version may also include changes that are patch level, but not major level.  

The Patch number must be reset to 0 when the Minor number is incremented.  

###Patch  
The Patch number should be incremented when backwards-compatible bug-fixes is introduced in the release. This indicates to consumers of the software or library that they can safely upgrade to the latest Patch release without having to worry about backwards-compatibility issues.  

###Pre-Release  
Pre-release numbers are appended after the Patch number following a dash. They can include any number of components separated by a dot. An example of a version with a pre-release number is 1.4.2-beta.2  

###References  
[http://semver.org](http://semver.org)  
