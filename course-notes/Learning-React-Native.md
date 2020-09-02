# Learning React Native

## Getting Started

Need xcode installed for iOS dev

**need homebrew installed!**

install watchman

```bash
brew install watchman
```

install RN CLI

```bash
sudo npm i -g react-native-cli

```

### Create the app

```bash
react-native init NAme_of_app
```

**Run iOS**

```bash
react-native run-ios
```

### Building the iOS Index file

Doesn't render HTML
Use new set of ui tags

```js
import { View, Text } from "react-native";
```

### Creating Stylesheets

```js
const styles = StyleSheet.create({
  defaultComponent: {
    style: 10,
  },
});
```

### Images

import the same as modules

import `<Image>` from `react-native`

can add styles to the images as well

use `source={import}` attribute to place the image

Use Dimensions from React native to get the width of the screen

### Responding to touches

Use `<Text>` components and style them like buttons.

add `onPress={}` attribute to text elements

### TouchableHighlight

Make a cooler looking touchable using multiple components.

import the `<TouchableHighlight>` from react-native

use `onPress`

### Use the Scroll View

when something grows out of the view

when you have a lot of content you want to use a `ScrollView`

### Work with the List View

efficiently manages long lists of Data

**needs a datasource for it to work**

```js
this.ds = new ListView.DataSource({
  rowHasChanged: (r1, r2) => r1 !== r2,
});

// in state
dataSource: this.ds.cloneWithRows(listOfStuff);
```

user `renderRow` to render a componenet for each value

user `renderHeader` to make a nice header for the list
