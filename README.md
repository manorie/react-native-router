# React Native Router
Awesome navigation for your React Native app.

![Twitter navigation](http://tristanedwards.me/u/react-native-router/native-router.gif)

# Install

Make sure that you are in your React Native project directory and run:

```npm install react-native-router --save```

# Usage

```javascript
var Router = require('react-native-router');
```

The basics:
```javascript
// The initial page
var HelloPage = React.createClass({
  render: function() {
    return <Text>Hello world!</Text>;
  }
});

// Your route object should contain at least:
// - The name of the route (which will become the navigation bar title)
// - The component object for the page to render
var firstRoute = {
  name: 'Welcome!',
  component: HelloPage
};

// The Router wrapper
var MyApp = React.createClass({
  render() {
    return (
      <Router firstRoute={firstRoute} />
    )
  }
});

AppRegistry.registerComponent('routerTest', () => MyApp);
```

Boom. That's it.

From the "Hello world!"-page you can then navigate further to a new component by calling ```this.props.toRoute()```. If we build upon our first example:

```javascript
var HelloPage = React.createClass({

  nextPage: function() {
    this.props.toRoute({
      name: "A new screen",
      component: HelloPage
    });
  },

  render: function() {
    return (
      <View>
        <TouchableHighlight onPress={this.nextPage} underlayColor="transparent">
          <Text>Next page please!</Text>
        </TouchableHighlight>
      </View>
    );
  }
});
```

Now it will go to the next page (which in this case is still HelloPage but with a new title) when you click on "Next page please!". Keep in mind that ```this.props.toRoute()``` needs to be called from one of the top-level routes, therefore, if you put your link is deeply nested inside multiple components, you need to make sure that the action "bubbles up" to the parents' props.


# A more advanced example: Twitter app

To see more of the router in action, you can check out the Twitter example app that comes with the package. Make sure that you first drag all the images from node_modules/react-native-router/twitter-example/images``` to your project's Images.xcassets:

![Drag the assets to xcassets](http://tristanedwards.me/u/react-native-router/drag-assets.gif)

After that, make sure you rebuild the app in XCode before you launch the simulator. Then test the app by requiring the TwitterApp component:

```javascript
var TwitterApp = require('./node_modules/react-native-router/twitter-example');

var {
  AppRegistry
} = React;

AppRegistry.registerComponent('routerTest', () => TwitterApp);
```

# Configurations

The <Router /> object used to initialize the navigation can take the following props:
- firstRoute (required): A React class corresponding to the first page of your navigation
- headerStyle: Used to set the default headerStyle. You'll probably want to change the backgroundColor.
- backButtonComponent: By default, the navigation bar will display a simple "Back" text for the back button. To change this, you can specify your own backButton component (like in the Twitter app).
- rightCorner: If you have the same occuring action buttons on the right side of your navigation bar (like the Twitter "Compose"-button), you can specify a component for that view.

toRoute() takes one parameter (a JavaScript object) which can have the following keys:
- name: The name of your route, which will be shown as the title of the navigation bar unless it is changed.
- component (required): The React class corresponding to the view you want to render.
- leftCorner: Specify a component to render on the left side of the navigation bar (like the "Add people"-button on the first page of the Twitter app)
- rightCorner: Specify a component to render on the right side of the navigation bar
- titleComponent: Specify a component to replace the title. This could for example be your logo (as in the first page of the Instagram app)
- headerStyle: change the style of your header for the new route. You could for example specify a new backgroundColor and the router will automatically make a nice transition from one color to the other!


# Todos
When swiping from left to right to go back, it would be nice if the navigation bar's opacity gradually changed with the user's finger position. (See [Issue #1](https://github.com/t4t5/react-native-router/issues/1))
