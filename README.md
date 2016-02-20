
# quaint-repple

Embed a REPL in Quaint

## Install

In your Quaint project directory, run the command:

    quaint --setup repple


## Sample usage

```quaint
repple repl ::
  language = javascript
  theme = xcode
  code =>
    function fun(superFun) {
      return "Quaint is as fun as " + superFun  + "!";
    }
```


## Sample configuration

```json
"repple": {
  "language": "javascript",
  "theme": "xcode"
}
```

## `repple` macro

```quaint
repple <type> ::
  <option> = <value>
  ...
```

### Types

* `repl`
* `repl-aside`
* `editor`
* `editor-repl`


### Options

* `language`
* `theme`
* `code`


## Options

### language

Options:

* javascript (default)
* earlgrey

The programming language for the editor or repl.


### theme

Default: xcode

The name of the CodeMirror theme to use. You can view all the themes
here:

https://codemirror.net/demo/theme.html


