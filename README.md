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
  
**Firefox only measure correctly with:**
  `window.scrollY;`
