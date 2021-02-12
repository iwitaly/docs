---
description: Learn how to add Adapty React Native SDK to your project
---

# Installation

Run the installation command:

{% tabs %}
{% tab title="Yarn" %}
```bash
yarn add react-native-adapty
```
{% endtab %}

{% tab title="npm" %}
```
npm i react-native-adapty --save
```
{% endtab %}
{% endtabs %}

Install required iOS pods:

{% tabs %}
{% tab title="Bash" %}
```bash
cd ios && pod install && cd ../
```
{% endtab %}
{% endtabs %}

Update **`/android/build.gradle`** file. Make sure there is a **`kotlin-gradle-plugin:1.4.0`** dependency or newer:

{% tabs %}
{% tab title="Gradle" %}
{% code title="/android/build.gradle" %}
```diff
...
buildscript {
  ...
  dependencies {
    ...
    classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.4.0"
  }
}
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

Update **`android/app/build.gradle`** file. Make sure **`multiDex`** is enabled:

{% tabs %}
{% tab title="Gradle" %}
{% code title="/android/app/build.gradle" %}
```yaml
...
android {
  ...
  defaultConfig {
    ...
    multiDexEnabled true
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

 

