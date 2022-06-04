---
layout: default
title: "JavaScript: Basic React"
date: 2022-06-03 18:00:00
categories: JavaScript
---

## Props

#### Source Code

```javascript
<script type="text/babel">

    /*
    shortCut : 'props.text' => '{ text }'
    React.js does not know the props' type -> does not occur an error even if you pass the wrong data type
    ==> PropType: allows you to check each different types
    fontSize = 14 is the default value
    */
    function Btn({ text, fontSize = 14 }) {

        return <button
            style={{
                backgroundColor: "tomato",
                color: "white",
                padding: "10px 20px",
                border: 0,
                borderRadius: 10,
                fontSize: fontSize
            }}
        >{text}</button>
    }

    // We can set propType - is going to allow us to check which 'types' of data should be received as props
    // Also we can set isRequired which means 'Should have a value'; without a value will show an warning message
    Btn.propTypes = {
        text: PropTypes.string.isRequired,
        fontSize: PropTypes.number,
    };

    function App() {
        return (
            <div>
                <Btn text="Save Changes" fontSize={18} />
                <Btn fontSize={14} text={"Continue"} />
            </div>
        );
    }

    const root = document.querySelector(".root");
    ReactDOM.render(<App />, root);

</script>

</html>
```

## CSS modules

- There were two ways;
    1. create styles.css, then import "./styles.css"
    2. Using html like..  ```html <button style={{ ... }} > ```
- Now, using CSS modules, we can create an isolated css file for a specific component
- 예를들어 Button.module.css 에서도 클래스 이름 title 를 사용하고, App.module.css 에서도 클래스 이름 title 를 사용한다고 가정해 봤을 때, 같은 클래스 이름이라도 다르게 스타일을 적용할 수 있다.
- 즉, 스타일을 독립적으로 사용가능

#### Source Code
```javascript
import Button from "./Button";
// import "./styles.css"; 대신에 독립적으로 css 파일을 만들어 적용 할 수 있다.
import styles from "./App.module.css";

function App() {
  return (
    <div>
      <h1 className={styles.title}>Welcome back!!!</h1>
      <Button text={"Continue"} />
    </div>
  );
}

export default App;

```

## useEffect

- Normally, everytime when a state changes, the entire component is re-rendered = Codes runs repeatedly
- Then, how we can render a component when a condition is changed ?
- For examplem, when we get the data from the API, it is better to get API only once.
- There are two arguments
    - useEffect(1ST,[2ND])
        1) 1st Argument: A function which allows you running 'one' specific function at only one time.
        2) 2nd Argument: one OR more state that tells react.js 'if a specific state 'keyword' changes, run a function that is stated in 1st argument.

#### Source Code
```javascript
import { useState, useEffect } from "react";

/**
 * state 가 변화 할 때마다 전체 App 컴포넌트는 re-render 된다.
 * 처음에만 render 되게 어떻게 만들까?
 * 예를들어, api 를 통해 데이터를 가져올 때.. api 를 한번만 가져오고 state가 업데이트 될 때, re-render 되는 걸 원치 않을 것.
 * 
 * useEffect
 * 1st argument -> A function: allows us to run a specific code only one time even if a state is changed ...
 * 2nd argumrnt -> Telling react.js if only specific state 'keyword' is changed, run this code.
 */
function App() {
  const [counter, setValue] = useState(0);
  const [keyword, setKeyword] = useState("");

  const onClick = () => setValue(prev => prev + 1);
  const onChange = (event) => setKeyword(event.target.value);

  useEffect(() => {
    console.log("I run only once");
  }, []);

  useEffect(() => {
    console.log("I run when 'keyword' changes");
  }, [keyword]);

  useEffect(() => {
    console.log("I run when 'counter' changes");
  }, [counter]);

  return (
    <div>
      <input
        value={keyword}
        onChange={onChange}
        type="text"
        placeholder="Search here..."
      />
      <h1>{counter}</h1>
      <button onClick={onClick}>Click me</button>
    </div>
  );
}

export default App;

```