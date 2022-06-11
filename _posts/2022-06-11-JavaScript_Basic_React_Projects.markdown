---
layout: default
title: "JavaScript: Basic React Projects"
date: 2022-06-11 11:20:00
categories: JavaScript
---

## Basic projects using concepts I have learned

### 1. ToDo List

#### What I learned
- Do not modify the status directly. Use a function that modifies the state; State must always be 'New'!
- The map function takes all elements of the array and converts them into a new array.
    - If there are six elements in the array, a function is executed six times.
- ReactJS basically recognizes all of elements in the array, so you have to give them unique keys
    - The first argument = value
    - The second is index.
          ```
          toDos.map(item, index) =>
            <li key={index}>{item}</li>
          ```

### Source Code
```javascript
import { useState } from "react";

function App() {

  const [toDo, setToDo] = useState("");
  const [toDos, setToDos] = useState([]);
  const onChange = (event) => setToDo(event.target.value);

  const onSubmit = (event) => {
    event.preventDefault();
    if (toDo === "") {
      return;
    }
    // In normal js, we would use toDos.push when we want to add an element to an array
    // But, remember we never modify a state directly!! We use a function which modifies a state
    // state should be always 'NEW'
    setToDos(currentArray => [toDo, ...currentArray]);
    setToDo("");
  };

  return (
    <div>
      <h1>My To Dos ({toDos.length})</h1>
      <form onSubmit={onSubmit}>
        <input
          onChange={onChange}
          value={toDo}
          type="text"
          placeholder="Write what to do..."
        />
        <button>Add To Do</button>
      </form>
      <hr />
      <ul>
        {
          // map function does take all array's elements and transform them; transforms to a New array
          toDos.map((item, index) =>
            (<li key={index}>{item}</li>)
          )}
      </ul>
    </div>
  );
}

export default App;
```