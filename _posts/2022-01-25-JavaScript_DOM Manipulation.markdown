---
layout: default
title: "JavaScript: DOM Manipulation"
date: 2022-01-25 16:00:00
categories: JavaScript
---

### What is DOM manipulation

- Browser API to interact with the browser usgin code

<em>It prodive you to do:</em>

- Build a model that pops up over your content

- Wipe parts of the page and add your own content

- Update content on the page with fresh or new data

- Track form usage and provide user feedback

- Trigger CSS animation

- Build charts, graphs, and reports... etc

<em>To select HTML with the browser API such as getElementID(), but the two simplest ways are</em>

- document.querySelector() , document.querySelectorAll() &rarr; provides you the ability to work with the browser view based on css selectors

```javascript
// Note that querySelector only return the first matching element and ignore others
// querySelectorAll always returns a collection of none, one, or many items

const content = document.querySelector(`#content`);

const header = document.querySelector(`h1`);

const bold = document.querySelector(`p strong`);

const featured = document.querySelector(`.featured`);

const paragraphs = document.querySelectorAll(`p`);

const divs = document.querySelectorAll(`div`);
```

- querySelectorAll() - to get a collection of DOM elements &rarr; Need to convert a a collection of DOM elements to as arrays

```javascript
const headers = Array.from(document.querySelectorAll(`p`));

//TO TEST
headers.map((header) => console.log(header));
```

- We can select HTML inside of elements with .innerHTML and the text inside the header with .innerText

```javascript
// <a href="http://www.naver.com">Heading</a>
console.log(title.innerHTML);

// Heading
console.log(title.innerText);

title.innerText = "something else";
```

- We can also get the attributes of any HTML elements; id,class, and href...etc

```javascript
const article = document.querySelector(`article`);

console.log(article.id);

const h2 = document.querySelector(`h2`);

console.log(h2.className);
```

### How to manipulate html and css with your JS

- If we save elements to variables we can simply override the values of the HTML text, HTML attributes, and just about everything else

```javascript
const link = document.querySelector(`.post-title a`);
// Replace the HTML inside the link with bold markup
link.innerHTML = `<strong>Hi</strong>`;

const h2 = document.querySelector(`h2`);

// Override the class and add a new one
h2.className = `post-title hidden`;
h2.innerHTML = `NEW HEADING`;
```

- You can also add a class or remove

```javascript
// Gets the <h1>
const header = document.querySelector(`h1`);

// Add class
// header.className +='main'
header.classList.add(`main`);

// Results in <h2 class="entry-header"></h2>
header.classList.add(`entry-header`);

// Removes the `main` class
header.classList.remove(`main`);
```

- For hiding an element, you can manually override the class attribute like section.class = "hidden", but using classList is recommended to add, remove, and toggle classes.

- To completely replace the class string, you would use className

- InsertAdjacentHTML() &rarr; allows us select an existing element on the page and add our element before it, inside it, or after it.

  - InsertAdjacentHTML(beforebegin) - outside of selected tag, before begin of tage
  - afterend - outside of selected tag, after end of tag
  - beforeend - inside selected tag, at the end of innerText
  - afterbegin - inside selected tag, at the end of innerText

```javascript
// Create a function for our title UI
function title(text) {
  return `<h1>${text}</h1>`;
}
// Select our app div
const container = document.querySelector(`.app`);
// Add title inside app
container.insertAdjacentHTML(`beforebegin`, title(`Hello!`));
```

### How to listen for user iinteractions on the page

- EventListeners on any element on the page
- Types of events
  - Scrolls
  - Hovers
  - Mouse movements
  - Window resize
  - Key presses...etc

Source codes

- <em>Scrolls</em>

```javascript
const button = document.querySelector("#scroll");
const footer = document.querySelector("footer");

button.addEventListener("click", scrollToFooter);

function scrollToFooter(e) {
  // find the y position of footer
  // getBoundingClientRect() method that gives us the top, left, right, and bottom position of where an element appears in the window
  const footerY = footer.getBoundingClientRect().top;
  e.preventDefault();
  // call window.scrollBy to move the window down to the footer
  window.scrollBy({
    left: 0,
    top: footerY,
    behavior: "smooth",
  });
}
```

- <em>Media Event</em>

```javascript
const video = document.querySelector("video");
const playBtn = document.getElementById("play");
const pauseBtn = document.getElementById("pause");
const restartBtn = document.getElementById("restart");
const forwardBtn = document.getElementById("skipForward");
const timestamp = document.getElementById("timestamp");

video.addEventListener("timeupdate", updateTimestamp);
playBtn.addEventListener("click", playVideo);
pauseBtn.addEventListener("click", pauseVideo);
restartBtn.addEventListener("click", restartVideo);
forwardBtn.addEventListener("click", skipForward);

function updateTimestamp() {
  timestamp.innerHTML = parseInt(video.currentTime);
}

function playVideo() {
  video.play();
}

function pauseVideo() {
  video.pause();
}

function restartVideo() {
  video.currentTime = 0;
}

function skipForward() {
  video.currentTime = video.currentTime + 10;
}
```

- <em>Other Events</em>

```javascript
// Get a DOM collection and convert to a JS array for mapping
const links = Array.from(document.querySelectorAll("nav.main a"));

// Add an event listener to each link to call sayHi() when clicked
links.map((link) => link.addEventListener("click", sayHi));

// The Browser API will give us the Event Object
function sayHi(e) {
  console.log(e);
  e.preventDefault();
  alert("Hi!");
  // Logs out the Event Object
  console.log(e);
  console.log(this);
  console.log(this.innerText);
}

// Will log out X and Y position of the mouse
document.addEventListener("mousemove", logMousePosition);

function logMousePosition(e) {
  console.log(e.clientX + " x " + e.clientY);
}

// Keyboard Events Example
document.addEventListener("keypress", logKeys);

function logKeys(e) {
  key = e.which;
  console.log(key);
  console.log(String.fromCharCode(key));
}

// Working with Form
const form = document.querySelector(`form.contact`);
form.addEventListener("submit", logFormDetails);

function logFormDetails(e) {
  e.preventDefault();
  let name = document.querySelector(`#name`);
  let email = document.querySelector(`#email`);
  let message = document.querySelector(`#message`);

  console.log(`Form Details:`);
  console.log(`Name: ${name.value}`);
  console.log(`Email: ${email.value}`);
  console.log(`Message: ${message.value}`);
}
```
