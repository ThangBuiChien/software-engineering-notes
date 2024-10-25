## Run the GUI

```
cd /path/to/apache-jmeter-x.x/bin
```

```
jmeter.bat
```

## Configure a Basic Concurrency Test

Create a Test Plan:

1. Go to the top-left menu: File > New.
   Right-click on the Test Plan in the left panel and select: Add > Threads (Users) > Thread Group.
   Configure Thread Group:

2. In the Thread Group, set the following parameters:
   - Number of Threads (Users): This determines the number of concurrent users.
   - Ramp-Up Period (in seconds): This is how long JMeter will take to start all threads (users). Set 0 for immediate start.
   - Loop Count: Set it to a number like 1 to simulate each user running the test once or to a higher number for repeated tests.
3. Add HTTP Request Sampler:

   - Right-click on the Thread Group and select: Add > Sampler > HTTP Request.
   - In the HTTP Request sampler, configure the details of the request:
   - To add json => Set the Request Headers (Content-Type)
     - Right-click on the HTTP Request sampler => Add > Config Element > HTTP Header Manager
     - In the HTTP Header Manager =>
       - Name: Content-Type
       - Value: application/json

4. Add View Results Tree Listener:

   - Right-click on the Thread Group and select: Add > Listener > View Results Tree.
   - This will show the results of your test in the GUI.

5. Run the Test:

   - Click the green start button (play icon) at the top of the screen to run the test. JMeter will simulate the configured number of users sending requests concurrently.

6. Analyze Results:

   - After the test finishes, go to the View Results Tree listener to see the individual request responses.
   - You can also use other listeners like Summary Report or Aggregate Report to analyze the performance (e.g., average response time, error rates).
