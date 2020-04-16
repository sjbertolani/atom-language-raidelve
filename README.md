# language-delve package

Until further notice:

We have an npm package called ```tree-sitter-delve-language```
this should be installable via npm on the command line

```npm install -g tree-sitter-delve-language```


This repo needs to be installed into Atom ( run from this directory)
```apm install```


package.json - where we specify the dependencies ( including the npm package)

grammars/tree-sitter-delve.cson - where you define the css selectors to highlight different aspects of the code


Resources

Tree Sitter grammar spec for delve
https://github.com/RelationalAI/raicode/blob/master/deps/src/parser/delve.js

How to add a new grammer to Atom using the Tree Sitter syntax
https://flight-manual.atom.io/hacking-atom/sections/creating-a-grammar/

A walkthrough that shows how to add a grammer to Atom
https://gist.github.com/Aerijo/df27228d70c633e088b0591b8857eeef