> An event triggered on a specific child element will bubble up the DOM hierarchy through it’s ancestor elements
> 

i.e. the event triggered on a child will be triggered on all of it’s ancestors

- this is a default DOM action when an event is triggered

Consider the following HTML structure:

```html
<div id="outer">
  <div id="middle">
    <button id="inner">Click me</button>
  </div>
</div>
```

Now, if a click event occurs on the "Click me" button (**`#inner`**), it will trigger the click event on the button first and then propagate or bubble up through its ancestors: **`#middle`** and **`#outer`**.

JavaScript code to demonstrate event bubbling:

```jsx
document.getElementById('outer').addEventListener('click', function (event) {
  console.log('Outer div clicked');
});

document.getElementById('middle').addEventListener('click', function (event) {
  console.log('Middle div clicked');
});

document.getElementById('inner').addEventListener('click', function (event) {
  console.log('Button clicked');
});
```

If you click the button, you will see the following output in the console:

```css
Button clicked
Middle div clicked
Outer div clicked
```

This demonstrates the order in which the click event bubbles up through the DOM hierarchy.

Event bubbling can be useful, and it allows you to capture and handle events at different levels of the DOM hierarchy. However, if not handled properly, it can lead to unintended behavior.

<aside>
💡 You can stop the event from further propagation using **`event.stopPropagation()`** if you want to prevent it from reaching certain ancestors.

</aside>
