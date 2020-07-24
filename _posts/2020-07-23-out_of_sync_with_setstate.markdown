---
layout: post
title:      "Out of Sync with setState"
date:       2020-07-24 01:51:29 +0000
permalink:  out_of_sync_with_setstate
---


When I started learning React, I was always baffled by this phenomenon - I'm using a simple React component which has a input field with an onChange event attached. The onChange event fires, and updates the component state with the value from the input field.  I log the input in the console to do some debugging like so:

```
handleChange = event => {
    this.setState({
      [event.target.name]: event.target.value
    })
    console.log(this.state.input)
  }
```

But when I look at the console log, there appears to be a lag, for example if I was typing "Learn" the console would display the following:

**''** after typing L

**'L'** after typing e

**'Le'** after typing a

**'Lea'** after typing r

**'Lear'** after typing n

What is happening here?

![](https://media.giphy.com/media/11OO4x7JURZoTC/giphy.gif)


If you are encountering React for the first time, go grab a Magic Marker and write this across your forehead:

# setState IS ASYNCHRONOUS

In other words, console.log() was fired before waiting for setState() to complete.  Why is this?  According to the React documentation:


> setState() does not immediately mutate this.state but creates a pending state transition. Accessing this.state after calling this method can potentially return the existing value. There is no guarantee of synchronous operation of calls to setState and calls may be batched for performance gains.


While this approach may seem counterintuitive, it isn't.  React's setState changes the state and triggers a rerendering.  This could potentially be a very expensive operation and if setState was synchronous, it could leave the browser unresponsive for a significant amount of time.  Long story short, setState is asynchronous.

Going back to the original block of code, if I wanted to call console.log() to accurately reflect the component's state after setState() is called, I would do something like this:

```
handleChange = event => {
    this.setState({
      [event.target.name]: event.target.value
    }, ()=> {console.log(this.state.input)})
  }
```

Calling an anonymous function as the second argument to setState allows you execute an operation AFTER the state has been updated.  

After you memorize this fact, please wipe the magic marker off of your forehead.



