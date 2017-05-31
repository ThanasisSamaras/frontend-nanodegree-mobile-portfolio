## Website Performance Optimization portfolio project

The challenge for this Udacity Front-End Nanodegree project was to optimize a given online portfolio for speed! In particular, I had to optimize the critical rendering path and make this page render as quickly as possible by applying the techniques I've picked up in [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, click on Click or download, Download ZIP and open the frontend-nanodegree-mobile-portfolio folder. You can then check out the repository and inspect the code.

### Part 1: PageSpeed Score

#### Tools used:

- Grunt task runner for minification of CSS and JS. Instructions on how to get started with Grunt can be found [here](https://gruntjs.com/).
- [ImageMagick](https://www.imagemagick.org/script/index.php) commands to convert and resize images.
- A simple HTTP 8080 server with python, to inspect the site on the phone.
- ngrok, in order to make my local server accessible remotely and check the index.html on PageSpeed Insights. To get started with ngrok:

1. Open a browser and visit localhost:8080.
2. Download and install [ngrok](https://ngrok.com/) to the top-level of the project directory.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

3. Copy the public URL ngrok gives you and try running it through PageSpeed Insights.

#### Optimizations in index.html:

1. Embedded CSS to HTML and minified JS.
2. Made script async to prevent it from blocking the parser and used a media print type so as print.css is not required to render the page.
3. Removed web fonts and analytics from being loaded, as these scripts had an impact on page load.
4. Reduced image sizes and changed format where approprtiate.
5. Overall, achieved a PageSpeed score of 92/100 for mobile and 93/100 desktop.

### Part 2: Getting Rid of Jank

#### Frame Rate

Applied optimizations to views/js/main.js make views/pizza.html render at 60fps when scrolling.

- Split the for loop in updatePositions function into two different loops, to separate layout from style calculation.
- Saved items length and scrolling phases to separate variables and used these in the for loop, avoiding thus querying the DOM each time.
- Moved items value outside the function so as to query items after they've been created but before they're needed. Also, defined the items globally, so it can be accessed by the updatePositions function.
- Defined items within the event listener so that DOM is queried only when the DOM content is loaded. Also, switched to getElementsByClass because it's faster.
- Reduced the number of created pizzas in the event listener, by calculating dynamically the number of pizzas only needed to fill the screen.

#### Computational Efficiency

Time to resize pizzas is now less than 5 ms using the pizza size slider on the views/pizza.html page.

- Simplified changePizzaSizes function, by figuring out only the required pizza width and setting the width of each element to that percentage from within the for loop.
- Saved the collection of DOM nodes into a variable randomPizzas, so as to avoid querying the DOM every time.
- Also, removed back and forth of conversions between pixels and percentages in the for loop, by saving significant time.
