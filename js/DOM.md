# JS DOM

# Table of contents 

- [JS DOM](#js-dom)
- [Table of contents](#table-of-contents)
	- [1. DOM](#1-dom)
		- [1.1. DOM Document](#11-dom-document)
			- [1.1.1. Accessing elements:](#111-accessing-elements)
			- [1.1.2.Changing content:](#112changing-content)
			- [1.1.3. Changing attributes:](#113-changing-attributes)
			- [1.1.4. Change styles:](#114-change-styles)
			- [1.1.5. Adding and deleting elements:](#115-adding-and-deleting-elements)
			- [1.1.6. Adding event handlers:](#116-adding-event-handlers)
			- [1.1.7. Useful `document` properties:](#117-useful-document-properties)
		- [1.2. DOM Validate](#12-dom-validate)
			- [1.2.1. Form](#121-form)
			- [1.2.2. Numeric input](#122-numeric-input)
		- [8.3. DOM CSS](#83-dom-css)
		- [1.4. DOM Animation](#14-dom-animation)
		- [1.5. DOM Event](#15-dom-event)
			- [1.5.1. Usage](#151-usage)
			- [8.5.2. Common Event Types (using with addEventListener)](#852-common-event-types-using-with-addeventlistener)
		- [1.6. DOM Navigation](#16-dom-navigation)
		- [1.7. DOM Nodes](#17-dom-nodes)
		- [1.8. Nodes](#18-nodes)
		- [1.9. Collections](#19-collections)
		- [1.10. Node Lists](#110-node-lists)


## 1. DOM

- Is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document
- With the object model, JavaScript gets all the power it needs to create dynamic HTML:
  - JavaScript can change all the HTML elements in the page
  - JavaScript can change all the HTML attributes in the page
  - JavaScript can change all the CSS styles in the page
  - JavaScript can remove existing HTML elements and attributes
  - JavaScript can add new HTML elements and attributes
  - JavaScript can react to all existing HTML events in the page
  - JavaScript can create new HTML events in the page

**`innerText` and `innerHTML`**:
| Property | Returns | Includes HTML tags? | Affected by CSS? |
| ------------- | ------------------ | ------------------- | ---------------- |
| **innerText** | Visible text only | No | Yes |
| **innerHTML** | Text + HTML markup | Yes | No |

```javascript
	// innerText
	<div id="box">
	  Hello <b>World</b>
	</div>

	<script>
		let box = document.getElementById("box");
		console.log(box.innerText); // "Hello World"
	</script>

	// innerHTML
	<div id="box">
	  Hello <b>World</b>
	</div>

	<script>
		let box = document.getElementById("box");
		console.log(box.innerHTML); // "Hello <b>World</b>"
	</script>
```

- `outerHTML`: is basically `innerHTML` but also includes the element's own tag.
- `textContent`: gets or sets the all text inside an element, even the text inside hidden elements; much faster than `innerText`.
- Example:

```javascript
	<div id="box">
		Hello <b>World!</b>
		<span style="display:none">Hidden</span>
	</div>

	// innerHTML
	<script>
		let box = document.getElementById(box);
		console.log(box.innerHTML);
		// "Hello <b>World!</b>";
	</script>

	// outerHTML
	<script>
		let box = document.getElementById(box);
		console.log(box.outerHTML);
		// "<div id="box">Hello <b>World</b></div>"
	</script>

	// textContent
	let box = document.getElementById(box);
	console.log(box.textContent);
	// "Hello World Hidden"
```

### 1.1. DOM Document

- The document object represents your web page.
- If you want to access any element in an HTML page, you always `start` with accessing the `document` object.

#### 1.1.1. Accessing elements:

```javascript
document.getElementById("demo"); // return an element having `id` or null
document.getElementsByTagName("h1"); // return HTMLCollection of all <h1>
document.getElementsByClassName("myClass"); // HTMLCollection of all elements with class="myClass"
document.querySelector("#demo"); // First match of CSS selector
document.querySelectorAll("p"); // NodeList of all <p>
```

#### 1.1.2.Changing content:

```javascript
document.getElementById("demo").innerText = "Changed Text!";
document.getElementById("demo").innerHTML = "<b>Bold Text</b>";
```

#### 1.1.3. Changing attributes:

```javascript
document.getElementById("demo").setAttribute(attribute, value);
document.getElementById("demo").id = "newID"; // direct change
```

#### 1.1.4. Change styles:

```javascript
document.getElementById("demo").style.color = "red";
document.getElementById("demo").style.fontSize = "20px";
```

#### 1.1.5. Adding and deleting elements:

```javascript
	document.createElement("div"); // return element
	document.createTextNode(text); // return text node
	document.createAttribute(name); // return attribute node
	document.removeChild("div"); // return node recently deleted
	document.appendChild("element"); // return node recently added
	document.replaceChild(new, old); // return node recently replaced
	document.write(text); // write into the HTML output stream
```

#### 1.1.6. Adding event handlers:

```javascript
document.getElementById(id).onclick = function () {
  // code
};
```

#### 1.1.7. Useful `document` properties:

```javascript
document.title; // title of the page
document.URL; // current page URL
document.domain; // domain name
document.body; // body element
document.head; // head element
document.forms; // all forms
document.images; // all images
document.cookie; // cookies of the page
```

### 1.2. DOM Validate

#### 1.2.1. Form

- In the HTML DOM, a `<form>` element is represented as a `HTMLFormElement` object.
- Each form has properties (like action, method, name) and contains form controls (like `<input>`, `<select>`,`<textarea>`).
- When you put inputs inside a `<form>`, the browser has automatic input checking (validation).
- Validation can be defined by many different methods, and deployed in many different ways.
  - Server side validation is performed by a web server, after input has been sent to the server.
  - Client side validation is performed by a web browser, before input is sent to a web server.

```javascript
<form action="/action_page.php" method="post">
  <input type="text" name="fname" required>
  <input type="submit" value="Submit">
</form>
```

#### 1.2.2. Numeric input

```javascript
<!DOCTYPE html>
<html>
<body>
	<h2>JavaScript Validation</h2>
	<p>Please input a number between 1 and 10:</p>
	<input id="numb">
	<button type="button" onclick="myFunction()">Submit</button>
	<p id="demo"></p>
<script>
	function myFunction() {
	  // Get the value of the input field with id="numb"
	  let x = document.getElementById("numb").value;
	  // If x is Not a Number or less than one or greater than 10
	  let text;
	  if (isNaN(x) || x < 1 || x > 10) {
	    text = "Input not valid";
	  } else {
	    text = "Input OK";
	  }
	document.getElementById("demo").innerHTML = text;
	}
</script>
</body>
</html>
```

### 8.3. DOM CSS

Use with changing element syntax of DOM document

```javascript
<!DOCTYPE html>
<html>
<body>
	<h1 id="id1">My Heading 1</h1>
	<button type="button" onclick="document.getElementById('id1').style.color = 'red'">
Click Me!</button>
</body>
</html>
```

### 1.4. DOM Animation

### 1.5. DOM Event

#### 1.5.1. Usage

An event is something that happens in the browser that JavaScript can react to.
Examples:

- A user clicks a button
- A user types in an input
- A page loads
- A form is submitted
- A key is pressed

```javascript
// 1. inline HTML (not recommend)
<button onclick="alert('Hello!')">Click Me</button>;

// 2. Assigning to a property
const btn = document.getElementById("myBtn");
btn.onclick = function () {
  alert("Clicked!");
}; // a function is called from the event handler

// 3. Using addEventListener (best way and good habit)
const btn = document.getElementById("myBtn");
btn.addEventListener("click", function (event) {
  alert("Button clicked!");
});
```

#### 8.5.2. Common Event Types (using with addEventListener)

**Mouse Events / Pointer Events**

- \*`click` → when clicked
- \*`dblclick`→ double-click
- \*`mouseover` → when mouse enters
- \*`mouseout` → when mouse leaves
- \*`mousemove` → when mouse moves
- `contextmenu` → when right-click happens (can make - your own right-click menu).
- `wheel` → when you scroll with the mouse wheel.
- `mouseenter` → like mouseover, but doesn’t bubble.
- `mouseleave` → like mouseout, but doesn’t bubble.
- `pointerdown` / `pointerup` → works for mouse, - pen, and touch.
- `pointermove` → track finger or pen movements.

**(used on phones/tablets)**

- `touchstart` → finger touches screen.
- `touchend`→ finger lifted.
- `touchmove` → finger moves around.
- `touchcancel` → touch interrupted (e.g., phone call).

**Keyboard Events**

- \*`keydown` → key is pressed
- \*`keyup` → key is released
- `compositionstart`, `compositionend` → when typing complex input (like Chinese/Japanese IME).
- `beforeinput` → fires before input actually - changes (can block it).

**Form Events**

- \*`submit` → form is submitted
- \*`change` → input value changes (e.g., checkbox toggled)
- \*`input` → value changes while typing
- \*`focus` → input gets cursor
- \*`blur` → input loses cursor
- `reset` → when a form is reset.
- `invalid` → when form validation fails.
- `select` → when text is selected inside an`<input>` or `<textarea>`.

**Window/Document Events**

- \*`load` → page loaded
- \*`resize` → window resized
- \*`scroll` → page scrolled
- `DOMContentLoaded` → fires when HTML is loaded before images/css (faster than load).
- `beforeunload` → fires before leaving page (used for “Are you sure you want to leave?”).
- `visibilitychange` → when the page is hidden (user changes tab).

**Media Events (audio/video)**

- `play` → video/audio starts playing.
- `pause` → video/audio paused.
- `ended` → playback finished.
- `volumechange` → volume changed.
- `timeupdate` → current play time updated.

**Drag & Drop Events**

- `dragstart` → when drag begins.
- `dragover` → while dragging over a target.
- `drop` → when dropped.
- `dragend` → when dragging ends.

**Special UI Events**

- `animationstart`, `animationend`, - `animationiteration` → CSS animation lifecycle.
- `transitionend` → CSS transition finished.
- `fullscreenchange` → when entering or exiting fullscreen.
- `copy`, `cut`, `paste` → clipboard events.

(NOTE: `*` is solid foundation)

### 1.6. DOM Navigation

### 1.7. DOM Nodes

### 1.8. Nodes

### 1.9. Collections

### 1.10. Node Lists