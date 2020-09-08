# python-websocket-visualization

**An example of how to use a websocket server to update a web-based visualization in a Python loop.**

## Overview
This repository illustrates how to start and update a web-based visualization tool in real-time from a single Python script in an asynchronous manner, 
without having to refress the web-browser page. 

## The Components

### websocket_example.py

This [file](websocket_example.py) represents the core of the program and contains:
  1. A class [`WsServer`](websocket_example.py#L10) that represents a Python WebSocket server.
  2. A class [`HTTPServer`](websocket_example.py#L52) used to start an HTTP server.
  3. A function [`start()`](websocket_example.py#L72) to start the web-based visualization.
  4. A function [`update()`](websocket_example.py#L80) to update the web-based visualization.
  5. A function [`close()`](websocket_example.py#L87) to end the visualization.
  6. A script that can be used as example.

### index.html

This [file](index.html) contains a very simple ~10-line HTML code that renders the progress bar to be updated by the Python loop.

### dynamicUpdate.js

This [file](dynamicUpdate.js) contains the JavaScript code used to communicate with the WebSocket Server and update the status of the progress bar.

## How It Works

The example Python script works as follows.
  1. Initialize the HTTP and WebSocket servers in two separate threads.
  2. Start a loop. At every iteration, do:
    1. Send an update message through WebSocket (no need to wait, everything is asynchronous).
  3. The message is received by the Javascript WebSocket connection and the status of the progress bar is updated accordingly.
  
## How to use it in your projects

You can clone this repository with:
``` git clone https://github.com/robinhenry/python-websocket-visualization```

There are very few changes that need to be made to use this framework for any web-based visualization:
  1. Edit the [index.html](index.html) file to your liking. Make sure to give an `id` property to all elements that you will want to dynamically update.
  2. Edit the [`ws.onmessage`](dynamicUpdate.js#L13-L16) JavaScript function to update any HTML elements or interest upon recept of a new message.
  3. Edit the [`update()`](websocket_example.py#L80-L85) Python function to add to the WebSocket message any information required by 2.
  4. That's it!
  
I hope you will find it useful!
