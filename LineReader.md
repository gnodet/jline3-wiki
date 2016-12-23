The [`LineReader`](https://github.com/jline/jline3/blob/master/reader/src/main/java/org/jline/reader/LineReader.java) interface allows reading lines from a terminal, with full input/line editing.

Instances of `LineReader` can be obtained using the [`LineReaderBuilder`](https://github.com/jline/jline3/blob/master/reader/src/main/java/org/jline/reader/LineReaderBuilder.java) class:
```java
  Terminal terminal = ...;
  LineReader lineReader = LineReaderBuilder.builder()
                              .terminal(terminal)
                              .build();
```

## LineReader building options

The builder can be customised to create more suitable line readers:
```java
   LineReader lineReader = LineReaderBuilder.builder()
                              .terminal(terminal)
                              .completer(new MyCompleter())
                              .highlighter(new MyHighlighter())
                              .parser(new MyParser())
                              .build();
```

| Option        | Description                                                                                          |
|---------------|------------------------------------------------------------------------------------|
| terminal      | The [`Terminal`](Terminals) to use |
| appName       | The application name |
| variables     | A `Map<String, Object>` containing variables |
| completer     | The [`Completer`](Completion) component to use |
| history       | The [`History`](History) component to use |
| highlighter   | The [`Highlighter`](Highlighting and parsing) component to use |
| parser        | The [`Parser`](Highlighting and parsing) component to use |
| expander      | The [`Expander`](Variable expansion) component to use |

## Using LineReader

See [Using line readers](Using line readers).