# NYSDOH-Sepsis-Data-Open-Definitions



"match": {
  "flags": [ "g", "i" ]
}
```

And specify how many lines under the match should be replaced:

```json
"match": {
  "matchLine": true,
  "matchNextLines": "3"
}
```

This rule will be applied to the entire line with the match and the next 3 lines (below it).
Note that, the `matchNextLines` option can be used only with `matchLine` set to `true`, otherwise it's got no meaning.

#### Getting more from custom patterns

You can event make your patterns to be applied to the html code.
Adding the `forced` option to the `match`:
```json
"match": {
  "forced": true
}
```

From now your pattern will be applied to the html code, so it may seriously broke entire terminal output!
The forced patterns must be carefully designed to correctly manipulate the html code.
If you're a beginner you should do most things without using forced patterns.


### More about regex rules

You can use the following properties in regex matches:

* `matchLine` - bool value specifies if the regex should be applied to the whole line
* `matchNextLines` - integer value specifies how many lines after the line containing current match should be also matched
* `replace` - text that the match will be replaced with

### Special annotation

You can use special annotation (on commands/rules definitions or in settings - command prompt message/current file path replacement) which is really powerful:

* (R - can be used in the rules user definitions)
* (T - can be directly typed to the terminal)
* (A - can be used from the terminal API)

| Property name | Usage context | Description |
|----------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `;;` | R/T/A | Divides the commands (commands divided by this will be executed separatly; one after another) |
| `%(dynamic)` | R/T/A | Indicates that the value should be dynamically updated. Usage example: `echo %(raw) %(dynamic) <ANY CONTENT WITH VARIABLES>` |
| `%(raw)` | R/T/A | Used to delay the variables expansion (the variables are expanded only at output - can be used with `echo` and `%(dynamic)` to create dynamic entries) |
| `%(project.root)` | R/T/A | Refers to the first currently opened project directory |
| `%(project.count)` | R/T/A | Refers to the number of the currently opened project directories |
| `%(project:[index])` | R/T/A | Refers to the choosen currently opened project directory |
| `%(username)` `%(user)` | R/T/A | Refers to the currently logged user |
| `%(computer-name)` `%(hostname)` | R/T/A | Refers to the currently used computer's name |
| `%(home)` | R/T/A | Refers to the current user home directory (experimental) |
| `%(path)` `%(cwd)`  | R/T/A | Refers to the current working directory path |
| `%(atom)` | R/T/A | Refers to the atom directory |
| `%(file)` | R/T/A | Refers to the current file - same as %(editor.file) |
| `%(editor.file)` | R/T/A | Refers to the file currently opened in the editor (full path) |
| `%(editor.path)` | R/T/A | Refers to the file currently opened in the editor (parent folder path) |
| `%(editor.name)` | R/T/A | Refers to the file currently opened in the editor (file name) |
| `%(line)` | T | Refers to the input command number (used for prompt styling) |
| `%(env.[property])` | R/T/A | Refers to the node.js environmental variables - To get the list of all available system properties use `%(env.*)` ([See node.js process_env](http://nodejs.org/api/process.html#process_process_env)) |
