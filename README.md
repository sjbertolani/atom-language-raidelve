# language-delve package

To install, from the command line run:

``` apm install https://github.com/sjbertolani/atom-language-delve```

In Atom, you may have to set the language to Delve to get the highlighting to work. It is supposed to autodetect if the file ends in ".delve" but that has not always worked. See the bottom right hand corner for the language setting.


Then you need to add the contents of styles.less to the Atom styles.less ( Atom -> stylesheet....). 
^^^ This will install these color selections globably in your editor. There are other ways to do this. 

---
Background

We have a delve parser - npm package called ```tree-sitter-delve-language```
this should be installable via npm on the command line

```npm install -g tree-sitter-delve-language```

This repo needs to be installed into Atom ( run from this directory)
```apm install``` or ``` apm install https://github.com/sjbertolani/atom-language-delve```


Then open any file ending in .delve that has code in it.

---

style.less - how we select and color different items. This needs to be added to your styles.less. Ideally, this should get imported as part of the package but I can't figure out how to do that. 

package.json - where we specify the dependencies ( including the npm package)

grammars/tree-sitter-delve.cson - where you define the css selectors to highlight different aspects of the code

---

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

---

You might need ```npm install -g node-gyp```

---

Additional Notes:

- You can test if the parser is working by placing your cursor before something in the code and running the Log Cursor Scope command ( on a mac this is Command + Option + P ). For example, doing this in front of the keyword ```and``` should result in a pop up that says "delve" "keyword.control". If you see this, the parser is correctly parsing delve.

- These scopes are how we setup the css selectors. In the styles.less you can see how the scopes ( like delve and keyword.control) get mapped from the lefthand side to the right hand side ( css ) selectors.

- In some documentation, you may see something about using patterns to make selections ( in grammar/tree-sitter-delve.cson ). But, because we are using a tree-sitter parser.... you have to wrap this into the scope hierarchy. 
