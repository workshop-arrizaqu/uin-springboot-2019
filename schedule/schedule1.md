# Schedule

* spesific time

```java
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;

public class ExamSchedule2 {
    public static void main(String[] args) throws ParseException {
        //the Date and time at which you want to execute
        DateFormat dateFormatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        Date date = dateFormatter.parse("2020-02-08 12:24:00");

        //Now create the time and schedule it
        Timer timer = new Timer();

        //Use this if you want to execute it once
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println("working guys..");
            }
        }, date);

        //Use this if you want to execute it repeatedly
        //int period = 10000;//10secs
        //timer.schedule(new MyTimeTask(), date, period );
    }
}
```

* in periodic time

```java
public class ExamSchedule {

    public static void main(String[] args) {
        runningTask();
    }

    private static final ScheduledExecutorService scheduler =
            Executors.newScheduledThreadPool(1);

    public static void runningTask(){

        Runnable beeper = () -> System.out.println("beep");
        RunnableScheduledFuture<?> beeperHandle =
               (RunnableScheduledFuture<?>) scheduler.scheduleAtFixedRate(beeper, 0, 60, SECONDS);
        beeperHandle.cancel(false);
        Runnable canceller = () -> beeperHandle.cancel(false);
        scheduler.schedule(canceller, 61, SECONDS);
    }

}

```



