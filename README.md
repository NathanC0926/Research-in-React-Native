# Research in React Native

This repository contains research and examples related to React Native.

## Notes

### Differences Between React and React Native

#### React (React.js):

- Uses standard HTML elements like `<div>`, `<span>`, `<h1>`, etc.
- Styling is done using CSS or CSS-in-JS libraries.
- Uses the virtual DOM for rendering.

#### React Native:

- Uses components that map to native UI elements, such as `<View>`, `<Text>`, `<ScrollView>`, etc.
- Styling is done using JavaScript objects, often with the `StyleSheet` API: https://reactnative.dev/docs/stylesheet
- Uses native APIs to render components, which means it doesn’t use the virtual DOM.

### React Native with StyleSheet API

In React Native, you use the `StyleSheet` API to define your styles. Here’s an example:

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello, World!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f0f0f0',
  },
  text: {
    fontSize: 20,
    color: '#333',
  },
});

export default App;
```

### React with Tailwind CSS

Here’s an equivalent example using Tailwind CSS:

```javascript
import React from 'react';
import 'tailwindcss/tailwind.css';

function App() {
  return (
    <div className="flex justify-center items-center h-screen bg-gray-100">
      <h1 className="text-2xl text-gray-800">Hello, World!</h1>
    </div>
  );
}

export default App;
```
## Key Differences

### Syntax
- **React Native**: Uses JavaScript objects to define styles.
- **React with Tailwind CSS**: Uses utility classes directly in the `className` attribute.

### Styling Approach
- **React Native**: Styles are defined in a separate `StyleSheet` object and applied using the `style` prop.
- **React with Tailwind CSS**: Styles are applied directly in the `className` attribute using predefined utility classes.

### Flexibility
- **React Native**: You can dynamically change styles using JavaScript.
- **React with Tailwind CSS**: You can use conditional class names to apply different styles based on state or props.

  
# How to Call API Using React Native

This section covers how to make API calls in React Native, including examples and best practices.

## Introduction

React Native provides several ways to make API calls to fetch or send data. The most common methods are using the `fetch` API and the `axios` library. This guide will walk you through both methods with examples.

## Using the Fetch API

The `fetch` API is a built-in JavaScript function that allows you to make network requests. It is similar to `XMLHttpRequest` but more powerful and flexible.

## What is the Fetch API?

The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP protocol, such as requests and responses. It offers a global `fetch()` method that allows you to fetch resources asynchronously across the network. Unlike `XMLHttpRequest`, the Fetch API is promise-based, making it easier to work with asynchronous operations.

## Get and Post method using Fetch API

A basic fetch request looks like this:
```javascript
fetch(url, {options}) 
.then(data => { 
	// Do some stuff here 
}) 
.catch(err => { 
	// Catch and display errors 
}) 
```
## Sample Usage of Fetch API in React Native

This example demonstrates how to use the Fetch API in a React Native application to fetch data from an API.


```jsx
import React, { useEffect, useState } from 'react'; // Import necessary React hooks
import { View, Text, ActivityIndicator, StyleSheet } from 'react-native'; // Import React Native components

function App() {
  // Define state variables to manage data, loading state, and error state
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  // useEffect hook to perform side effects, such as fetching data, when the component mounts
  useEffect(() => {
    // Fetch data from the API
    fetch('https://jsonplaceholder.typicode.com/todos/1')
      .then((response) => response.json()) // Convert the response to JSON
      .then((json) => {
        setData(json); // Store the fetched data in the state
        setLoading(false); // Set loading to false as data is fetched
      })
      .catch((error) => {
        setError(error); // Store any errors in the state
        setLoading(false); // Set loading to false as the request is complete
      });
  }, []); // Empty dependency array means this effect runs once when the component mounts

  // Conditional rendering based on the state
  if (loading) {
    // Show a loading indicator while data is being fetched
    return <ActivityIndicator size="large" color="#0000ff" />;
  }

  if (error) {
    // Show an error message if there was an error fetching data
    return (
      <View style={styles.container}>
        <Text>Error: {error.message}</Text>
      </View>
    );
  }

  // Show the fetched data once it is loaded
  return (
    <View style={styles.container}>
      <Text>{data.title}</Text>
    </View>
  );
}

// Define styles for the components using StyleSheet
const styles = StyleSheet.create({
  container: {
    flex: 1, // Take up the full height of the screen
    justifyContent: 'center', // Center items vertically
    alignItems: 'center', // Center items horizontally
  },
});

export default App; // Export the App component as the default export



