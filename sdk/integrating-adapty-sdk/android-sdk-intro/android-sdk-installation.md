---
description: Learn how to install Adapty Android SDK via Gradle and configure Proguard
---

# Installation

You can install Adapty SDK via [Gradle](android-sdk-installation.md#install-via-gradle).



### Install via Gradle

Add the following to your top-level **`build.gradle`** at the end of repositories:

{% code title="top-level build.gradle" %}
```groovy
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
{% endcode %}

And then add the dependency to your module-level **`build.gradle`** at the end of dependencies:

{% code title="module-level build.gradle" %}
```groovy
dependencies {
    ...
    implementation 'com.github.adaptyteam:AdaptySDK-Android:0.8.6'
}
```
{% endcode %}



### Configure Proguard

You should add `-keep class com.adapty.** { *; }` to your Proguard configuration.

