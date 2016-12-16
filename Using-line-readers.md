Line readers are used to read an input line from the console, usually a command line that follow a known syntax that can be leveraged using a [highlighter and parser](Highlighting and parsing).

## Simple line reading

For REPL style programs, one can use a simple loop:
```java
    LineReader reader = LineReaderBuilder.builder().build();
    String prompt = ...;
    while (true) {
        String line = null;
        try {
            line = reader.readLine(prompt);
        } catch (UserInterruptException e) {
            // Ignore
        } catch (EndOfFileException e) {
            return;
        }
        ...
    }
```

## Various calls

There are a few overridden `readLine` methods that takes various parameters, depending on the use cases. They all delegate to the most generic one which is:
```java
  String readLine(String prompt, String rightPrompt, Character mask, String buffer) throws UserInterruptException, EndOfFileException;
```

 * `prompt` is the unexpanded prompt pattern that will be displayed to the user on the left of the input line
 * `rightPrompt` is the unexpanded prompt pattern that will be displayed on the right of the first input line
 * `mask` is the character used to hide user input (when reading a password for example)
 * `buffer` is the initial content of the input line

## Widgets and key mapping

TODO...

