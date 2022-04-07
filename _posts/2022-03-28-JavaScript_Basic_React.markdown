---
layout: default
title: "JavaScript: Basic React"
date: 2022-03-28 20:30:00
categories: JavaScript
---

### What is React?

- React is a javascript library for building user interface
- By breaking it up into small reusable pieces of code called 'Components'
- Componenets for the pieces of the UI that you will likely reuse over and over again
- The other big benefit is that React keeps your application's data or at state
- and the UI in-sync and can efficiently update you UI when data changes.

### Features

- React does not create actual DOM nodes

### What you must know about React

- Components, applications state, organizing and managing your UI code and other core features of React

### How to install and get set up with React

- There are two ways
  - With a tool called Create React App; it automatically sets up a build system, and creates the files and folders you need to get started with React.

### Create a React Element

- React is only a library for creating and updating HTML elements in your UI.
- React provides the createElement function to create and return elements
- createElement has THREE arguments

  - 1. Type of element; usually a string which represents an HTML element or a tag (e.g. h1 element)
  - 2. Object containing any attributes and value you want to give the element; can pass an empty object, or the value null.
  - 3. Contents or children of the element
       e.g. <h1> It could also be more elements created by React.createElement </h1>

- React does not create actual DOM; it is an object representation of a DOM node
- It has several properties like key, props, and ref
  - props는 property의 약자로, 부모에게 받아온 데이터를 뜻 함

### Render an Element

- React uses a faster, easier, and friendlier way to create elements with a special syntax called JSX
- Mark-up-like syntax to create React elements
- We need the Babel compiler to transpile React elements with JSX.
