## Website Performance Optimization portfolio project

In this repository, you will find the original source files for the Website Optimization project, as well as the optimized code, which can be found in the `dist` folder. **Please use only the files in the `dist` folder to evaluate the project.**

Additionally, a live version of the site can be found [here](http://www.achateauenrose.com/udprojsit/) for your (and [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?url=achateauenrose.com%2Fudprojsit&tab=desktop)') convenience.

#### Part 1: Optimize PageSpeed Insights score for `index.html`

The largest optimizations made to `index.html` were as follows:
- Compress images
- Added inline CSS for critical styles
- Non-essential, render-blocking scripts/styles now load asyncronously or only when required via media query

Additionally, changes were made to:
- Allow for caching files
- Remove slow loading web fonts
- Minify .css and .html files

#### Part 2: Optimize Frames per Second in `pizza.html`

##### Pizza Size Slider

To make the slider resize pizzas in less than 5 ms, I reworked the `changePizzaSizes()` function in `main.js` into a simplified function where the width is solely determined by a specific percentage, depending on the slider input. The `determineDx()` function has been entirely removed, as the prior size of the pizzas in relation to the new input should be, and now is, irrelevant. I also changed `document.querySelector()` to the faster `document.getElementById()` in the `changeSliderLabel()` function.

##### Render `pizza.html` at `60fps`

Several optimizations were made to make `pizza.html` render at `60fps`. 
1. `scrollTop` was removed from the `for` loop in `updatePositions()`, as it was creating a forced synchronous layout.
2. Additional functions `onScroll()` and `requestTick()` were created to run on a scroll event listener and ensure that `requestAnimationFrame()` calls do not stack up, respectively.
3. The faster `document.getElementsByClassName()` was used in place of `document.querySelectorAll()` in the `randomPizzas` variable.
4. `randomPizzas.length` and `items.length` were saved in local variables so they do not need to be checked in each iteration of their respective `for` loops.
5. `pizzasDiv` was declared ouside its `for` loop so the DOM call is made only once.
6. `phase` was declared ouside its `for` loop so it is only created once.
7. Changed `document.querySelector()` to the faster `document.getElementById()` for `movingPizzas1`, and stored it in a local variable outside the `for` loop so it is not re-created in each loop iteration.
8. Declared the `elem` variable in the initialization of the `for` loop rather than within the loop.
9. The size of the `for` loop within the `DOMContentLoaded` event listener was altered to reduce the number of sliding pizzas created from 200 to 50.

This summarizes the main optimizations made to `index.html` and `views/js/main.js` for `pizza.html`.