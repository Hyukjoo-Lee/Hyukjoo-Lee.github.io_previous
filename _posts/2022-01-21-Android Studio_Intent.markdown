---
layout: default
title: "Android Studio: Explicit Intent & Implicit Intent View binding"
date: 2022-01-21 17:00:00
categories: Android Studio
---

### View Binding

1.  What is View Binding

    1-1. Before

    - We needed to assign variables such as TextView nameView, phoneView, and addressView ... etc

    - We also needed to reference views in xml and then do operations by using findViewById

    - Time consuming and inefficient

    - View Binding is an alternative

    1-2. Changes

    - 3.5 version : we used findViewById

    - 3.6 version : view binding

    - 4.1 version : Kotlin Synthetic; can use id as an variable; only Kotlin supports and NullPointException occurs frequently --> deprecated

    - Current version: Java and Kotlin use view binding only

    1-3. Difference with findViewById

    - View Binding automatically create a class, so we do not need to write id and set types

    - findViewById

      - Null error can occur when a developer use invalid id

      - Cast excepton can occur when a developer made a mistake e.g. textView type <-> imageView type

      - Speed is slower than

2.  How to use

    2-1. add gradle

    - Version should be higher than 3.6

    - Higher than 4.0

    ```java
    android {

         ...


         buildFeatures {


             viewBinding = true


         }

    }

    - 3.6 ~ 4.0

    android {

         ...


         viewBinding {


             enabled true


         }

    }
    ```

    2-2. activity

    #### Java

    ```java
    public class MainActivity extends AppCompatActivity {

    private ActivityMainBinding binding;

    @Override

    protected void onCreate(Bundle savedInstanceState) {

         super.onCreate(savedInstanceState);


         binding = ActivityMainBinding.inflate(getLayoutInflater()); // 1


         setContentView(binding.getRoot()); // 2

    }

    private void updateUI(UserProfile userProfile){

         binding.name.setText("Hyukjoo Lee"); // 3


         binding.phone.setText("000-000-0000");


         binding.address.setText("Burnaby, BC");

    }
    ```

}

1. ActivityMainBinding.inflate(getLayoutInflater());
   inflate --> instantiate view in xml

2. Before : R.layout.activity_main
   After : binding.getRoot()
   Pass root view we created

3. access properties in the object

rule : ActivityXXXBinding

#### Kotlin

```java
private lateinit var binding: ActivityMainBinding

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {


        super.onCreate(savedInstanceState)


        binding = ActivityMainBinding.inflate(layoutInflater)


        setContentView(binding.root)



        binding.textView.text = "Hi"
    }

}
```

### In school class: Android Mobile App II

```java
in build.gradle(Module:) script

    android {

         ...


         buildFeatures {


             viewBinding = true


         }

    }
```

- Build Menu -> Clean Project -> Rebuild Project

this is to ensure binding class is generated

- Import binding class and do some modification

```java
// Source Code
package com.example.converter;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;

import android.widget.EditText;
import android.widget.TextView;

import com.example.converter.databinding.ActivityMainBinding;

import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    private ActivityMainBinding binding; // 1

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // 2
        binding = ActivityMainBinding.inflate(getLayoutInflater());
        View view = binding.getRoot();
        setContentView(view);
    }

    public void convertCurrency(View view) {

        // Traditional ways
//        EditText dollarText = findViewById(R.id.dollarText);
//        TextView textView = findViewById(R.id.textView);

        // dollarText.getText()... => binding.dollarText...
        if(!binding.dollarText.getText().toString().equals("")){
            float dollarValue = Float.parseFloat(binding.dollarText.getText().toString());
            float euroValue = dollarValue * 0.85F ;
            binding.textView.setText(String.format(Locale.ENGLISH, "%.2f", euroValue));
        }
        else {
            binding.textView.setText("No Value");
        }
    }
}
```
