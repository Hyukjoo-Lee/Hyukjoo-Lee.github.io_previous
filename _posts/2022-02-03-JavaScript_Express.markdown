---
layout: default
title: "JavaScript: npm Express & ejs"
date: 2022-02-03 21:50:00
categories: JavaScript
---

### Express framework

- Express provides a method that specifies a function called for a specific HTTP verb (GET, POST, SET, etc.).

- Specifies the URL pattern ("Route") and the "View" engine to be used, the template file location, and how to specify the template to be used to render the response.

https://www.npmjs.com/package/express

### EJS framework

- EJS is an module for Embedded JavaScript template, a simple template language that can create 'HTML markups' for JavaScript.

- (If you're a java developer, you can say you play the same role as a familiar 'JSP')

- Logic and data necessary in-between HTML may be added using a tag in the form of <%...%>.

- In particular, it is best to send server data into html directly through the for-loop or if statement.

https://www.npmjs.com/package/ejs

### Simple JS Source code (BMI Calculator)

```javascript
// Import modules
const express = require("express");

const app = express();
const port = 3000;

app.use(express.static("public"));
app.use(express.urlencoded({ extended: true }));

// Import npm ejs(Embedded JavaScript templating)
// which allows you to create html markup
app.engine("html", require("ejs").renderFile);
// Syntax : views, __dirname + "/" + <folderName>
app.set("views", __dirname + "/" + "webpage");

// Render basic html file
app.get("/", function (req, res) {
  res.render("bmi.html");
});

// Get request and respond rending a new page with html values
app.post("/", function (req, res) {
  let age = req.body.age;
  let weight = req.body.weight;
  let height = req.body.height;

  // TO TEST
  // console.log(age + " " + weight + " " + height);

  // Calculate BMI
  let bmi = (weight / [height * height]) * 10000;

  // One decimal point
  let result = bmi.toFixed(1);

  // Render new page with html markups
  res.render("./result.html", {
    age: age,
    weight: weight,
    height: height,
    result: result,
  });
});

app.listen(port, function () {
  console.log("Listening port " + port);
});
```
