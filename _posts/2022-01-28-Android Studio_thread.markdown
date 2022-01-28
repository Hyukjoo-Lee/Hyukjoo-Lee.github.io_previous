---
layout: default
title: "Android Studio: Thread Demo"
date: 2022-01-28 12:50:00
categories: Android Studio
---

### Process VS Thread

<em>Process</em>

- Executing program on the memory through OS.
- Generally, one process is operating with one thread.

<em>Thread</em>

- A thread of execution in a program.
- Multi-threads programming &rarr; more than two threads on the single process
- Every thread has a priority. When code running in some thread creates a new Thread object.

### How to create a new thread of execution

- One is to declare a class to be a subclass of Thread.

```java
class PrimeThread extends Thread {
    long minPrime;
    // Constructor
    PrimeThread(long minPrime) {
        this.minPrime = minPrime;
    };

    public void run() {
        // Compute primes larger than minPrime

        // Then create a thread and start it running
        PrimeThread p = new PrimeThread(143);
        p.start();
    }

}
```

- The other way to create a thread is to declare a class that implements the Runnable interface.

```java
    class PrimeRun implements Runnable {

        long minPrime;
        PrimeRun(long minPrime) {
            this.minPrime = minPrime;
        }

        @Override
        public void run() {
          // Compute primes larger than minPrime
            PrimeRun p = new PrimeRun(143);
            new Thread(p).start();
        }
    }
```

### Simple and sample example to introduction of thread

```java

public class MainActivity extends AppCompatActivity {

    private ActivityMainBinding binding;
    // 3
    // Use the created Looper instead of the default one
    // A Handler allows you to send and process Message
    // and Runnable objects associated with a thread's MessageQueue.

    // Looper: Made by thread and do some repetitive operations in a loop
    Handler handler = new Handler(Looper.getMainLooper()) {
        @Override
        public void handleMessage(@NonNull Message msg) {
            Bundle bundle = msg.getData();
            // Get message (currentDataandtime)
            String string = bundle.getString("myKey");
            // Set text
            binding.myTextView.setText(string);
        }
    };

    // 1
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        View view = binding.getRoot();
        setContentView(view);
    }

    // 2
    public void buttonClick(View view) {
        // New thread will be created, and main thread is deleted
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                // Get currentTime from the System
                long endTime = System.currentTimeMillis() + 10 * 1000;

                // Pause 10 seconds
                while (System.currentTimeMillis() < endTime) {
                    synchronized (this) {
                        try {
                            wait(endTime - System.currentTimeMillis());
                        } catch (Exception e) {

                        }
                    }
                }
                // Returns a new Message from the global message pool
                Message msg = handler.obtainMessage();
                Bundle bundle = new Bundle();
                // Set Data format
                SimpleDateFormat simpleDataFormat = new SimpleDateFormat("yyyy.MM.dd G 'at' HH:mm: ss z");
                // To update the date and time from the system
                String currentDataandtime = simpleDataFormat.format(new Date());
                // Reference AND put String data into 'myKey' key
                bundle.putString("myKey", currentDataandtime);
//                bundle.putString("myKey", "Thread Completed");
                // Set a new message data passing bundle
                msg.setData(bundle);
                // Send message to Handler to process the message
                handler.sendMessage(msg);
            }
        };
        // Start thread
        Thread myThread = new Thread(runnable);
        myThread.start();
    }
}
```
