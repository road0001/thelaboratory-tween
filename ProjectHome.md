[![](http://thelaborat.org/img/code_google_title.jpg)](http://thelaborat.org/)
# Intro #
This project has the objective to host all as3 classes related to tweening. There will be 2 main focus:

# 1) ByteTween #
Light weight engine (focusing in low Kb increase and not being a do-it-all engine).

## v1.3 ##
Fixes some bugs from v1.2 that causes malfunction on large number of tweens.
Adds new modules to the module list, they are the Gradients module. Added too the ShortTween wich is a shortcut for the most common tweens (x,y,alpha,...). Correction of bugs added some bytes to the basic version.

### Features ###
  * Same as v1.2 and bug fixes.
  * New modules! Added GradientRGB and GradientARGB (call for "gradientRGB" and "gradientARGB" respectively).
  * ShortTween = static class with shortcut to most common tweens (alpha,x,y,...).

#### Modules Available ####
  * **SimpleVersion(1.0Kb)** Actually not a Module. Just the ByteTween **without** overlap check,pause,unpause,cancel. Just the basic Numeric Tween. The smallest size the code will generate.
  * **ColorModule(+0.4Kb)** Adds the 'color' tween feature.
  * **ControlModule(+0.2Kb)** Adds the 'pause','unpause','cancel' functions to the engine.
  * **FrameModule(+0.1Kb)** Adds the 'frame' tween feature.
  * **OverlapModule(+0.1Kb)** Adds the overlap check in the tween execution (remove older tweens of same property when a new one of same property arrives).
  * **ScaleModule(+0.1Kb)** Adds the 'scale' tween feature (tween both scaleX and scaleY).
#### New Modules ####
    * **GradientRGB(+0.4Kb)** Given an Array of RGB uint values, tween all colors through time.
    * **GradientARGB(+0.4Kb)** Given an Array of ARGB uint values, tween all colors (including alpha channel) through time.

#### ShortTween List ####
  * x,y,position (both x/y),scaleX,scaleY,scale (both scaleX/Y),shrink (scale=0),expand (scale=1),alpha,fadeIn (alpha=1),fadeOut (alpha=-1),color,rotation,width,height.

**Usage:**
```
//has_overlap: Flag that says if the engine will check overlap.
//has_control: Flag that says if the engine can do pause,unpause,cancel actions.
//... args: Adds 0 or more modules by just adding the module classes separated by commas.
//Ex.: ByteTween.init(stage,true,true,OverlapModule,ControlModule,ColorModule);
ByteTween.init(stage,has_overlap:Boolean,has_control:Boolean,... args);
ByteTween.add(target:*, property:String,value:*,duration:Number,delay:Number, ease:Function,p_callback:Function,... arguments);

//New ShortTween **some examples
ShortTween.x(target:*,pos_x:Number,duration:Number,delay:Number, ease:Function,p_callback:Function,... arguments);
ShortTween.alpha(target:*,alpha:Number,duration:Number,delay:Number, ease:Function,p_callback:Function,... arguments);
//Same as alpha but tween directly to alpha=1.0
ShortTween.fadeIn(target:*,duration:Number,delay:Number, ease:Function,p_callback:Function,... arguments);
//Same as alpha but tween directly to alpha=-0.1
ShortTween.fadeOut(target:*,duration:Number,delay:Number, ease:Function,p_callback:Function,... arguments);

```


## v1.2 ##
Upgrade of version 1.1 with pratically same features. The difference is now the system can be configured by setting wich functionality module you want active on compile time.
With this system you can setup from just a numeric tweener to the full functional tween engine with color,scale,... tweens.
Well this is the most stable version. I think that new versions will come in form of modules but now I'm busy in finishing the MotionPack and new useful classes for ya!

### Features ###

  * Same as v1.1 but now you can add/remove functionalities on compile time.
  * Module System that permits to add the funcionality you want and control the size of your swf.
  * Most simple version of ByteTween starts now with just **0.8Kb**!! Ok actually 885 bytes.. sorry..
  * Functinonality Modules. Choose what you wan just insert it :)
  * Even with all funcionalities inserted the max size that the code will achieve is **~2Kb**!!
  * Alpha tween with visibility test is included in the basic package. Well it's just a boolean check :)

## v1.1 ##
First official version. v1.0 is a gold version :).
### Features ###


  * **Ridiculous amount of Kb increase: Just 1.2Kb!**
  * numeric properties tweening.
  * 'color'.
    * Using ColorTransform.
  * 'alpha' with visibility control (negative alpha sets visible=false).
  * 'frame' tweening.
  * 'scale' tween.
    * Both scaleX and Y at the same time.
  * 21 easing functions + All Robert Penner's classic functions.
  * Tween pause,unpause,cancel control.
    * Operation pointed by the target and its properties.
  * Tween overlap control.
    * A starting tween checks for older tweens of same property and cancel them).

# 2) MotionPack #
Package of classes,events and interfaces that allows the developer not only to do the common tweening tasks (with the BaseTween class), but also develop its own tweening classes.
It uses a Interface system that allow easy implementation and do not use the only "slot" of the "extends" keyword :).

# Easing Functions Expansion #
Within the "org.thelab.motion.transition" package are the most common transitions used in tweens, and also the well known Robert Penner's transition functions.

But one can also implement its own tween functions.

Both tween engines uses default functions for it. The template for them is:
```
function ease_name(r:Number):Number;
```
Where the "r" parameter is a Number inside 0.0 -> 1.0 range.
Where 0.0 is the tween start and 1.0 is the tween end.
The result of this function is used in the following equation:
```
target[property] = initial_value + (delta_value)*ease_name(r);
```
