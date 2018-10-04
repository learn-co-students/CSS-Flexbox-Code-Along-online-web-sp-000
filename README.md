# Building a Responsive Layout with CSS Flexbox 
## Problem Statement 
Using CSS to create a website that looks good to as many users as possible can
be a challenge. Your webpage may look great on the screen you designed it on,
but if you open the page up on a small laptop, suddenly the page content is
squeezed, spilling over, or pushed out of place. If you open that same page
on a larger monitor, you might see excess empty space.

However, CSS has some powerful solutions for this. In this lesson we will
be discussing one of them: flexbox.

Flexbox makes it easier to build page layouts that are dynamic. As the
designer of a web page, you can designate some parts of your page to
automatically resize depending on window size, filling empty space in a way that
you specify. It is also very useful for displaying columns or rows of items,
keeping items evenly spaced regardless of their individual sizes, or allowing
them to _wrap_ to a new line cleanly.

In this lesson, we will discuss some of the common ways to use flexbox and the
associated properties you can use while coding through some examples. Feel free
to code along using the provided `index.html` and `index.css` files. You can
test out your page by either running `httpserver` if you are using the
in-browser Learn IDE, or by right clicking the `index.html` in Finder and
opening it in a browser.

## Objectives
1. Setting up a Flex Container
2. Identify and Use Flex Properties

## Setting Up a Flex Container

In order to use flexbox properties, we must first define a container where we
want flexbox to apply. In `index.html`, we've already defined some HTML in the
`<body>`: a `<div>` element with a class of 'flex-container' that has three child
elements called `<header>`, `<main>` and `<footer>`, which will act as our first
flex container. In `index.css`, there's some starter code, too. We've set pre-defined
attributes of `background-color`, `width` and `height` for the `header`, `main`,
and `footer` elements.

First, create a block in `index.css` called `.flex-container`, which will define
CSS for our 'flex-container' class. To apply flexbox, we need to add `display:
flex` as a property here and set a width and height of the container. We can
also set width and height to the full size of the window using `100vw`, and
`100vh`, so our CSS block will look like this:

```
.flex-container {
  display: flex;
  width: 100vw;
  height: 100vh;
}
```

## Identify and Use Flex Properties
Save `index.css` and check out `index.html` in your browser. Cool! We're taking
some inspiration from nature today, and going with colors that look like you're
oceanside. Looks like we're on our way! If you inspect the page, you'll see that
the three sections displayed are actually our `<header>`, `<main>` and
`<footer>` elements. Note, too, that the three sections are evenly dividing the
page. If you resize your browser window, the three sections will stay evenly
split, expanding and shrinking to fit. With just a little bit of CSS, we've
already got some responsiveness!

However, we've got a small issue--it doesn't make much sense to have a
`<header>` on the left and a `<footer>` on the right; they should be on the top
and bottom of our page. We'll need to add one more line of CSS for this using
`flex-direction`.

#### `flex-direction`

By default, flexbox will display content horizontally. If we want to change
this, we'll need to define a direction. In `index.css`, add the following line
to `.flex-container`: 

```
flex-direction: column;
```

Refresh `index.html` to see the change. This time, our ivory `<header>` appears
along the top of our page, with `<footer>` at the bottom! 

The `flex-direction` property has a few setting options:

* `row` - the default setting, organizes items from left to right
* `column` - organizes items from top to bottom
* `row-reverse` - organizes items from _right_ to _left_
* `column-reverse` - organizes items from _bottom_ to _top_

Switching `flex-direction` to the `column-reverse` setting, for instance, will
put our pale blue `<footer>` on top, and our ivory `<header>` on the bottom.

We'll go ahead and keep the setting as `column` so our elements are in logical
order, but our `<header>` and `<footer>` sections are quite large. Go back into
`index.css`, and in the `header` block, change the `height` property to `10%`,
then check the page out in your browser.

This time, our `<header>` is much shorter. More importantly, though, our
`<main>` and `<footer>` sections have actually expanded, evenly filling the
remainder of the page. The height of our `<header>` is now 10% of the parent
container, which, in this case, is the height of our window.

It likely makes more sense to set a specific height to `<header`>, as it will most
often contain navigation and a website logo that we want to keep at a consistent
height. Similarly, footers usually contain static links and information, so we will
set the height property in the `header` and `footer` CSS blocks to `80px`.

Refresh the page and you'll see the effect: The `<main>` section will display as
turqoise and tke up the majority of the page. If you shrink the height of your browser
window, the height of `<main>` will change significantly. Our `<header>` and
`<footer>` sections will still adjust in height a little, but we'll take a look
at preventing that later on. Previously, to create this sort of layout, we would
have added the `position` property to the individual `<header>` and `<footer>`
elements, but with flexbox, the position is being handled by the _parent
container_, applying to all of its children.

Now that we've set up a basic layout using flexbox, we can go deeper into some
of its cool properties.

#### `flex-wrap`

Let's display a series of items in the `<main>` section of our page. Make six
`<div>` elements inside of `<main>` and assign them a class name 'item', adding
the number 1 through 6 in them, like so:

```
<div class="item">1</div>
<div class="item">2</div>
<div class="item">3</div>
<div class="item">4</div>
<div class="item">5</div>
<div class="item">6</div>
```

In our CSS file, define a block for `.item` with `height` and `width` set to
`100px`, `margin` set to `5px`, and `background-color` set to `#FCF2EC`. Now, in
the `main` CSS block, set `display` to `flex`. The two classes should look like
the following:

```
main {
  display: flex;
  background-color: #FBFFF4;
  width: 100%;
  height: 100%;
}

.item {
  height: 100px;
  width: 100px;
  margin: 5px;
  background-color: #FCF2EC;
}
```

If you refresh, you should see six pink boxes horizontally aligned. If you reduce
the width of your browser window, these boxes will evenly shrink to fit. Go back
into `index.css`, and in `.main`, add the following line:

```
flex-wrap: wrap;
```

Now, if you refresh the browser, grow and shrink the window, the boxes will stay
100 pixels wide, _and 'wrap' to a new line_ one by one when there is no more
space to fit! The `flex-wrap` property defines how items in a flex container
handle positioning when there are too many items to fit the space. By default,
`flex-wrap` is set to `nowrap`, which is what we saw initially. You can also try
changing `flex-wrap` to `wrap-reverse`, which will act similar to `wrap`, except
from the _bottom and up_, instead of top and down. We'll keep the property set
to `wrap` for now, though.

Let's add in the previous property we discussed, `flex-direction`. If you add
`flex-direction: column` to the `main` CSS block, flexbox will still _wrap_
items, but instead of in a new line underneath, the items will appear in a new
_column_ to the right of the first.

#### `flex-flow`

In our CSS block labeled `main`, we've now got `flex-direction` and `flex-wrap`
defined. These two properties often go hand in hand, so CSS provides a shorthand
property that defines both in one line: `flex-flow`. To implement this, in
the block `main`, replace `flex-direction` and `flex-wrap` with the following:

```
flex-flow: column wrap;
```

The `flex-flow` property takes in two settings, the first for direction and the
second for wrapping. If you only include one setting, the other will be set to
its default, `row` or `nowrap`.

Again, notice we've only defined flex properties in the parent element, using
`main`. We're effectively letting our browser decide how to handle the
positioning of the child divs with these two lines of CSS for the parent. For
the next section, switch the direction back to `row` (so, either `flex-flow: row
wrap;`, or just `flex-flow: wrap;`).

#### justify-content

Now that we've got wrapping and direction set up, we can define where we want
items positioned in more detail. The first property we will look at is
`justify-content`, which will define where items start and end, and how they are
spaced in between. In the `main` CSS block, add:

```
justify-content: center;
```

Now, our six pink boxes are centered together on the page. Wrapping will still
apply here, so if the page shrinks enough, some of the boxes will spill over,
but _remain centered on the next row_. Very cool! Getting HTML elements to
behave this way _without_ flexbox is actually fairly difficult, but we've got it
set up in short order.

The `justify-content` property has a number of settings:

* `center` - centers all elements while preserving the original spacing in-between
each of them. 
* `flex-start` - aligns all elements to the beginning of the container. This is
the default setting, so we've actually already seen what this looks like. 
* `flex-end` - aligns all elements to the end of the flex container. If you apply
this setting, our pink boxes will align to the right side of the screen.
However, if the page shrinks, the last flex elements will still wrap to the next
row, so order is preserved.
* `space-around` - adds space in between each flex element so they fill the space
they are in, evenly dividing the row and centering each element in each
division. This white space in between will shrink as the page shrinks, and items
will wrap when they no longer fit on the same row.
* `space-between` - similar to `space-around`, except this time, the _first_ and
_last_ flex elements on a row will be aligned to the beginning and end of the
row, removing white space on the edges of the container. On a new row, the first
and last elements will again align to the beginning and end.

If you change `flex-flow` back to `column wrap`, the flex elements will act the
same way, _only vertically_, so `justify-content` will apply based on the
`flex-direction` you've defined.

#### `align-items`

Centering vertically is actually fairly non-intuitive using basic CSS. Flexbox
provides a solution, though, in the `align-items` property. In the `main` CSS
block, make sure `flex-flow` is set to `row wrap` once again, and then add the
following line: 
```
align-items: center;
```

Save, then refresh your page in the browser and take a look. Now, our pink boxes
are centered _vertically_ within our `<main>` container. If the window shrinks,
the elements will wrap as expected, and each row will center within its own
space. Now, go back to your `flex-flow` setting and change it from `row` to
`column`. Our flex elements will now be centered _horizontally_. So, where
`justify-content` will arrange flex elements in the same direction that you've
defined in `flex-direction` or `flex-flow`, `align-items` will arrange elements
in the direction **perpendicular** to your `flex-direction` setting.

Just like `justify-content`, the `align-items` property has a few different
settings:

* `center` - centers elements vertically if the `flex-direction` is set to `row`, and horizontally if the `flex-direction` is set to `column`.
* `flex-start` - aligns elements to the top of the flex container if `flex-direction` is set to `row`, and to the left of the container if `flex-direction` is set to `column`.
* `flex-end` - aligns elements to the bottom or right of the flex container, the opposite of `flex-start`.
* `stretch` - Stretches elements to fit the container. Try this by setting `align-items` to `stretch`, then make sure `flex-flow` is set to `row wrap`, and in the `.item` CSS block, remove `height: 100px`. Each element will now stretch to fit the height of the flex container. The `stretch` setting will have the same effect on flex columns if you add back in the `height` property but remove `width: 100px`.
* `baseline` - aligns elements based on the _text_ baseline inside each element. If you tried out the `stretch` setting, make sure your `flex-direction` is set back to `row` and that both `height` and `width` are set to `100px` in the `.item` CSS block. Now, set `align-items` to `baseline`, go to your `index.html` file and remove some of the numbers that are contained in our divs, leaving a few. Save both the HTML and CSS, and check out the page in your browser. Any div that is now empty is aligned normally, but any div that still has text in it will align _based on the bottom of the text_.

To perfectly center an element horizontally and vertically, with flex, we can
use a combination of both `justify-content` and `align-items` like so: 

```
justify-content: center;
align-items: center;
```

#### `align-content`

The `align-content` property defines how multiple rows of elements will be
displayed. The effects of `align-content` will not apply if `nowrap` is set, and
won't be visible until more than one row or column of flex content is present.
Because of this, it is often best to use `align-content` in conjunction with
`align-items`, giving you a more nuanced control over the effects of wrapping.

* `center` - centers all rows in the container. Combined with `align-items: center`, this will keep all items and rows grouped together, instead of centering each row independently.
* `stretch` - similar to `align-items: stretch` when multiple rows are present.
* `space-around` - centers elements vertically on each row (or horizontally on each column) the same way as if you only used `align-items: center`.
* `space-between` - similar to `justify-content: space-between`, if two rows of elements are present, the first row will align to the top of the container, and the second row will align to the bottom. Any additional rows will be evenly centered and spaced in between.
* `flex-start` - aligns elements to the beginning of the flex container
* `flex-end` - aligns elements to the end of the flex container

### Setting Up Child Elements with Flex

So, we've gotten pretty far with flexbox just by defining properties on the
container, but we can go even further by setting CSS properties within the
children of the container.

#### `flex-basis`

So far, we've been setting the size of our child elements in a flex container by
using the `width` and `height` properties. We can achieve the same effect using
the `flex-basis` property, which determines the initial width of an element in a
flex container. Width, in this case, refers to the length of an element in the
`flex-direction` assigned, so if `flex-direction` is set to `column`,
`flex-basis` affects the `height` of each element. There are a few settings for
`flex-basis` we can use, allowing us to handle sizing in different ways:

* `flex-basis: 100px;` - will give elements an initial width of `100px`, if the container is set to `row`, or an initial height of `100px`, if the container is set to `column`. Other units can be used here, such as `em`.
* `flex-basis: --%` - will set the element to a percentage of a container size. Setting `flex-basis` to 50% on one child element, for instance, will cause that child to take up half of a container row. Set to 100%, the child will fill the entire row, causing it to wrap if there are other children in the flex container.
* `flex-basis: content;` - will set the element's size based on the `width` or `height` properties if they are defined. Otherwise, the element will be sized based on the content inside the element.

#### `flex-grow`

The `flex-grow` property specifies how much space the element should take up
within a flex container. By default, `flex-grow` is equal to `0`, meaning
elements that do not have `flex-grow` specifically defined will not grow larger
than the `width`, _for rows_, `height`, _for columns_, or `flex-basis` they are
set to, producing the wrapping effect we've seen so far - all of our child
elements remain the same size, and spill over into a new line if they don't fit.

Assigning a `flex-grow` value greater than `0` changes this behavior, allowing a
child element to expand. The higher the number, the more space an element will
take up, relative to its siblings. For instance, if we had just two child
elements, the first with `flex-grow` set to `1`, and the second with `flex-grow`
set to `2`, the second element will be twice as wide as the first.

One way to think of this: in total, the sum of all `flex-grow` values, `1` and
`2` equals 3, so `flex-grow: 1;` is 1/3 of the row; if the sum of all
`flex-grow` values was 12, `flex-grow: 1;` would be 1/12 of the row.

The `flex-grow` property can be used in conjunction with a set width which can
create a variety of layouts. For instance, let's create a new CSS class,
`setWidth`, with `flex-basis` set to `100px`, and `flex-grow` set to `1`, like
so:

```
.setWidth {
  flex-basis: 100px;
  flex-grow: 1;
}
```

Then, for all of the pink child divs in our flex container, set the classes to
be `class="item setWidth"`, we get a cool effect - elements will still wrap if
the container size can't fit them in a line, but all elements will expand in
size to fill any empty space, so if one pink box is on a new line, it fills 100%
of the space, while all other boxes will fit evenly on their row.

If no divs have a set width, but have `flex-grow` set greater than `0`, elements
_will not_ wrap, instead, shrinking to fit all into one row.

#### `flex-shrink`

The `flex-shrink` property determines how much an element in a flex container will
shrink; the larger the number, the more the element will shrink in relation to
other elements in the container, with the default set to `1`. To see this in
action, let's go back to our the first flex container where `<header>`,
`<main>`, and `<footer>` are the children. Currently, although we've set the
height of `header` and `footer`, if the page is shortened, these sections will
still shrink to fit.

In your CSS file, under `header`, add `flex-shrink: 0`, and under `footer`, add
`flex-shrink: 3`. Check out `index.html` in your browser and you can see that
our `<header>` is no longer changing size. Setting `flex-shrink` to `0` will
stop an element from shrinking to fit.

But what about our `<footer>`? Adjusting the height of the browser window will
now cause the `<footer>` to shrink much more than before until it disappears
entirely. Setting `flex-shrink` to `3` causes the `<footer>` to shrink _3_ times
as much as normal.

#### `flex`

Using `flex-grow`, `flex-shrink`, and `flex-basis` in combination allows us to:
1. Set how much that element expands to fill space
2. Set how much the element will shrink to fit
3. Set how large the item is to start

These three settings tend to go together, and because of this, CSS has provided
a shorthand alternative to set all three: `flex`. The `flex` attribute can take
three settings:

```
flex: <flex-grow value> <flex-shrink value> <flex-basis value>
```

Alternatively, you can also use `auto`, `initial` and `none`:

* `flex: auto` - equal to `flex-grow: 1; flex-shrink: 1; flex-basis: content;`, elements set to this will grow and shrink evenly to fit the container.
* `flex: initial` - equal to `flex-grow: 0; flex-shrink: 1; flex-basis: content;`, elements with this settings will shrink to fit, but will not grow beyond their set width or the size of their content.
* `flex: none` - will prevent shrinking and growing, keeping elements to a set size or the size of their content.
* `flex: 1` - or any value greater than `0` - will act the same as `flex-grow: 1`.
* `flex: 100px` - or any valid width - will act the same as `flex-basis: 100px`.

It is recommended that you use `flex` over the individual `grow`, `shrink` and
`basis` properties. Since `flex` automatically handles some of the settings if
they aren't provided, it is less prone to conflicting behavior. Try assigning
our pink boxes different values for `flex` to see how they work.

#### `align-self`

Flexbox offers a way for us to change individual element positions, in the event
that we want one or more elements in a flex container to be positioned
differently than the rest. For instance, if we create a new class, assign
`align-self` to `flex-end` and add that class to one of our pink boxes, when we
take a look at it in browser, we will see that while that pink box will remain
in order relative to other boxes, it will appear at the bottom of the flex
container, while all others remain at the top.

#### `order`

Flexbox has one property which is slightly different than the rest: `order`. The
`order` takes in a positive or negative number value, and will cause flex
container children to rearrange based on ascending numerical value.

On a simple webpage like the one we've created during this lesson, `order` isn't
necessary (we could always just manually rearrange the order of elements we
want, right?). However, if you're building a fully responsive website, you may
realize your page layout needs to change depending on the screen size of a
visitor. For instance, on mobile, say you want to emphasize one element, such as
moving a submit button for ease of use, but on a computer screen, the button can
stay in the original order it is written in the HTML.   We could accomplish this
using `order` in conjunction with [`@media`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media).

It should be noted that modifying the order of elements may negatively affect
users who use assistive technology such as screen readers.

## Moving On

When you're ready to leave this lab, run `learn` from the command line. If the
test pass, enter `learn submit`. You'll then be prompted to move on!

### Conclusion

That covers all the properties of flexbox, but feel free to continue to practice
with various settings. It is possible to use flexbox to create very unique page
layouts, recreate some of the awesome modern layouts we see (i.g. the dynamic
columns you see on [pinterest.com](pinterest.com)), or just add a little more
responsiveness to make your site look good regardless of how big or how small
your user's screen is.
