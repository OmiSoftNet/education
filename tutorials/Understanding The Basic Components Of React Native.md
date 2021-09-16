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

```jsx
import React, {Component} from 'react';
import {AppRegistry, View, Text} from 'react-native';

class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: 'It displays using state',
    };
  }

  render() {
    return (
      <View style={{backgroundColor: 'blue'}}>
        <Text> {this.state.firstVar}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Example 2:

*Using styleSheet*

```jsx
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: 'It displays using styleSheet',
    };
  }

  render() {
    return (
      <View>
        <Text style={styles.textStyle}> {this.state.firstVar}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);

const styles = StyleSheet.create({
  textStyle: {
    margin: 50,
    fontSize: 30,
    color: 'red',
    fontWeight: 'bold',
  },
});
```

Result:

![styleSheet example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830700-196x337.png)

#### 5. Flex layout

Flex Layout is provided to give a clean layout to the component. Children of a component layout are specified using the Flexbox. Using the flexDirection, alignItems, and justifyContent properties we can archive the right layout

##### 5.1. flexDirection:

Values: ('row', 'column')

This property decides the primary axis of the layout. Component’s children should be organized

Horizontally (row) or Vertically (column). Default value is column

Example:

```jsx
import React, {Component} from 'react';

import {AppRegistry, View} from 'react-native';

export default class NativeSample extends Component {
  render() {
    return (
      <View style={{flex: 1, flexDirection: 'row'}}>
        <View style={{width: 50, height: 50, backgroundColor: 'blue'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'red'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'green'}} />
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Result:

![flexDirection Example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830770.png)

##### 5.2. justifyContent

JustifyContent determines the distribution of children in primary Axis.

Values:flex-start, center, flex-end, space-around, and space-between.

Space-between provide an equal space between the children

Example:

```jsx
import React, {Component} from 'react';
import {AppRegistry, View} from 'react-native';

export default class NativeSample extends Component {
  render() {
    return (
      <View
        style={{
          flex: 1,
          flexDirection: 'row',
          justifyContent: 'space-between',
        }}>
        <View style={{width: 50, height: 50, backgroundColor: 'blue'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'red'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'green'}} />
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

 Result:
 
 ![justifyContent example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830805.png)
 
##### 5.3. alignItems

alignItems determines the alignment of children in the secondary axis.

Values : (flex-start, center, flex-end, strecth)

- flex-start : align at the start
- center : align at the center,
- flex-end : lign at the end,
- stretch : stretched to fill.

Example:

```jsx
import React, {Component} from 'react';

import {AppRegistry, View} from 'react-native';

export default class NativeSample extends Component {
  render() {
    return (
      <View
        style={{
          flex: 1,
          flexDirection: 'row',
          justifyContent: 'space-between',

          alignItems: 'center',
        }}>
        <View style={{width: 50, height: 50, backgroundColor: 'blue'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'red'}} />

        <View style={{width: 50, height: 50, backgroundColor: 'green'}} />
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Result:

![alignItems example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830841.png)

#### 6. Handling text input

We use the basic component TextInput to get text input from the user. It has props
onChangeText, onSubmitEditing. onChangeText function is called whenever the text is changed.

onSubmitEditing is invoked when the text is submitted.

Example:

```jsx
import React, {Component} from 'react';

import {AppRegistry, Text, TextInput, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: ' ',
    };
  }

  render() {
    return (
      <View style={{margin: 50}}>
        <TextInput
          style={{height: 40}}
          placeholder="Type your text!"
          onChangeText={firstVar => this.setState({firstVar})}
        />

        <Text style={{padding: 10, fontSize: 42}}>{this.state.firstVar}</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Result:

![Handling text input example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487830905-200x337.png)

#### 7. scrollView

Scrollview used to render the large list or large content in view with a scrollbar.
It helps to view the large content.

Example:

```jsx
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, ScrollView, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: ' ',

      listvalue: [
        {name: 'list1', id: 1},
        {name: 'list2', id: 2},
        {name: 'list3', id: 3},
        {name: 'list4', id: 4},
        {name: 'list5', id: 5},
        {name: 'list6', id: 6},
        {name: 'list7', id: 7},
        {name: 'list8', id: 8},
        {name: 'list9', id: 9},
        {name: 'list10', id: 10},
        {name: 'list11', id: 11},
        {name: 'list12', id: 12},
      ],
    };
  }

  makeList = item => (
    <Text key={item.id} style={styles.list}>
      {item.name}
    </Text>
  );

  render() {
    return (
      <View
        style={{
          margin: 50,
          height: 500,
        }}>
        <Text>Scroll View</Text>

        <ScrollView>{this.state.listvalue.map(this.makeList)}</ScrollView>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);

const styles = StyleSheet.create({
  list: {
    margin: 15,
    padding: 5,
    height: 40,
    borderColor: 'red',
    borderWidth: 1,
  },
});

```

Result:

![scrollView example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487831144-199x337.png)

#### 8. FlatList (List View)

It is used to display the vertically scrolling list of changing data. It renders the dataSource array value to the view.

- dataSource is a model to listView.
- renderRow is used  to fetch the data from dataSource and render it to the view(screen)
- rowHasChanged it determines the row change.

Example:

```jsx
import React, {Component} from 'react';
import {AppRegistry, Text, FlatList, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      dataSource: [
        'row 1',
        'row 2',
        'row3',
        'row4',
        'row5',
        'row6',
        'row7',
        'row8',
      ],
    };
  }

  render() {
    return (
      <View
        style={{
          margin: 50,
          height: 500,
        }}>
        <Text>List View</Text>

        <FlatList
          data={this.state.dataSource}
          renderItem={({item}) => <Text>{item}</Text>}
        />
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);
```

Result:

![FlatList example](https://habiletechnologies.com/wp-content/uploads/2017/02/screenshot_1487831246-198x337.png)

#### 9. Networking

Most of the apps need to fetch data from remote URL. You maybe want to make POST
a request or simply fetch the data from another server. React provides fetch
function to make an HTTP request to another server. Catch the error throw by
fetch otherwise dropped by silently

Example:

```jsx
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, ScrollView, View} from 'react-native';

export default class NativeSample extends Component {
  constructor() {
    super();

    this.state = {
      firstVar: {movies: []},
    };
  }

  hideText = () => {
    fetch('https://facebook.github.io/react-native/movies.json')
      .then(response => response.json())
      .then(responseJson => {
        this.setState({firstVar: responseJson});
      })
      .catch(error => {
        console.error(error);
      });
  };

  makeList = item => {
    <Text key={item.title} style={styles.list}>
      {item.title}
    </Text>;
  };

  render() {
    return (
      <View>
        <Text onPress={this.hideText}>Click here to Fetch Data</Text>

        <Text>{this.state.firstVar.title}</Text>

        <Text>{this.state.firstVar.description} </Text>

        <ScrollView>{this.state.firstVar.movies.map(this.makeList)}</ScrollView>
      </View>
    );
  }
}

AppRegistry.registerComponent('NativeSample', () => NativeSample);

const styles = StyleSheet.create({
  list: {
    margin: 15,
    padding: 5,
    height: 40,
    borderColor: 'red',
    borderWidth: 1,
  },
});
```

![Networking Example 1](https://habiletechnologies.com/wp-content/uploads/2017/02/fetch1.png)
![Networking Example 2](https://habiletechnologies.com/wp-content/uploads/2017/02/fetch2.png)
