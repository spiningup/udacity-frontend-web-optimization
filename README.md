## Part 1 - PageSpeed Score
### _Goal: index.html achieves a PageSpeed score of at least 90 for Mobile and Desktop._

### Steps taken:
1. Add async to loading analytics.js
`<script async src="https://www.google-analytics.com/analytics.js"></script>`
2. Add media option to loading print.css
`<link href="css/print.css" rel="stylesheet" media="print">`
3. Inline 'css/style.css' in 'index.html'
4. Compress and resize 'pizzeria.jpg'; compress all other images
5. Use webfont to load google fonts at the end of body
```
<script src="https://ajax.googleapis.com/ajax/libs/webfont/1.6.16/webfont.js"></script>
<script>
 WebFont.load({
    google: {
      families: ['Open+Sans:400,700']
    }
  });
</script>
```

## Part 2 - Getting Rid of Jank
### _Goal: Make 'views/pizza.html' render at 60fps when scrolling._

### Steps taken:
1. 'document.body.scrollTop' does not change, so move it to outside the loop:
```
function updatePositions() {
...
var items = document.querySelectorAll('.mover');
var bodytop = document.body.scrollTop;
for (var i = 0; i < items.length; i++) {
  var phase = Math.sin((bodytop/ 1250) + (i % 5));
  items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
}
```
2. There is no need to put 200 pizzas in the background, calculate the number of
pizzas needed according to screen size:
```
document.addEventListener('DOMContentLoaded', function() {
  ...
  var n = (Math.ceil(screen.width / 173.33) * Math.ceil(screen.height / 256));
  for (var i = 0; i < n; i++) {
```

### _Goal: Time to resize pizzas is less than 5 ms using pizza size slider._

### Steps taken:
1. Remove function 'determineDx' in 'main.js' and simplify 'changePizzaSizes'
```
function changePizzaSizes(size) {
  switch(size) {
    case "1":
      newWidth = 25;
      break;
    case "2":
      newWidth = 33.33;
      break;
    case "3":
      newWidth = 50;
      break
    default:
      console.log("bug in sizeSwitcher");
  }
  var allpizza = document.querySelectorAll(".randomPizzaContainer");

  for (var i = 0; i < allpizza.length; i++) {
    allpizza[i].style.width = newWidth + '%';
  }
}
```
