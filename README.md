# language-delve package

We have a delve parser - npm package called ```tree-sitter-delve-language```
this should be installable via npm on the command line

```npm install -g tree-sitter-delve-language```


This repo needs to be installed into Atom ( run from this directory)
```apm install```

Then you need to add the contents of styles.less to the Atom styles.less ( Atom -> stylesheet....). 

Then open any file ending in .delve that has code in it.

---

style.less - how we select and color different items. This needs to be added to your styles.less 


package.json - where we specify the dependencies ( including the npm package)

grammars/tree-sitter-delve.cson - where you define the css selectors to highlight different aspects of the code


Resources

Tree Sitter grammar spec for delve
https://github.com/RelationalAI/raicode/blob/master/deps/src/parser/delve.js

How to add a new grammer to Atom using the Tree Sitter syntax
https://flight-manual.atom.io/hacking-atom/sections/creating-a-grammar/

A walkthrough that shows how to add a grammer to Atom
https://gist.github.com/Aerijo/df27228d70c633e088b0591b8857eeef

Create Syntax Highlighting Package
https://www.sitepoint.com/how-to-write-a-syntax-highlighting-package-for-atom/

https://stackoverflow.com/questions/38928523/in-an-atom-package-how-do-i-style-patterns-in-a-grammar

https://acarril.github.io/posts/atom-latex