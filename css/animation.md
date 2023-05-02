## CSS Transition has 4 basic properties
1. property (box-shadow, height, etc. pp)
2. timing (1s, 400ms, ...)
3. ease (linear, ease-in-out, ...)
4. delay (0.5s)

<br>

### Note
**combined into one transition statement -> transition: box-shadow 1s ease-in-out 1s`this is the delay`, background-color 0.5s ease**

--------------------

* put Transition in component itself not the hover-state
* active for pressed button

--------------------

## Animating with JS
When we want to change an elements position, it is easier to solve this with javascript by appending a new class that holds the new position or use transition / translate
<br> **-> here, the animation state needs the transition property**
