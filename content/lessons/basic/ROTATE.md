---
title: "Rotate Square"
lesson: 4
chapter: 7
date: "03/01/2018"
type: "lesson"
---
# Basic Rotation

#### Live Code [https://rnplay.org/apps/VI9yaw](https://rnplay.org/apps/VI9yaw)

![Simple Rotate Animation](../images/SimpleRotateAnimation.gif)

```js
import React, { Component } from "react";
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Animated
} from "react-native";

class SampleApp extends Component {
  
  componentWillMount () {
    this._animatedValue = new Animated.Value(0);
  },
  componentDidMount () {
    Animated.timing(this._animatedValue, {
        toValue: 100,
        duration: 3000
    }).start(); 
  }
  
  render () {
    
    const interpolatedRotateAnimation = this._animatedValue.interpolate({
    	inputRange: [0, 100],
      outputRange: ['0deg', '360deg']
    });
    
    return (
      <View style={styles.container}>
       <Animated.View 
      		style={[styles.box, {transform: [{rotate: interpolatedRotateAnimation}]}]}
      	/>
      </View>
    );
  }
};

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  box: {
    backgroundColor: 'red',
    position: 'absolute',
    top: 100,
    left: 100,
    width: 100,
    height: 100
  }
});

```

## Merge them all together

#### Live Code [https://rnplay.org/apps/2XNa8g](https://rnplay.org/apps/2XNa8g)

We just need to adjust our render function to bring all the code together

```js
  render() {
    
    const interpolatedRotateAnimation = this._animatedValue.interpolate({
    	inputRange: [0, 100],
      outputRange: ['0deg', '360deg']
    });
    
    const interpolatedColorAnimation = this._animatedValue.interpolate({
    	inputRange: [0, 100],
      outputRange: ['rgba(255,255,255, 1)', 'rgba(51,156,177, 1)']
    });
    
    return (
      <View style={styles.container}>
       <Animated.View 
      		style={[styles.box, {backgroundColor: interpolatedColorAnimation, 
      				transform: [{translateY: this._animatedValue}, 
      							{rotate: interpolatedRotateAnimation}
      						    ]}
			    	]}
      	/>
      </View>
    );
  }
```