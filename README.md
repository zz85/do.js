do.js
=====

Minimalistic Event Dispatcher

About
=====
do.js is a simple event dispatching library written in < 20 lines of code.

See usage on how to use it.

```
function Do(parent) {
	var listeners = [];
	this.do = function(callback) {
		listeners.push(callback);
	};
	this.undo = function(callback) {
		listeners.splice(listeners.indexOf(callback), 1);
	};
	this.fire = function() {
		for (var v = 0; v < listeners.length; v++) {
			listeners[v].apply(parent, arguments);
		}
	};
}
```

Why Do?
=======
Not that I want to create yet another xyzsource library/micro-framework, but here's the story.

While on the train to work, I was tinkling with [source](https://github.com/zz85/3ource) and needed a simple event listener system.

That's how I wrote this (in probably less than 5 minutes) just because I needed something simple and have something I could understand easily. The api also attempts to be english like while minimise typing.

Do.js can be pronounced as doh-dot-j-s, or do-dot-j-s. Doh like in play dough, do-ra-me, doraemon, [domo](http://domo-js.com/). Do like in "do this", "I do", or a do-while loop. (My original name for this class would be "ondo", but nvm it..)

One difference between your usual way you handle 

```
element.addEventListener('bla', function(something) {});
vs
element.onBla.on(function(something) {});
```

Of course, this library may not be of production quality or fitting your usual/preferred event dispatching style, in that case feel free to try out [eventdispatcher.js](https://github.com/mrdoob/eventdispatcher.js/) or many other libraries out there.

This event handling approach is however nothing new, and my idea's inception probably started with Robert Penner's (the guy who also brought us easing/tweening equations) related work with [Signals in as3](https://github.com/robertpenner/as3-signals). You may also like to check out [this page](http://millermedeiros.github.io/js-signals/) which includes a good comparison of [different observer pattern implementations](https://github.com/millermedeiros/js-signals/wiki/Comparison-between-different-Observer-Pattern-implementations).

Usage
=====

```
function Cat() {
	this.name = 'cat';
	this.onSay = new Do(this); // Create an event listener type
}

Cat.prototype.says = function(something) {
	console.log('Cat says ' + something);
	this.onSay.fire(something); // Notifies listeners of something
}

var cat = new Cat();

cat.onSay.do(function(something) {  // Adds listener
	console.log('I hear ' + this.name + ' say ' + something);
});

cat.says('Meow!');
```

Node
====
Do supports node.js.

```
var Do = require('./do.js');

var onFire = new Do();
onFire.do(something)

onFire.fire('bla');
```

Tests
=====
Not yet. You make a [pull request](https://github.com/zz85/do.js/pulls).

Contact
=====
For improvements, suggestions, you may use [github issues](https://github.com/zz85/do.js/issues).
You may also subscribe to my Twitter: [@blurspline](http://twitter.com/blurspline)

License
=====
MIT
