#ijeomamotion.js
 
A Javascript library for creating animations. Ijeoma (ee-JOH-mah) means bon voyage in Igbo, a language from Nigeria. The code is based on [ijeomamotion for Java/Processing](https://github.com/ekeneijeoma/ijeomamotion) which was ported to JS for processing.js so it could be used in Processing, cross-mode (between Java and JS modes with no changes to the code). While processing.js and Processing Javascript mode were sleeping ijeomamotion was being refactored to ijeoma.js which weights a lot less, has more muscle and is independent from processing.js and p5.js although there is an [addon for p5.js](https://github.com/ekeneijeoma/p5.ijeomamotion.js) because we still love Processing :) 

#Download 
Developement: [ijeomamotion.js](https://raw.githubusercontent.com/ekeneijeoma/ijeomamotion.js/master/build/ijeomamotion.js)

Production: [ijeomamotion.min.js](https://raw.githubusercontent.com/ekeneijeoma/ijeomamotion.js/master/build/ijeomamotion.min.js)

#Examples  
[MOTION](http://ekeneijeoma.github.io/ijeomamotion.js/examples/Motion.html): counts from a starting time of 0 to an ending duration. 

[MOTION.Tween](http://ekeneijeoma.github.io/ijeomamotion.js/examples/Tween.html): eases multiple number variables and object properties from a starting value to an ending value within a duration. 

[MOTION.Parallel](http://ekeneijeoma.github.io/ijeomamotion.js/examples/Parallel.html): plays multiple tweens at the same time.

[MOTION.Sequence](http://ekeneijeoma.github.io/ijeomamotion.js/examples/Sequence.html): plays tweens one after the other.

[MOTION.Timeline](http://ekeneijeoma.github.io/ijeomamotion.js/examples/Timeline.html): plays Tweens, Parallels and Sequences any time using MOTION.Keyframes.

[Mouse](http://ekeneijeoma.github.io/ijeomamotion.js/examples/mouse.html)

[Gradients](http://ekeneijeoma.github.io/ijeomamotion.js/examples/gradients.html): shows how to create custom property for tweening colors

[Lines](http://ekeneijeoma.github.io/ijeomamotion.js/examples/lines.html)

[Pie Chart](http://ekeneijeoma.github.io/ijeomamotion.js/examples/pieChart.html)

[Circular Network](http://ekeneijeoma.github.io/ijeomamotion.js/examples/circularNetwork.html)

[Square](http://ekeneijeoma.github.io/ijeomamotion.js/examples/square.html): shows how to combine sequences and tweens in a timeline

#Getting Started 
###Tweening
Tweening a variable named x from 0 to 1024 in 1000 millseconds. 
```javascript 
//new MOTION.Tween(object, property, end, duration, [delay], [easing])
var x = 0;
var tween = new MOTION.Tween(window, "x", 1024, 1000).play(); // if no object is passed it will default to window
```
or
```javascript 
//new MOTION.Tween(property, [start,end], duration, [delay], [easing])
var tween = new MOTION.Tween("x", [0,1024],1000).play(); // object defaults to window and the variable x is defined in window with a starting value of 0
```

Tweening multiple variables and object properties
```javascript
//new MOTION.Tween(duration, [delay], [easing])
var tween = new MOTION.Tween(1000).add(window, "x", [0,1024]).add(window, "y", [0,768]).add(window, "size", [0,100]).play();
```
or
```javascript
//new MOTION.Tween(duration, [delay], [easing])
var tween = new MOTION.Tween(1000).add("x", [0,1024]).add("y", [0,768]).add("size", [0,100]).play(); // object defaults to window
```

###Removing tween 
If you're creating and playing a lot of tweens that you're only using once you should set useOnce(). It's set to false by default.
```javascript 
new Motion(...).useOnce();
or
//applies call to all tween instances
MOTION.useOnce();
```


You can also call play and stop on all motion objects using
```javascript
MOTION.playAll()
MOTION.stopAll()
```

###Calling functions on start update and end events 
```javascript
t = new MOTION.Tween(...).onStart(func).onUpdate(func).onEnd(func).play(); 
```

###Updating
```javascript 
MOTION.update(time) //best used with requestAnimationFrame
```
or
```javascript 
MOTION.update() //will use performance.now() or Date.now() if not supported.
```

###Delaying
```javascript
var tween = new MOTION.Tween("w", 1024, 1000, 500).play(); //delay for 500 milliseconds
```
or
```javascript
var tween = new MOTION.Tween("w", 1024, 1000).delay(500).play();
```
###Pausing, Resuming  
```javascript  
t.pause(); 
t.resume(); 
t.seek(position); 

//applies call to all motion instances
MOTION.pauseAll();
MOTION.resumell();
MOTION.seekAll(position);
```
###Repeating
```javascript
var tween = new MOTION.Tween(...).repeat().play();

MOTION.repeatAll([duration]);
```
###Reversing
```javascript 
var tween = new MOTION.Tween(...).repeat().reverse().play();

MOTION.reverseAll();
```

###Changing speed/timescale
```javascript 
var tween = new MOTION.Tween(...).timeScale(2) //plays back twice as fast

MOTION.timeScaleAll(time);
```

###playing

##Playing back tweens in parallel
```javascript
var parallel = new MOTION.Parallel()
  .add(new MOTION.Tween(...)) 
  .add(new MOTION.Tween(...)) 
  .play(); 
``` 

##Playing back tweens in sequence
```javascript
var sequence = new MOTION.Sequence() 
  .add(new MOTION.Tween(...)) 
  .add(new MOTION.Tween(...))  
  .repeat()
  .play();
``` 

##Playing back tweens in a timeline
```javascript
var timeline = new MOTION.Timeline()
  .add(new MOTION.Tween(...), 1000) //creates a keyframe at 1000 milliseconds and adds that tween object
  .add(new MOTION.Tween(...), 2000)
  .repeat()
  .play();
``` 
or
```javascript
var timeline = new MOTION.Timeline();
var keyframe1 = new MOTION.Keyframe(1000).add(new MOTION.Tween(...))
var keyframe2 = new MOTION.Keyframe(2000).add(new MOTION.Tween(...))
timeline.add(k1).add(k2).play();
``` 

##Going to and playing or stopping at a keyframe
```javascript
timeline.play(time)
timeline.stop(time)
```

