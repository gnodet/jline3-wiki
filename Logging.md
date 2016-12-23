JLine uses the [`java.util.logging`](https://docs.oracle.com/javase/8/docs/api/java/util/logging/package-summary.html) framework for logging.

It uses a single logger named `org.jline` and all access to this logger is done through the [`org.jline.utils.Log`](https://github.com/jline/jline3/blob/master/terminal/src/main/java/org/jline/utils/Log.java) class.

The logging configuration can be done by any usual mechanism, JLine does not do any configuration at all for the logging, so bridges such as the [Log4j JDK Logging Adapter](https://logging.apache.org/log4j/2.0/log4j-jul/index.html) or [SLF4J JUL Bridge](http://www.slf4j.org/legacy.html#jul-to-slf4j) can be freely used to redirect JLine log to the backend of your choice.
