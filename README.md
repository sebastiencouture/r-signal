recurve-signal [![Build Status](https://secure.travis-ci.org/sebastiencouture/recurve-signal.png?branch=master)](https://travis-ci.org/sebastiencouture/recurve-signal)
===

Custom event/messaging library for the browser and Node.js. Inspired by AS3 signals library.

Similar to other event dispatching mechanisms such as event emitters, or buses. But instead of registering for events by
string name you register on a signal object responsible for one event.

## Usage

### Example

```javascript
var started = new Signal();

// Add some listeners
started.on(onStartA);
started.on(onStartB);

// Trigger the signal. onStartA and onStartB will be called with "oh ya" as
// the message
started.trigger("oh ya");

// Remove a listener
started.off(onStartA);

// onStartA will not be called, but onStartB will be called
started.trigger("oh no");
```

For more examples, take a look at the [unit tests](test/recurve-signal.spec.js)

### Creating a Signal

#### Signal()

```javascript
var started = new Signal();
```

### Adding Listeners

#### on(callback, context)

Add a listener. The callback will be called each time the signal is triggered.

If a listener for the callback and context already exists then this method will do nothing. Duplicate
listeners will not be added.

```javascript
var started = new Signal();
signal.on(onStart, this);

function onStart() {
}
```

#### once(callback, context)

Adds a listener callback that will only be called once and will then be removed.

If a listener for the callback and context already exists then this method will do nothing. Duplicate
listeners will not be added.

```javascript
var started = new Signal();
signal.once(onStart, this);

function onStart() {
}

started.trigger(); // onStart will be called and then removed as a listener
started.trigger(); // onStart will not be called
```

### Trigger Signal

#### trigger()

Triggers the signal. Arguments passed into the method will be passed as parameters to all listeners

```javascript
var signal = new Signal();
signal.on(function(message) {
    // will be called with "oh ya" as the message
});

signal.trigger("oh ya");
```

### Removing Listeners

#### off(callback, context)

If a callback and context are specified then the listener with matching callback and context is removed

```javascript
var started = new Signal();
signal.on(onStartA, this);
signal.on(onStartB, this);
signal.off(onStartA, this); // only onStartA will be removed
```

If only a callback is specified then the listener with matching callback is removed

```javascript
var started = new Signal();
signal.on(onStartA, this);
signal.on(onStartB, this);
signal.off(onStartA); // only onStartA will be removed
```

If only a context is specified then all listeners with the matching context are removed

```javascript
var started = new Signal();
signal.on(onStartA, this);
signal.on(onStartB, this);
signal.on(onStartC);
signal.off(null, this); // onStartA and onStartB will be removed
```

If no callback or context are specified then all listeners are removed (equivalent to clear)

```javascript
var started = new Signal();
signal.on(onStartA, this);
signal.on(onStartB, this);
signal.on(onStartC);
signal.off(); // onStartA, onStartB, and onStartC will be removed
```

#### clear()

```javascript
var started = new Signal();
signal.on(onStart);
signal.clear();
```

### Disabling

#### disable(value)

Disable or enable listeners from being called when the signal is triggered.

```javascript
var signal = new Signal();
signal.on(onStart);
signal.disable();

signal.trigger(); // onStart will not be called
signal.disable(false);
signal.trigger(); // onStart will be called
```

## Running the Tests

```
grunt test
```

## Installation

The library is UMD compliant. Registers on `window.Signal` for global.

```
npm install recurve-signal
```

## Browser Support

IE6+

## License

The MIT License (MIT)

Copyright (c) 2015 Sebastien Couture

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.