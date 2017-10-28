Tab completion of available commands, options and parameters is supported by
implentations of the [Completer](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/reader/Completer.html) interface. Results are returned as a collection of [Candidate](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/reader/Candidate.html). `Completer`s can be combined into a hierarchy.

## Completer Subclasses

[AggregateCompleter]() &ndash; Combines zero or more completers.

[ArgumentCompleter]() &ndash; invokes a child completer, so individual completers do not need to know about argument parsing semantics.

[DirectoriesCompleter]() &ndash; returns matching directories as a collection of [Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html?is-external=true)

[EnumCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/reader/impl/completer/EnumCompleter.html) &ndash; Needs description.

[FileNameCompleter]() &ndash; returns matching files as a collection of [Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html?is-external=true)

[FilesCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/builtins/Completers.FilesCompleter.html) &ndash; Needs description.

[NullCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/reader/impl/completer/NullCompleter.html) &ndash; Needs description.

[RegexCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/builtins/Completers.RegexCompleter.html) &ndash; Needs description.

[StringsCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/reader/impl/completer/StringsCompleter.html) &ndash; Needs description.

[TreeCompleter](https://static.javadoc.io/org.jline/jline/3.5.1/org/jline/builtins/Completers.TreeCompleter.html) &ndash; Needs description.

*TODO: make code examples for all of the above.*

## Pro tip
If you use a `TreeCompleter`, and you want all of the top-level node values to be displayed, thereby displaying the available commands, when the user's first keypress is a tab,
call `unsetOpt` on the `LineReader` as shown:
```
LineReader reader = LineReaderBuilder().builder()
    .terminal(terminal)
    .completer(treeCompleter)
    .parser(parser)
    .build()

reader.unsetOpt(LineReader.Option.INSERT_TAB)
```
