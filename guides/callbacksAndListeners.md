# Callbacks and listeners

In order to make components more dynamic in can be usefull to add custom callback functions. This allows you to program things like button components that expose the onPress event.

In the guide we will write all components using typescript. If you need help setting up or understanding typescript please refer to the [README.md](https://github.com/3DJakob/expo-typescript-get-started-guide).

## What is a callback function

A callback function is a function that is passed as an argument to another function and is executed after some kind of event. Callback functions are a common pattern in JavaScript, and are used to handle asynchrony in the language.

Here is an example of a callback function in JavaScript:

```js
function greet(name: string, callback: () => void) {
  console.log('Hello, ' + name + '!')
  callback()
}

function sayGoodbye(): void {
  console.log('Goodbye!')
}

greet('John', sayGoodbye)
```

In this example, the `greet` function takes a name and a callback function as arguments. It logs a greeting to the console and then calls the `callback` function. The `sayGoodbye` function is passed as the callback function and is executed after the greeting is displayed. The output of this code would be:

```
Hello, John!
Goodbye!
```

## Implementing a callback function on a custom button component

On the `<TouchableOpacity>` component a event listener can be added with the `onPress` prop. Each time that event fires the declared function on the `onPress` prop will be called.

```tsx
<TouchableOpacity onPress={myFunction}>
```

By passing in a callback function in the component props we can then instead call the function in the parent. The result should look something like this:

```tsx
import React from 'react'
import { GestureResponderEvent, Text, TouchableOpacity } from 'react-native'

export interface ButtonProps {
  title: string
  onPress: (event: GestureResponderEvent) => void
}

const Button: React.FC<ButtonProps> = ({ title, onPress }) => {
  return (
    <TouchableOpacity onPress={onPress}>
      <Text>
        {title}
      </Text>
    </TouchableOpacity>
  )
}

export default Button
```

The button props typings are defined in the `ButtonProps` interface. As you can see we define our `onPress` callback function which sends the event back to the parent.