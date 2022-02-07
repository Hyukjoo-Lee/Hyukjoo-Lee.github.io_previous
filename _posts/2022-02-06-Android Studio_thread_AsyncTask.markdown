---
layout: default
title: "Android Sudio: Thread Demo(2)_AsyncTask"
date: 2022-02-06 17:00:00
categories: Android Studio
---

### The main thread

- Independent path of execution in a running program
- Code is executed line by line
- App runs on Java Thread called 'main' or 'UI thread'
- Draws UI ont the screen
- Responds to user actions by handling UI events

### ANR (Application Not Responding)

- An error which occurs when an UI thread blocks for too long time.

- What is a long running task?

  - Network operation
  - Long calculations
  - Downloading / Uploading files
  - Processing images
  - Loading data

- Worker Thread (UI thread) is a solution
  - All you can do inside Worker Thread, is functionality to fetch the data
  - Once you get the data, you can update UI then
  - It makes application running smoothly

### AsyncTask

- Use AsyncTask to implement basic background tasks

- The reason we have created an AsyncTask class is that provides you very good framework to put your data in your background, and then update UI very smoothly and efficiently

<em>Methods</em>

![AsyncTask image](https://github.com/Hyukjoo-Lee/Hyukjoo-Lee.github.io/blob/main/_posts/images/thread.png?raw=true "AsyncTask helper methods")

1. onPreExecute() - Runs on the main thread, and sets up the task
2. doInBackground() - runs on a background thread, all the work to happen in the background
3. onProgressUpdate() - Runs on the main thread, it receives calls from publishProgess() from background thread
4. onPostExecute() - runs on main thread when work donne, process results and publish results to the UI

<em>AsyncTask class definition</em>

```java
priate class MyAsyncTask entends AsyncTask<String, Integer, Bitmap> {...}

@Params
String - could be query, URL for filenam
Integer - percentage completed, steps done
Bitmap - an image to be displayed


protected void onPreExecute() {
// display a progress bar
// show a toast
}

protected Bitmap doInBackground(String... query){
// Get the bitmap
// Ruturn type of your doInBackground will be always the same as your result param
return bitmap
}

protected void onProgressUpdate(Integer... progress) {
setProgessPercent(progress[0]);
}

protected void onPostExecute(Bitmap result) {
    //
// Do something with the bitmap
}

```

### Start background work

```java
public void loadImage(View view) {
    String query = EditText.getText().toString();
    new MyAsyncTask(query).execute();
}
```

### AsyncTask Loader?

- Loaders are designed to keep config data changes

- Can monitor changes in data source and deliver new data

- Callbacks implemented in Activity

### What is a LoaderManager

- Manages loader functions via callbacks
- Can manage multiple loaders e.g. loader for db data, AsyncTask data, for internet data...etc

### Steps for AsyncTaskLoader subclass

1. Subclass AsyncTaskLoader
2. Implement constructor
3. loadInBackground()
4. onStartLoading()

### Source code

```java
package com.example.simpleasynctask;

// This class will perform a simple background task: It sleeps for a random amount of time
// In real app, the background task can perform all sorts of work,
// from querying a db to connecting to internet.. etc

// 1. Methods : onPreExecute(), doInBackground(), onProgressUpdate, and OnPostExecute
// 2. Params : The data type of the param sent to the task upon executing the doInBackground()
// 3. Result : The data type of the result delivered by the onPostExecute() override method

// e.g. AsyncTask
// Params: A String as a param in doInBackground() to use in a query
// Integer for onProgressUpdate(), to represent the percentage of job complete
// A Bitmap for the result in onPostExecute(), indicating the query result

import android.app.ProgressDialog;
import android.content.Context;
import android.os.AsyncTask;
import android.widget.TextView;

import java.lang.ref.WeakReference;
import java.util.Random;

public class SimpleAsyncTask extends AsyncTask <Void, Integer, String>{

    Context ctx;
    ProgressDialog pd;

// Define a variable of the type WeekReference<TextView>
// What is WeakReference? - The weak reference prevents the memory leak by allowing the object held
// by that reference to be garbage collected if necessary.
private WeakReference<TextView> mTextView;

    // Constructor
    // Needs to update the TextView in the Activity once it has completed sleeping (in the onPostExecute())
    SimpleAsyncTask(TextView tv, Context ct) {
        mTextView = new WeakReference<>(tv);
        ctx = ct;

    }

    @Override
    protected String doInBackground(Void... voids) {

        // Generate a random number between 0 and 10
        Random r = new Random();
        int n = r.nextInt(11);

        // Make the task take long enough that we have
        // time to rotate the phone while it is running
        int s = n * 200;

        // Sleep for the random amount of time
        try {
            Thread.sleep(s);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Return a String result
        return "Awake at last after sleeping for " + s + " milliseconds!";
    }

    // onProgressUpdate() which allows you to update the UI while the AsyncTask is running
    // Update the UI with the current sleep time


    @Override
    protected void onProgressUpdate(Integer... values) {
        super.onProgressUpdate(values);
    }

    @Override
    protected void onPostExecute(String result) {
        mTextView.get().setText(result);
    }
}



```

#### Reference:

https://developer.android.com/topic/performance/vitals/anr?hl=ko
