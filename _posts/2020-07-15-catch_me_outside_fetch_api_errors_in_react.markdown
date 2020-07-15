---
layout: post
title:      "Catch Me Outside : Fetch API Errors in React"
date:       2020-07-15 17:52:25 -0400
permalink:  catch_me_outside_fetch_api_errors_in_react
---



You love the Fetch API.  Like most of us, you grew up with Fetch API posters on your wall and at age 30 your arm is covered in a sleeve of Fetch API tattoos.  

The Fetch API lets you send Ajax requests with ease, and yes, it impresses little kids at a birthday parties.  

But there is a dark side...

**ERROR HANDLING!!!**

Take a look at this common method to handle fetch errors:

```
fetch(url).then((response) => {
  // You will always get a response, unless there is NETWORK error
  // 4xx and 5xx errors are treated as successful responses
}).catch(error) => {
  // Again, only network errors will come here
};
```

Since Fetch doesn't throw an error for non-2xx responses, your exceptions will be swallowed and prevent you from finding the bugs in your React components.  So what's the solution?  

According to [Dan Abramov's tweet](https://twitter.com/dan_abramov/status/770914221638942720?lang=en):

> The solution is so simple. Just don’t chain catch() *after* then() that renders UI. Instead pass error handler as second arg to then().


Like this:
```
fetch(url)
      .then(res => res.json())
      .then(
        (result) => {
          // This is where you do something with the response data
        },
        // Handle 👏 errors 👏 here 👏 instead 👏 of 👏 a 👏catch 👏 block
        (error) => {
				  // This is where you do your error handling
        }
      )
```


Better yet, let's look at some real code.  Here we are looking at a component with a constructor and a componentDidMount function for a simple todo list application.

```
constructor(props){
    super(props)
    this.state = {
      error: null,
      isLoaded: false,
      data: []
    }
  }
	
componentDidMount() {
    fetch(url)
      .then(res => res.json())
      .then(
        (result) => {
          this.setState({
            isLoaded: true,
            data: result
          });
        },
        (error) => {
          this.setState({
            isLoaded: true,
            error
          });
        }
      )
  }	
```
	
	
Simple and clean, right?  If you are dead-set on using "catch", there are still ways to handle errors that don't let 404's and the like slip through the cracks.  Check this out:

```
	fetch(url)
    .then(function(response) {
        if (!response.ok) {
            throw Error(response.statusText);
        }
        return response;
    }).then(function(response) {
        console.log("ok");
    }).catch(function(error) {
        console.log(error);
    });	
```
		
In the above snippet, we are evaluating our response's 'ok' boolean value.  Since errors "ok" evalutate to false, once we have a false value we immediately throw an error with the statusText from the response.  Now our thrown error will trigger the catch block instead of missing it completely.

You could actually take it a step further and refactor the above strategy into a reusable method like so:

```
function handleErrors(response) {
    if (!response.ok) {
        throw Error(response.statusText);
    }
    return response;
}

fetch(url)
    .then(handleErrors)
    .then(function(response) {
        console.log("ok");
    }).catch(function(error) {
        console.log(error);
    });
```

What's that?  The kids have gone to bed and you want to take it up another notch?  Ok, take a gander at THIS:

```
function handleErrors(response) {
    if (!response.ok) {
        throw Error(response.statusText);
    }
    return response;
}
fetch(url)
    .then(handleErrors)
    .then(response => console.log("ok") )
    .catch(error => console.log(error) );
```

Arrow functions just make this look sexy.  Maybe too sexy.  Might want to clear out that browsing history after this blog post.

Long story short...

**DON'T RELY ON A CATCH BLOCK WITHOUT UNDERSTANDING IT WON'T CATCH 4xx and 5xx RESPONSE CODES! ** 

Sorry for the yelling.

		





