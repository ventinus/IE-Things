# IE-Things
Things I've learned about IE that you wouldn't normally expect... among other cross-browser JS things

#### Scroll event listener:
**normal:**
  `window.addEventListener('scroll', callback, false);`

**in IE:**
  `document.body.addEventListener('scroll', callback, false);`
  

#### Measure amount scrolled (distance to top of document):
**normal:**
  `window.scrollY;`
  or
  `$(window).scrollTop();`
  
**IE only measures correctly with:**
  `document.body.scrollTop;`
  
**Firefox only measures correctly with:**
  `window.scrollY;`


#### Measure distance between top of document and top of element
**normal (with jQuery):**
`$(element).offset().top`

or (without jQuery), you need to add up all the parents offsets to get the total offset to top of document:
```
function findTotalOffset(element) {
  var ol = ot = 0;
  if (element.offsetParent) {
    do {
      ol += element.offsetLeft;
      ot += element.offsetTop;
    } while (element = element.offsetParent);
  }
  return {left : ol, top : ot};
}
```
_note: IE measures it as the distance to the top of the window so it is advisable to cache all of the offsetTop values on pageload to provide accurate measurements of scroll points._

####2 Columns with equal height (without table and table-cell)####
basic markup (slim)
```
.container
  .col.col--1
    .content a little content
  .col.col--2
    .content
      .content__row
      .content__row
      .content__row
```

css to accompany:
```
.container {
  display: block;
  position: relative;
}

.col {
  width: 50%;
  height: 100%;
}

.col--1 {
  min-height: 500px; /* or whatever you need */
}

.col--2 {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
}

.content {
  height: 100%;
}

.content__row {
  display: block;
  height: calc(100% / 3);
}
```

####Using inline-block and font-size 0####
**Issue:** IE-10 has trouble resizing when you calculate the width of the elements meant to be next to each other.

For example, you would normally...
```
.container {
  display: block;
  font-size: 0;
}

.container > * {
  display: inline-block;
  font-size: initial;
  width: calc(100% / 3);
}
```
This results in basically every other pixel of resizing in pushing the last element to the next row rather than keeping it all together and inline. I believe the issue may lie in the `font-size: initial;` part but more research is needed. For now, a workaround is to change the width calculation of the children to `width: calc(99.999% / 3);` so you only end up losing .003% or something similarly minimal and unnoticeable.
