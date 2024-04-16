# fidget-photo
a simple rotatable and draggable photo modal made using javascript and html/css
<br><li>to rotate = use mouse wheel
<br><li>to drag = hold left mouse button
<br><br>![modal](https://shinminase.neocities.org/photos/modal.gif)
## css
```css
  .draggable {
    position: absolute;
    cursor: grab;
  }

  .draggable:active {
    cursor: grabbing;
  }
```

## html
```html
<!-- put ur photo here -->
<img id="myPhoto" class="draggable" src="https://i.pinimg.com/564x/c9/1e/49/c91e4922fa4f69a623c9bf56d06f8783.jpg" alt="photo" style="width:100%;max-width:300px">
 <!-- adjust as wanted. remove "style="width:100%;max-width:300px" if u want original image resolution-->
```
## javascript 
```javascript
  var img = document.getElementById("myPhoto");
  var pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;

  // when the user clicks and holds the image it should drag
  img.onmousedown = dragMouseDown;

  function dragMouseDown(e) {
    e = e || window.event;
    e.preventDefault();
    pos3 = e.clientX;
    pos4 = e.clientY;
    document.onmouseup = closeDragElement;
    document.onmousemove = elementDrag;
  }

  function elementDrag(e) {
    e = e || window.event;
    e.preventDefault();
    pos1 = pos3 - e.clientX;
    pos2 = pos4 - e.clientY;
    pos3 = e.clientX;
    pos4 = e.clientY;
    img.style.top = (img.offsetTop - pos2) + "px";
    img.style.left = (img.offsetLeft - pos1) + "px";
  }

  function closeDragElement() {
    document.onmouseup = null;
    document.onmousemove = null;
  }

  // make the image rotatable via mouse wheel
  var angle = 0;
  img.onwheel = function(e) {
    e.preventDefault();
    angle += e.deltaY * 0.1;
    img.style.transform = "rotate(" + angle + "deg)";
  };
```
