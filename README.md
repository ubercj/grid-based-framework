# Grid-based Framework

This is the final project in the CSS portion of The Odin Project's full-stack web development curriculum. You can read more about this assignment [here](https://www.theodinproject.com/paths/full-stack-ruby-on-rails/courses/html-and-css/lessons/design-your-own-grid-based-framework).

The prompt is pretty open-ended, it's basically just "create a simple grid-based framework." The [960 grid system](http://960.gs/) was linked for inspiration. I was surprised - and impressed - at how relatively simple the CSS behind that framework is. Something feels a little bit wrong about using defined pixel values for the grid, though. One of my favorite things about working with Bootstrap was how easy it was to make a layout responsive for different screen widths.

So, my two biggest priorities when designing this framework were:
* It should be responsive and mobile-first
* It should be easy to extend and customize

I think I did a pretty good job with the first one, and I took a decent stab at the second one without reinventing Bootstrap. It felt right to use percentages for as many of the width/height values as possible because I think it should make the layout more flexible. It seems like most framework use specific pixel values, though, so I fully acknowledge that I may not be knowledgeable enough to understand using percentages instead might be a bad idea.

Full disclosure: I also used this project as an opportunity to practice using Sass, so there is certainly room for improvement on how I used mixins, imports, and variables.

## Using and extending the framework

Clearly, this framework is just a starting point for a more fleshed-out layout and design. You can add your own custom styles to layer on top of the basic grid layout included in the framework. A good way to do this is:

* Create a new .scss file with your custom classes, styles, etc. and name it whatever you want.
* Change the `@use 'demo'` line at the top of `main.scss` to `@use 'your_filename_here'` - whatever you named your file.
* If you're using Sass in your CLI, run `sass sass/main.scss style.css` to compile everything into the css stylesheet.
* Make sure the stylesheet is imported at the top of the html document:
```
<link rel="stylesheet" href="style.css">
```

## How the grid works

Conceptually, the grid is pretty simple. The parent element is divided into 12 columns of equal width. An element with a class of `.grid_4`, for example, will span 4 of these equal columns (thus taking up 1/3 of the total width of the parent).

### Rows

New rows can be added easily with the `.row` class, which has pretty minimalist styling by default:

```
.row {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
}
```

### Gutters

Gutter widths can be customized via the `$gutter-x` and `$gutter-y` variables, and the widths of columns and offsets will be updated automatically using the nifty math available with Sass. These are the default values:

```
$grid-columns: 12;
$gutter-x: 1%;
$gutter-y: 1rem;
$cell-width: math.div((100% - ($grid-columns * $gutter-x)), $grid-columns);
```

For now, the grid classes only go up to 12 (`.grid_12` for example), so it's best not to change `$grid-columns` unless you're prepared to add to the underlying `main.scss` file.

### Offsets

Offsets can be used for more fine-tuned positioning of columns or adding defined whitespace. These are also fairly simple calculations. For example, a left offset spanning 6 columns (half of the parent) looks like this:

```
.left_offset_6 {
  margin-left: ($cell-width * 6) + ($gutter-x * 6.5);
}
```

## Responsiveness

It was really important to me that this framework would be customizable for different screen sizes. To that end, I basically took a page out of [Bootstrap's book](https://getbootstrap.com/docs/5.0/layout/grid/#responsive-classes) and created classes that cover 3 media queries, with mobile being the default, and options for designating separate layouts for tablets and desktop screens. Like Bootstrap, I like how much control this gives you over the layout.