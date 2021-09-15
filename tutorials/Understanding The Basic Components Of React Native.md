## Understanding The Basic Components Of React Native

[Original Tutorial](https://habiletechnologies.com/blog/understanding-the-basic-components-of-react-native/)

![Logo](https://habiletechnologies.com/wp-content/uploads/2017/02/reactnative.jpg)

The motto of react native is “Learn once write everywhere“. React native is like React,
however instead of using web components, it uses native components. You need to understand
some of the basic react components like JSX, components, state and props.

### Hello World Program

Let’s start with a basic Hello world program, and I assume that you’ve done the [Environment setup](https://reactnative.dev/docs/environment-setup)
for react native. To create the first sample app by using:

```sh
react native init NativeSample
```

Open the NativeSample project on your favorite IDE, and you will find the file called
index.android.js open the file and erase everything in that file. Let’s begin with our
own code. Paste the below code or type in the index.android.js

```jsx
import React, {Component} from 'react';
import {AppRegistry, Text, View} from 'react-native';

export default class NativeSample extends Component {
  render() {
    return (
      <View>
        <Text>Hello World!</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);

```

Run this using the command **react-native run-android**. You will see the screen like below (assuming there are no errors)

![Hello World Example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487829950.png)

You maybe think what these lines are. Let’s discuss the code one by one, In react native we want to import all the things we need because react native won’t import anything by default.In the first line, we import React and Component from react

**Component** - A component is a very basic element in react-native we can divide the large application into many small Components. This makes development fast and maintains the code very clear to understand.

**AppRegistry** - The JS entry point for all React native app is AppRegistry. In AppRegistry the app root Component should be registered. Then only react native loads the app and then run the app by invoking the AppRegistry.runApplication.

**Text** - Text is a basic built-in Component, it displays text in the Application.

**Render** - Content inside the render only displays in the Application screen.

### Core components of the React Native

#### 1. View

In React, View is a built-in component. If you familiar with div in HTML, view is
like div, it is used in mobile apps. The view is a content area where you display
your content.Using this you can arrange the content in a very good manner.

#### Usage of view  

- When you need to wrap your content inside the container
- When you need to use different style for different element  
- When you need a nested element
- It supports for Synthetic touch events, which is used for different purpose.

Example:

```jsx
import React, {Component} from 'react';
import {AppRegistry, Text, View} from 'react-native';

export default class NativeSample extends Component {
  render() {
    return (
      <View style={{backgroundColor: 'blue', margin: 5}}>
        <Text>Parent View</Text>

        <View style={{backgroundColor: 'red', margin: 5}}>
          <Text>first Child view</Text>

          <View style={{backgroundColor: 'green', margin: 5}}>
            <Text>Second Child view</Text>
          </View>
        </View>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);

```

Result:

![View Example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830411.png)

#### 2. State

There are two types of data which controls a component. They are state and props.
The state is mutable. It means a state can change the value at any time. The variable
data are stored in state. Initialize the state in a constructor and change the value
by calling the function ‘setState’ when you want.

Example 1:

```jsx
import React, {Component} from 'react';
import {AppRegistry, Text, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: 'It display using state',
    };
  }

  render() {
    return (
      <View>
        <Text> {this.state.firstVar}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Here we initialize a variable firstVar using state.

Result:

![State Example 1](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830524.png)

Example 2:

```jsx
import React, {Component} from 'react';
import {AppRegistry, Text, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: 'It display using state',
    };
  }

  hideText = () => {
    this.setState({firstVar: 'Updated State! ^___^'});
  };

  render() {
    return (
      <View>
        <Text onPress={this.hideText}>{this.state.firstVar}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Here we update the variable firstVar when the text is pressed.

#### 3. props

The second data type is props. It is immutable. It can be used to pass
the data to the different component. It makes a connection between
Container Component and Presentation Component.

Container Component is where we handle all the states and functionalities,
and Presentation Component is where View present it is a passive area.

Initialization of the state and update of the state are handled in
container component. The result will be passed to the presentation
component to display the view by using the props

Example:

Container component:

```jsx
import React, {Component} from 'react';
import {AppRegistry, View} from 'react-native';

import PresentationalComponent from './presentationalComponent';

class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: 'It display using state',
    };
  }

  hideText = () => {
    this.setState({firstVar: 'Updated State O_o'});
  };

  render() {
    return (
      <View style={{backgroundColor: 'blue'}}>
        <PresentationalComponent
          myText={this.state.firstVar}
          deleteText={this.hideText}
        />
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Presentation Component (presentationalComponent.js):

```jsx
import React from 'react';
import {Text, View} from 'react-native';

const PresentationalComponent = props => {
  return (
    <View>
      <Text onPress={props.deleteText}>{props.myText}</Text>
    </View>
  );
};

export default PresentationalComponent;
```

We can create many presentation components using one container component.
Props help to communicate between the components

#### 4. Style

The most important thing in web or mobile app is styling. It makes our
application attractive. We don’t need any special language or syntax for
styling. You can style your application by using the javascript object.
All components accept the props style.We can pass the style by changing
the CSS properties with camel case like ‘backgroundcolor- backgroundColor’.
You can also use inline style but it’s not a good practice.The best way to
create styleSheet object is,

Example 1:

*Inline style*

