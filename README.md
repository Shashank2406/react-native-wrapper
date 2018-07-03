# Native Module: react-native-helloworld
Getting started to write React Native bridge module for Android.

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