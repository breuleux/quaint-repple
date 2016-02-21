
# quaint-repple

Embed a REPL in Quaint

## Install

In your Quaint project directory, run the command:

    quaint --setup repple


## Sample usage

```quaint
repple repl ::
  language = javascript
  theme = zenburn
  code =>
    function fun(superFun) {
      return "Quaint is as fun as " + superFun  + "!";
    }
```


## Sample configuration

```json
"repple": {
  "language": "javascript",
  "theme": "zenburn"
}
```

## `repple` macro

The macro is used like this:

```quaint
repple <type> ::
  <option> = <value>
  ...
```


### Types

There are four "types" of interactive environments that you can embed:

* `repl`: a read-eval-print-loop where you can enter commands and view
  the results.

* `repl-aside`: a repl with an output area on the side. That output
  area can be written to by returning `Into("aside", "something")`
  to the repl.

* `editor`: a full editor with an output area on the side. Hit
  Ctrl+Enter to evaluate the code in the editor. The result will be
  printed out on the side.

* `editor-repl`: a full editor with a repl on the side. Hit Ctrl+Enter
  to evaluate the code in the editor. Then you can use the repl to
  play with the functionality you defined in the editor.


### Options

* `language`: the language to use, either `javascript` or `earlgrey`
* `theme`: the CodeMirror theme to use
* `code`: a code block in the chosen language. If `type` is `editor`
  or `editor-repl`, that code will appear in the editor at the start.
  If `repl` or `repl-aside` it will be executed and its return value,
  if it is not undefined, will be printed out in the repl.
  (Note: use `code =>` instead of `code =`).


## Evaluation environment

The repl and editor have access to a few special variables and
functions:

* `$out`: in the repl, represents the output box for the current
  expression. You may call `$out.log(value)` to log a value there.

* `$repl`: the repl object, if there is a repl. `$repl.cm` is the
  CodeMirror instance for the current expression, if you need to
  manipulate it.

* `$editor`: the editor object, if there is an editor. `$editor.cm` is
  the CodeMirror instance for the editor, if you need to manipulate
  it.

* `Into(id, value)`: when returned to the repl, that object instructs
  repple to print out the value in the element with id `id`. But note
  that the special value `"aside"` will print it in the area next to
  the repl when the type is `repl-aside`.

* `throw ReloadAfterPromise(promise)`: when a value of type
  `ReloadAfterPromise` is thrown, repple will automatically catch it,
  wait for the promise it encapsulates to end, and then re-execute the
  expression. Be careful with this one.

* `compile()`: in the mode `editor-repl`, this will trigger
  recompilation of the editor's contents.


## Options

### language

Options:

* javascript (default)
* earlgrey

The programming language for the editor or repl.

### theme

Default: "default"

The name of the CodeMirror theme to use. You can view all the themes
here:

https://codemirror.net/demo/theme.html
