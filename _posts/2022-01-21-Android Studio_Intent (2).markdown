---
layout: default
title: "Android Studio: Explicit Intent & Implicit Intent View binding (2)"
date: 2022-01-21 17:00:00
categories: Android Studio
---

### What is intent?

- Intent allows us transfer data from sender activity to receiver activity

- It is used to run an activity in another activity

- After creating an Intent, we store data which we wish to send into the Intent

- So, It is possible to execute the desired components in the activity; there are two methods

### Explicit Intent &larr;&rarr; Implicit Intent

<h3 style="color:red">Explicit Intent</h3>

- 실행하고자 하는 컴포넌트가 '명확' 할 때 사용
- e.g. The operation intention itself are

  1. Sending a <em>' Input value '</em> from MainActivity to SecondActivity.
  2. Returning a <em>' Input value '</em> form SecondActivity to MainAcitivy.

**Source Code**

```java
// In MainActivity.java
    public void sendText(View view) {

        Intent i = new Intent(this, SecondActivity.class);
        // Want to send this specific string to SecondActivity
        String myString = binding.editText1.getText().toString();
        // Add the string to the intent
        i.putExtra("qString", myString);
        // Launch SecondActivity
        startForResult.launch(i);
    }
```

```java
// In SecondActivity.java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

    ...
        // Return the activity started this activity.
        // Get data from the intent
        Bundle extra = getIntent().getExtras();
        // If there is no data from the intent, escape onCreate
        if(extra == null) {
            return;
        }

        // Retrieve extended string related with the key "qString"
        String qString = extra.getString("qString");
        binding.textView2.setText(qString);
    }
```

```java
    ...
    // Return a String
    public void returnText(View view) {
        finish();
    }

    @Override
    public void finish() {

        Intent data = new Intent();
        String returnString = binding.editText2.getText().toString();
        data.putExtra("returnData", returnString);
        // Set the result that this activity will return to its caller.
        setResult(RESULT_OK, data);
        super.finish();
    }
```

```java
    // In MainActivity.java

    // ActivityResultLauncher: a launcher for a previously-prepared call to
    // start the process of executing an ActivityResultContracts & ActivityResultCallback
    ActivityResultLauncher<Intent> startForResult = registerForActivityResult(
            new ActivityResultContracts.StartActivityForResult(),
            new ActivityResultCallback<ActivityResult>() {
                @Override
                public void onActivityResult(ActivityResult result) {
                    if(result.getResultCode() == Activity.RESULT_OK) {
                        // Get a returned string
                        Intent data = result.getData();
                        String returnString = data.getExtras().getString("returnData");
                        binding.textView1.setText(returnString);
                    }
                }
            });
```

<h3 style="color:red">Implicit Intent</h3>

- You can execute the desired component with any intention.
- Intents that do not specify the name of the component, but only contains a list of the features of the component to be called
- Android system retrieves intent filters to be matched with the feature
- e.g. If you want to display a location on a map, you can ask another app with that feature.

**Example app**
<img src="./images/android_ImplicitIntent.png">

**Source Code**

```java
    public void showWebPage(View view) {

        Intent intent = new Intent(Intent.ACTION_VIEW,
                Uri.parse("http://www.msn.com"));

        startActivity(intent);
    }
```

- Intent solution process finds two activities matched with implicit intent using the intent filter

```java
// Another web view app
    private void handleIntent() {
        // Return the intent that started this activity
        Intent intent = getIntent();
        // Retrieve data this intent is operating on.
        Uri data = intent.getData();
        URL url = null;

        try {
            // Get scheme, host, and decoded-path
            // In Manifest file, <data android:scheme="https" android:host="www.msn.com" />
            url = new URL(data.getScheme(), data.getHost(), data.getPath());
        } catch (Exception e) {
            e.printStackTrace();
        }
        // Load url
        binding.webView1.loadUrl(url.toString());
    }


    // In Manifest file
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
            // Set actions
            <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.BROWSABLE" />
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:scheme="https" android:host="www.msn.com" />
            </intent-filter>
        </activity>

```
