---
layout: default
title: "Software Engineering: SpringBoot & Vue.js"
date: 2022-01-18 13:50:00
categories: Software Engineering
---

### What is SpringBoot?

- It is a framework that allows spring framework-based projects to be developed immediately without difficult settings or Web Application Server settings.

- 스프링부트란? 프렌차이즈의 레시피들을 생각하면 된다
- 자바 프로그램을 만들기 위해서 어떠한 노하우들을 이용하는 것
- 스프링 부트를 이용하여 보다 쉽고 빠르게 자바 프로그램을 만들 수 있다

**웹 서비스의 동작원리**

클라이언트(서비스를 사용하는 프로그램 및 컴퓨터)와 서버(서비스를 제공하는 프로그램 및 컴퓨터)의 요청과 응답

**뷰 템플릿과 MVC 패턴**

View Templates: 화면출력(Presentation)
Controller: 처리과정(logic)
Model: 데이터(data)

**MVC의 역할과 실행흐름**

Controller : 클라이언트의 요청을 받음

package com.example.firstproject.controller;

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class FirstController {

	@GetMapping("/hi") // Request
	public String niceToMeetYou(Model model) {
		model.addAttribute("username", "이혁주");
		return "greetings";
	}
}
```

View: 최종 페이지를 만들어 주고

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="ISO-8859-1" />
    <title>Insert title here</title>
  </head>
  <body>
    <h1>{{username}}님, 반갑습니다!</h1>
  </body>
</html>
```

Model: 데이터를 뷰에게 전달 함

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class FirstController {

	@GetMapping("/hi")
	public String niceToMeetYou(Model model) {
		model.addAttribute("username", "이혁주"); // 데이터 등록 -> 뷰페이지 에서 사용 가능
		return "greetings"; // temlplates/greeting.mustache -> 브라우저로 전송
	}
}
```

**Few Spring project dependencies (tools)**

1. Spring Boot DevTools
   When the code for the contents transmitted to the browser is changed, the application is <b>automatically restarted to update the browser</b>'.

   For example, if you add a new field to an entity or add a new entity, you can view updated information from the h2 console <b>without restarting the project</b>.

2. Lombok
   It helps to reduce the amount of 'infrastructural code'. You don't need to write constructors, getters, setters, and even builders anymore. All you have to do is to put the proper <b>annotations</b> and the plugin will generate everything for you.

3. Spring Data JPA
   Interface that manages relational data; Access database and allows a developer get wanted information
   <u>Map RDB to an object and use it</u>

```Java
package com.example.demo.model;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "courses")
public class Course {

	@Id
	@GeneratedValue(strategy = GenerationType.AUTO) // Id is automatically generated
	private long id; // Id of a record in the DB

	@Column(name = "code")
	private String code;

	@Column(name = "title")
	private String title;

	public Course() {

	}

	public Course(String code, String title) {
		this.code = code;
		this.title = title;
	}

	public long getId() {
		return id;
	}

	public void setId(long id) {
		this.id = id;
	}

	public String getCode() {
		return code;
	}

	public void setCode(String code) {
		this.code = code;
	}

	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}

}
.....

Course c1 = new Course("CSIS2175", "ADVANCED INTEGRATED SOFTWARE DEVELOPMENT"
```

4. H2 Database
   It is a relational database management system written in Java. It can be embedded in Java applications or run in client-server mode.

5. Spring Web
   The spring-web dependency contains common web specific utilities for both Servlet and Portlet environments

6. Rest Respositories HAL Explorer

   - Spring Data Rest Respository는 Spring Data 프로젝트의 서브 프로젝트로 Repository의 설정만으로 REST API 서버를 구성해주는 신박한 기능입니다. 사용자는 Entity 클래스와 Repository 인터페이스만 작성하면 나머지 CRUD 작업은 모두 알아서 RESTful하게 생성됩니다.

   - SpringData REST의 주요 기능은 Data Repository로부터 Resource를 추출하는 것으로 핵심은 Repository 인터페이스입니다. 예를 들어 OrderRepository와 같은 Repository인터페이스가 있을 경우 소문자의 복수형 resource를 뽑아내어 /orders 를 만듭니다. 그리고 /orders/{id} 하위에 각 item을 관리할 수 있는 resource를 추출해 냅니다.
