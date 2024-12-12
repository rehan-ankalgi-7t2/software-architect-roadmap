Event capturing is the opposite of event bubbling in the DOM (Document Object Model). While event bubbling involves the propagation of an event from the target element up through its ancestors, 

> event capturing involves the downward propagation of an event from the root of the DOM hierarchy down to the target element.
> 

In JavaScript, you can use the **`addEventListener`** method with the third parameter set to **`true`** to enable event capturing. Here's an example:

```html
<div id="outer">
  <div id="middle">
    <button id="inner">Click me</button>
  </div>
</div>
```

JavaScript code to demonstrate event capturing:

```jsx
document.getElementById('outer').addEventListener('click', function (event) {
  console.log('Outer div clicked during capturing');
}, true);

document.getElementById('middle').addEventListener('click', function (event) {
  console.log('Middle div clicked during capturing');
}, true);

document.getElementById('inner').addEventListener('click', function (event) {
  console.log('Button clicked during capturing');
}, true);
```

If you click the button, you will see the following output in the console:

```css
Button clicked during capturing
Middle div clicked during capturing
Outer div clicked during capturing
```

In this example, the third parameter **`true`** is passed to **`addEventListener`**, enabling event capturing. The order of execution of event listeners during capturing is from the root to the target element.

**Note** that in practice, event capturing is less commonly used than event bubbling. Most event handling is done during the bubbling phase. However, understanding both phases is important for handling events effectively in complex DOM structures. 

<aside>
💡 If you don't explicitly specify **`true`** as the third parameter, the default behavior is event bubbling.

</aside>

## Real world scenarios where `event capturing` can be used

1. **Global Event Handling:**
Event capturing allows you to set up global event handlers at the document level during the capturing phase. This can be useful for scenarios where you want to capture events at the very beginning of their lifecycle.
    
    ```jsx
    document.addEventListener('click', function (event) {
      console.log('Global click event captured');
    }, true);
    ```
    
2. **Event Delegation:**
Event delegation is a pattern where a single event listener is added to a common ancestor of multiple elements, and events are captured or bubbled to that ancestor. Event capturing can be used for event delegation to capture events as they come down the DOM hierarchy.
    
    ```html
    <ul id="list">
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
    ```
    
    ```jsx
    document.getElementById('list').addEventListener('click', function (event) {
      if (event.target.tagName === 'LI') {
        console.log('List item clicked:', event.target.textContent);
      }
    }, true);
    ```
    
3. **Focus Management:**
Event capturing can be used for managing focus-related events, such as capturing focusin or focusout events on a container element.
    
    ```jsx
    document.getElementById('container').addEventListener('focusin', function (event) {
      console.log('Element focused in:', event.target);
    }, true);
    ```
    
4. **Custom Event Frameworks:**
In custom event frameworks or libraries, capturing phases might be used for specific tasks during the event lifecycle.
    
    ```jsx
    // Custom event framework
    const eventDispatcher = new EventTarget();
    
    eventDispatcher.addEventListener('customEvent', function (event) {
      console.log('Custom event captured:', event.detail);
    }, true);
    
    // Triggering a custom event
    eventDispatcher.dispatchEvent(new CustomEvent('customEvent', { detail: 'Event data' }));
    ```
    

While these scenarios exist, it's essential to note that event capturing is often less common in everyday development, and event bubbling is sufficient for most use cases. It's crucial to choose the event phase based on your specific requirements and the structure of your DOM.
