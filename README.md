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
    }while (element = element.offsetParent);
  }
  return {left : ol, top : ot};
}
```
_note: IE measures it as the distance to the top of the window so it is advisable to cache all of the offsetTop values on pageload to provide accurate measurements of scroll points._
