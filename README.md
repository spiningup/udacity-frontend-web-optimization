## Part 1 - Critical Rendering Path
### Goal: index.html achieves a PageSpeed score of at least 90 for Mobile and Desktop.

### Steps taken:
1. Add async to loading analytics.js
`<script async src="https://www.google-analytics.com/analytics.js"></script>`
2. Add media option to loading print.css
`<link href="css/print.css" rel="stylesheet" media="print">`
3. Inline 'css/style.css'
4. Compress and resize pizzeria.jpg; compress all other images
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

rewrite changePizzaSizes
update number of pizzas
