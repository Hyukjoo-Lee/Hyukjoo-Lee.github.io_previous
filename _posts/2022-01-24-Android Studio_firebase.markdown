---
layout: default
title: "Android Studio: Firebase environment setting"
date: 2022-01-24 23:00:00
categories: Android Studio
---

### What is firebase?

- Mobile, and Web development platform

- It makes possible to develop a serverless applications

### Main functions and features

1. Authentication system

- Authentication is responsible for logging in within Firebase

- Support such as security process, password search, ID search, password change, email authentication...etc

2. Database based on NoSQL

- A fast and simple NoSQL-based database in the form of a document

- Supports Real Time Stream Protocol (RTSP) databases (Send data in real time)

3. Provides console

- Server administrator page

- Support for access security, MySQL (database), Node.JS server, Spring server ...etc

4. Providde Analytics

- Statistical information on how users use the app

- e.g. tracking error statistics, user retention rate, customer app update status, the amount of time users stayed on a specific page, events, etc.

### How to set firebase in Android Studio

1. Create a project in firebase web page, and add jason file to the app

2. in build.gradle(Project), add google() repository if you do not have & add dependencies classpath 'com.google.gms:google-services:4.3.10'

```java
// build.gradle (project)
buildscript {
    repositories {

        google()
        ...
    }
    dependencies {
        classpath "com.android.tools.build:gradle:7.0.3"
        // Here
        classpath 'com.google.gms:google-services:4.3.10'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
```

3. in another build.gradle(Module), add google-servies plugin & add up-to-date dependencies (Now: 1/24/2022)

```java
plugins {
    id 'com.android.application'
    id 'com.google.gms.google-services'
}
```

```java
dependencies {

    implementation 'androidx.appcompat:appcompat:1.4.1'
    implementation 'com.google.android.material:material:1.5.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.3'
    // From here
    implementation platform('com.google.firebase:firebase-bom:29.0.4')
    implementation 'com.google.firebase:firebase-analytics'
    implementation 'com.google.firebase:firebase-storage'
    implementation 'com.google.firebase:firebase-database:20.0.3'
    // end
    testImplementation 'junit:junit:4.+'
    androidTestImplementation 'androidx.test.ext:junit:1.1.3'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
}
```

4. Test Real Time Stream Protocol (RTSP) databases

- Create a class (database name)

```java
public class RegisterActivity extends AppCompatActivity {

    private ActivityRegisterBinding binding;
    // Add database reference
    DatabaseReference reff;
    // Assign the Users class
    Users users;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityRegisterBinding.inflate(getLayoutInflater());
        View view = binding.getRoot();
        setContentView(view);

        // Create an object
        users = new Users();
        // child("") : A new DatabaseReference to the given path
        reff = FirebaseDatabase.getInstance().getReference().child("Users");
        binding.btnRegister.setOnClickListener(v -> {
            // Set Email and password input
            users.setEmail(binding.inputEmailRego.getText().toString().trim());
            users.setPassword(binding.inputPasswordRego.getText().toString());

            // Push the users object
            reff.push().setValue(users);
            Toast.makeText(RegisterActivity.this, "data is inserted successfully.", Toast.LENGTH_SHORT).show();
        });

        binding.txtForLogin.setOnClickListener(v -> startActivity(new Intent(RegisterActivity.this, LoginActivity.class)));
    }
}
```

```java
// This is a database class ('Users' is a database name)
public class Users {
    private String Email;
    private String Password;

    public Users() {

    }

    public String getEmail() {
        return Email;
    }

    public void setEmail(String email) {
        Email = email;
    }

    public String getPassword() {
        return Password;
    }

    public void setPassword(String password) {
        Password = password;
    }

}
```
