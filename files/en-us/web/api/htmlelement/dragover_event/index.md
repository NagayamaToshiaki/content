---
title: 'HTMLElement: dragover event'
slug: Web/API/HTMLElement/dragover_event
page-type: web-api-event
tags:
  - API
  - DOM
  - HTMLElement
  - DragEvent
  - Event
  - Reference
  - Web
  - drag and drop
browser-compat: api.HTMLElement.dragover_event
---
{{APIRef}}

The `dragover` event is fired when an element or text selection is being dragged over a valid drop target (every few hundred milliseconds).

The event is fired on the drop target(s).

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Bubbles</th>
      <td>Yes</td>
    </tr>
    <tr>
      <th scope="row">Cancelable</th>
      <td>Yes</td>
    </tr>
    <tr>
      <th scope="row">Default action</th>
      <td>Reset the current drag operation to "none".</td>
    </tr>
    <tr>
      <th scope="row">Interface</th>
      <td>{{domxref("DragEvent")}}</td>
    </tr>
    <tr>
      <th scope="row">Event handler property</th>
      <td>
        {{domxref("GlobalEventHandlers/ondragover", "ondragover")}}
      </td>
    </tr>
  </tbody>
</table>

## Examples

### A minimal drag and drop example

In this example, we have a draggable element inside a container. Try grabbing the element, dragging it over the other container, and then releasing it.

We use three event handlers here:

- in the `dragstart` event handler, we get a reference to the element that the user dragged
- in the `dragover` event handler for the target container, we call `event.preventDefault()`, which enables it to receive `drop` events.
- in the `drop` event handler for the drop zone, we handle moving the draggable element from the original container to the drop zone.

For a more complete example of drag and drop, see the page for the [`drag`](/en-US/docs/Web/API/HTMLElement/drag_event) event.

#### HTML

```html
<div class="dropzone">
  <div id="draggable" draggable="true">
    This div is draggable
  </div>
</div>
<div class="dropzone" id="droptarget"></div>
```

#### CSS

```css
body {
  /* Prevent the user selecting text in the example */
  user-select: none;
}

#draggable {
  text-align: center;
  background: white;
}

.dropzone {
  width: 200px;
  height: 20px;
  background: blueviolet;
  margin: 10px;
  padding: 10px;
}
```

#### JavaScript

```js
let dragged = null;

const source = document.getElementById("draggable");
source.addEventListener("dragstart", event => {
  // store a ref. on the dragged elem
  dragged = event.target;
});

const target = document.getElementById("droptarget");
target.addEventListener("dragover", event => {
  // prevent default to allow drop
  event.preventDefault();
});

target.addEventListener("drop", event => {
  // prevent default action (open as link for some elements)
  event.preventDefault();
  // move dragged element to the selected drop target
  if (event.target.className == "dropzone") {
    dragged.parentNode.removeChild(dragged);
    event.target.appendChild(dragged);
  }
});
```

#### Result

{{EmbedLiveSample('A minimal drag and drop example')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- Other drag and drop events:

  - {{domxref("HTMLElement/drag_event", "drag")}}
  - {{domxref("HTMLElement/dragstart_event", "dragstart")}}
  - {{domxref("HTMLElement/dragend_event", "dragend")}}
  - {{domxref("HTMLElement/dragenter_event", "dragenter")}}
  - {{domxref("HTMLElement/dragleave_event", "dragleave")}}
  - {{domxref("HTMLElement/drop_event", "drop")}}

- This event on other targets:

  - {{domxref("Window")}}: {{domxref("Window/dragover_event", "dragover")}} event
  - {{domxref("Document")}}: {{domxref("Document/dragover_event", "dragover")}} event
  - {{domxref("SVGElement")}}: {{domxref("SVGElement/dragover_event", "dragover")}} event