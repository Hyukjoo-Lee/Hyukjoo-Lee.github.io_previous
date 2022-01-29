---
layout: default
title: "Software Engineering: MVC_Controller (Source code)"
date: 2022-01-28 20:00:00
categories: Software Engineering
---

**Controller Source code**

```java
package com.example.demo.controller;

@CrossOrigin(origins = "http://localhost:8081")
@RestController
@RequestMapping("/api")
public class CourseController {

	// CourseRepository Interface
	// After these two lines, you can access the database
	@Autowired
	// Use this variable to add,delete,search and modify database
	CourseRepository courseRepository;

	@GetMapping("/courses/{id}") // PathVariable
	public ResponseEntity<Course> getCourseById(@PathVariable("id") long id) {

		// findById - the entity with the given id or Optional#empty() if none found
		Optional<Course> courseData = courseRepository.findById(id);

		// If any data is present, HttpStatus.OK is returned -> and JSON file is shown
		if (courseData.isPresent()) {
			return new ResponseEntity<>(courseData.get(), HttpStatus.OK);
		} else {
			return new ResponseEntity<>(HttpStatus.NOT_FOUND);
		}
	}

	// API endPoint, by convention, we use a noun(not getCourse.. etc)
	@GetMapping("/courses")
	public ResponseEntity<List<Course>> getAllCourses(@RequestParam(required = false) String title) {

		try {
			List<Course> courses = new ArrayList<Course>();
			if (title == null) {
				courseRepository.findAll().forEach(courses::add);
//				List<Course> results = courseRepository.findAll();
//				for(Course c : results) {
//					courses.add(c);
//				}
			} else {
				// Exact match of title
				courseRepository.findByTitle(title).forEach(courses::add);
			}

			return new ResponseEntity<>(courses, HttpStatus.OK);

		} catch (Exception e) {
			return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
		}

	}

}

```
