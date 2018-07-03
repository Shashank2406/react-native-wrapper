# Native Module: react-native-helloworld
Getting started to write React Native bridge module for Android.
We start by creating a native module. A native module is a Java class that usually extends the ReactContextBaseJavaModule class and implements the functionality required by the JavaScript. Our goal here is to be able to write MyModule.alert('Hello World'); from JavaScript to display a short toast on the screen.

create a new Java Class named MyModule.java inside android/app/src/main/java/com/your-app-name/ folder with the content below:

// MyModule.java

```java
package com.custom.helloworld;

import android.widget.Toast;

import com.facebook.react.bridge.NativeModule;
import com.facebook.react.bridge.ReactApplicationContext;
import com.facebook.react.bridge.ReactContext;
import com.facebook.react.bridge.ReactContextBaseJavaModule;
import com.facebook.react.bridge.ReactMethod;

import java.util.Map;
import java.util.HashMap;

public class MyModule extends ReactContextBaseJavaModule {

  public ToastModule(ReactApplicationContext reactContext) {
    super(reactContext);
  }
}
```
ReactContextBaseJavaModule requires that a method called getName is implemented. The purpose of this method is to return the string name of the NativeModule which represents this class in JavaScript. So here we will call this ToastExample so that we can access it through React.NativeModules.MyModule in JavaScript.
```java
  @Override
  public String getName() {
    return "MyModule";
  }
```
To expose a method to JavaScript a Java method must be annotated using @ReactMethod. The return type of bridge methods is always void. React Native bridge is asynchronous, so the only way to pass a result to JavaScript is by using callbacks or emitting events (see below).
```java
  @ReactMethod
  public void show(String message, int duration) {
    Toast.makeText(getReactApplicationContext(), message, Toast.LENGTH_LONG).show();
  }
``` 

## How to Run the Example

```bash
cd Example
npm install
react-native run-android
```

## How to Use the Module
1. Create a new React Native project:

    ```bash
    react-native init NewProject
    ```
2. Add the local module to dependencies in **package.json**: 

    ```json
    "dependencies": {
		"react": "16.0.0-alpha.6",
		"react-native": "0.43.3",
		"react-native-helloworld":"file:../"
	},
    ```
3. Link dependencies:

    ```bash
    react-native link
    ```
4. Use the module in **index.android.js**:

    ```javascript
    import MyModule from 'react-native-helloworld';

    const onButtonPress = () => {
        MyModule.alert('Hello World');
    };
    ```
