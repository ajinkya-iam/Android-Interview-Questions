# Android-Interview-Questions

### 1. What is the difference between a fragment and an activity in Android?
> In Android, an activity represents a single screen with a user interface with which the user can interact, while a fragment represents a portion of an activity's user interface or behavior that can be reused across multiple activities.

> The key difference between an activity and a fragment is that an activity can exist independently and be launched independently, while an activity must host a fragment. A single activity can host multiple fragments, and each fragment can be added, removed, or replaced at Android runtime based on the user's interaction.

> Another difference is that an activity has a life cycle of its own, while a fragment depends on its hosting activity's life cycle. When the hosting activity is destroyed, all its associated fragments are also destroyed.

### 2. What is the importance of the AndroidManifest.xml file in an Android application?
> The AndroidManifest.xml file is a key component of an Android application. It is an XML file that provides essential information about the application to the Android operating system. Some of the important roles that the AndroidManifest.xml file in the Android SDK plays are:

> **Declaring the application's package name:** The package name is a unique identifier for the application, and it is used to distinguish it from other applications installed on the device.
