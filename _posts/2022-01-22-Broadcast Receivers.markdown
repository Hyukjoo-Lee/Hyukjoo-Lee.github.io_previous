---
layout: default
title: "Android Studio: Broadcast Receivers"
date: 2022-01-23 20:00:00
categories: Android Studio
---

### What is broadcast?

- When you do some actions like turning off your phone and then turn on again, these actions are sent through Intent object
- Then, broadcast receiver receives the actions and send back to the app
- Use Implicit intents to send broadcasts or start activities
- Listens for incoming intents send by sendBroadcast()
- Intents can be sent
  1. By the system, when an event occurs that might change the behavioUr of an app
  2. By another app, including your own

**System broadcast**

- Automatically delivered when certain events occur
- After the system completes a boot
  android.intent.action.BOOT_COMPLETED
- When the wifi state changes
  android.net.wifi.WIFI_STATE_CHANGED

**Custom broadcasts**

- Deliver any custom intent as a broadcast
  1. sendBroadcast() method - asynchronous(one)
  - Can be at the same time (All receivers of the broadcast are run in an undefined order)
  - To send a normal broadcast, create a broadcast intent and pass it to sendBroadcast(Intent)
  2. sendOrderedBroadcast() - synchronously
  - Delivered to one receiver at one time
  - Can be controlled by android:priority attribute
  - Same priority &rarr; is run ramdomly
  3. Localbroadcast
  - Create a broadcast intent and pass it to LocalBroadcastManager.sendBroadcast

**Creating a broadcast receiver**

<b>Register your receiver for system broadcasts</b>

- Each system broadcast is wrapped in an Intent object: Contains event details like android.intent.action.battery_low, and also other data about the event in its extra field, for example a boolean extra indicating whether the battery is low or not

<b>Static or Dynamic receiver</b>

1.  Static - Use the <receiver> element in your AndroidManifest.xml file (cannot use static receivers starting from API level 26 and higher)

2.  Dynamic - use the app context or activity context
    1. Delete the entire <receiver> element)
    2. In MainActivity.java, create a CustomReceiver object as a member variable and initialize it
    ```java
    // In MainActivity.java
    // Create CustomReceiver object
    private CustomReceiver mReceiver = new CustomReceiver();
    ```

<b>Create an intent filter with Intent actions</b>

```java
// In MainActivity.java, at the end of onCreate() method
IntentFilter filter = new IntentFilter();

// Add actions
filter.addAction(Intent.ACTION_POWER_DISCONNECTED);
filter.addAction(Intent.ACTION_POWER_CONNECTED);
```

<b>Register and unregister the receiver</b>

```java
// In MainActivity.java, at the end of onCreate() method
....
// Register the receiver using the activity context
this.registerReceiver(mReceiver, filter);
```

```java
// In MainActivity.java
@Override
   protected void onDestroy() {
       //To save system resources and avoid leaks, dynamic receivers must be unregistered
       this.unregisterReceiver(mReceiver);
       super.onDestroy();
   }
```

<b>Implement onReceive() in your BroadcastReceiver</b>

```java
// In CustomReceiver.java
@Override
public void onReceive(Context context, Intent intent) {
    // Get intent's action and store it to a string
   String intentAction = intent.getAction();
   // Create a switch statement with the intentAction string
   if (intentAction != null) {
   String toastMessage = "unknown intent action";
   switch (intentAction){
       case Intent.ACTION_POWER_CONNECTED:
           toastMessage = "Power connected!";
           break;
       case Intent.ACTION_POWER_DISCONNECTED:
           toastMessage = "Power disconnected!";
           break;
   }

  //Display the toast.
  Toast.makeText(context, toastMessage, Toast.LENGTH_SHORT).show();
}
}

```

**Send and receive a custom broadcast**

<b>Define your custom broadcast action string</b>

- Create a constant member variable in both your MainActivity and your CustomReceiver class

```java
private static final String ACTION_CUSTOM_BROADCAST =
BuildConfig.APPLICATION_ID + ".ACTION_CUSTOM_BROADCAST";
```

<b>Add a send custom broadcast</b>

android:onClick="sendCustomBroadcast"

<b> Extract the string resource</b>

- Create ‘sendCustomBroadcast(View)' in MainActivity.java

- Use LocalBroadcastManager to manage the broadcast

```java
// In MainActivity, inside sendCustomBroadcast() method

// Create a new Intent, with your custom action string as the argument
Intent customBroadcastIntent = new Intent(ACTION_CUSTOM_BROADCAST);
// Send the broadcast using the LocalBroadcastManager class
LocalBroadcastManager.getInstance(this).sendBroadcast (customBroadcastIntent);
```

<b>Register and unregister your custom broadcast</b>

- Register the action in onCreate() and unregister it in onDestroy()

```java
// In MainActivity.java, inside onCreate() method

LocalBroadcastManage.getInstance(this).registerReceiver(mReceiver, new IntentFilter(ACTION_CUSTOM_BROADCAST));
```

- Unregister your receiver from the LocalBroadcastManager

```java
// In MainActivity.java, inside the onDestroy() method
LocalBroadcastManager.getInstance(this).unregisterReceiver(mReceiver);
```

<b>Respond to the custom broadcast</b>

In CustomReceiver.java, inside the onReceive() method, add another case statement in the switch block

```java
case ACTION_CUSTOM_BROADCAST:
   toastMessage = "Custom Broadcast Received";
   break;
```

**Summary**

- Broadcast receivers are fundamental components of an Android app.
- Broadcast receivers can receive broadcasts sent by the system or by apps.
- The Intent used in the broadcast mechanism is completely different from intents used to start activities.
- To process the incoming Intent associated with a broadcast, you subclass the BroadcastReceiver class and implement onReceive().
- You can register a broadcast receiver in the Android manifest file or programmatically.
- Local broadcasts are private to your app. To register and send local broadcasts, use LocalBroadcastManager. Local broadcasts don't involve interprocess communication, which makes them efficient. Using local broadcasts can also protect your app against some security issues, because data stays inside your app.
- To create unique Intent action names for broadcasts, a common practice is to prepend the action name with your package name.
- If your app targets API level 26 or higher, you can use dynamic receivers to receive all broadcasts.

```java
Intent intent = new Intent();
// addFlags
// intent.addFlags(Intent.FLAG_INCLUDE_STOPPED_PACKAGES);
intent.setAction("com.example.Broadcast");
intent.putExtra("MyData", 1000);
sendBroadcast(intent);
```

### Questions

- <em>Question 1: What is a system broadcast?</em>

  A. A message that your app sends and receives when an event of interest occurs in the app.
  B. A message that is sent from an app to a different component of the same app.
  C. A message that the Android system sends when a system event occurs.
  D. A message that the Android system receives when an event of interest occurs in your app.

- <em>Question 2: Which pair of methods do you use to register and unregister your broadcast receiver dynamically?</em>

  A. registerBroadcast() and unRegisterBroadcast().
  B. registerComponentCallbacks() and unRegisterComponentCallbacks().
  C. registerBroadcastReceiver() and 4. unRegisterBroadcastReceiver().
  D. registerReceiver() and unRegisterReceiver().

- <em>Question 3: Which of the following are true?</em>

  A. Broadcast receivers can't see or capture the intents used to start an activity.
  B. Using a broadcast intent, you can't find or start an activity.
  C. You can use a broadcast intent to start an activity.
  D. You can receive the intent used to start activity in your broadcast receiver.

- <em>Question 4
  Which class is used to mitigate the security risks of broadcast receivers when the broadcasts are not cross-application (that is, when broadcasts are sent and received by the same app)?</em>

  A. SecureBroadcast
  B. LocalBroadcastManager
  C. OrderedBroadcast
  D. SecureBroadcastManager

  **Answers**

  1. C
  2. D
  3. D
  4. B

<em>Reference</em>

[broadcast-receivers][broadcast-receivers]

[broadcast-receivers]: https://developer.android.com/codelabs/android-training-broadcast-receivers?index=..%2F..%2Fandroid-training#5
