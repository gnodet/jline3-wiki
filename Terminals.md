JLine provides a terminal abstraction using the [`Terminal`](https://github.com/jline/jline3/blob/master/terminal/src/main/java/org/jline/terminal/Terminal.java) interface which provides the following features:
 * Signals support
 * Input stream, output stream, non blocking reader, writer
 * Tty size and parameters
 * Infocmp capabilities

There are two different types of terminals
 * System terminals that handle an OS terminal window
 * Virtual terminals to support incoming connections

## System terminals

There is only a single system terminal for a given JVM, the one that has been used to launch the JVM.  The terminal is the same terminal which is accessible using the [`Console` JDK API](https://docs.oracle.com/javase/8/docs/api/java/io/Console.html).

The easiest way to obtain such a `Terminal` object in JLine is by using the [`TerminalBuilder`](https://github.com/jline/jline3/blob/master/terminal/src/main/java/org/jline/terminal/TerminalBuilder.java) class:
```java
  Terminal terminal = TerminalBuilder.terminal();
```
or
```java
  Terminal terminal = TerminalBuilder.builder()
                          .system(true)
                          .build();
```

The `TerminalBuilder` will figure out the current Operating System and which actual `Terminal` implementation to use.
The builder can be further customised in particular to handle signals, see [Signal support](#signal_support).

## Virtual terminals

Virtual terminals are used when there's no OS terminal to wrap.  A common use case is when setting up some kind of server with SSH or Telnet support.  Each incoming connection will need a virtual terminal.

Those terminals can be created using the following pattern:
```java
  Terminal terminal = TerminalBuilder.builder()
                          .system(false)
                          .streams(input, output)
                          .build();
```

The builder can also be given the initial size and attributes of the terminal if they are known:
```java
  int columns = ...;
  int rows = ...;
  Attributes attributes = new Attributes();
  // set attributes...
  Terminal terminal = TerminalBuilder.builder()
                          .system(false)
                          .streams(input, output)
                          .size(new Size(columns, rows))
                          .attributes(attributes)
                          .build();
```

## <a name="signal_support"></a>Signal support

JLine terminals support signals.  Signals can be raised and handled very easily.

System terminals can be built to intercept the native signals and forward them to the default handler.

```java
  Terminal terminal = TerminalBuilder.builder()
                          .system(true)
                          .signalHandler(Terminal.SignalHandler.SIG_IGN)
                          .build();

```

The [LineReader](LineReader) does support signals and handle them accordingly.

##  Terminal building options

| Option        | System | Virtual | Description                                                                                          |
|---------------|:------:|:-------:|------------------------------------------------------------------------------------------------------|
| name          |    x   |    x    | Name of the terminal, defaults to `"JLine terminal"`                                                 |
| type          |    x   |    x    | Infocmp type of the terminal, defaults to `System.getenv("TERM")`                                    |
| encoding      |    x   |    x    | Encoding of the terminal, defaults to `Charset.defaultCharset().name()`                              |
| system        |    x   |    x    | Forces or prohibits the use of a system terminal                                                     |
| streams       |        |    x    | Use the given streams for the input / output streams of the terminal                                 |
| jna           |    x   |    x    | Allow or prohibits using JNA based terminals, defaults to wether the JNA library is available or not |
| dumb          |    x   |         | Creates a dumb terminal if known terminals are not supported, else an exception is thrown         |
| attributes    |        |    x    | Initial attributes of the terminal                                                                   |
| size          |        |    x    | Initial size of the terminal                                                                         |
| nativeSignals |    x   |         | Handle JVM signals from the system terminal through the created terminal                             |
| signalHandler |    x   |         | Default signal handler                                                                               |

## Using terminals

TODO...