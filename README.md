# atom-language-raidelve package

## To install (short)

``` apm install https://github.com/sjbertolani/atom-language-raidelve```

___


## To install (long)

0 - In order for the apm install command to work, you must have python 2.7 in your PATH ( due to node-gyp only working with python 2 see issue - https://discuss.atom.io/t/npm-and-gyp-errors-during-apm-install/54658/4). You can check what version is available by typing ```python --version``` . If it is another version, consider modifying your path just for installing this package. You could do something like ```echo $PATH``` and remove any path that leads to another python version ( i.e. ~/anaconda3/bin ). Or you could just append ```export PATH=/usr/bin/:$PATH``` assuming you have python 2 in this directory. Alternatively, you could do something like-> ```export PYTHON=/usr/bin/python2.7``` <- although I haven't test this.

1 - ``` apm install https://github.com/sjbertolani/atom-language-raidelve``` This installs the atom package in ~/.atom/packages

2 - Start Atom

3 - In Atom, open a file containing RaiDelve code that has the file extension ".delve". Ideally, you will see some code now highlighted. 

---

You may also need to do the following things depending on your computer.

A - You may have to set the language in Atom to recognize the file as RaiDelve code. It is supposed to autodetect if the file ends in ".delve" but that has not always worked. See the bottom right hand corner of the Atom editor for the language setting.


## Debugging why the styling doesn't work

### Check the parsing is working
Open a .delve file, set the language to raidelve. Then place your cursor in front of a keyword ( ex. and ). Then use the command palette ( ctrl-shift-p ) and search for 'Log Cursor Scope'. Select that function and you should see a popup in the editor. If the parser is working correctly, you should see "delve " and "keyword.control". If you see "delve" and something else, you may not have your cursor in front of `and`. If you do not see the word "delve" in the popup, the parser is not working. See step 1. 

### Check the CSS styling is working
_This section may no longer apply as now this package should use your default styling settings._

On some machines, you can edit the colors in the styles.less file ( in Atom ) and the colors change immediately. However, I'm not convinced that always works. If the colors change in the delve file when you change them in the styles.less, then your style selection is working. 

If the colors do not change, or if there are no colors for left-hand-side variables ```def sales_event_type[salesevent]``` <- In this piece of code, if everything is working the ```def``` should be blue and the ```salesevent``` should be green. 

---

## Broken?

Atom autoupdated and now I see an error when I open Atom that says something about and npm or NODE_MODULE_VERSION mismatch

    In this case, I found the following to fix it
      1) Go to your package directory ~/.atom/packages/delve-language and try ```npm rebuild --update-binary & npm install``` **
      2) Also do ```apm rebuild --update-binary & apm install```.
      
      ** I needed to do ```export CC=clang & export CXX=clang++``` to get npm rebuild to run without errors.
___

## Background


You don't need to do these steps -> unless we need to debug the npm parser. This may happen if we change the grammar and need to update the parser.

We have a raidelve parser - npm package called ```tree-sitter-delve-language```
this should be installable via npm on the command line

```npm install -g tree-sitter-delve-language```

This repo needs to be installed into Atom ( run from this directory)
```apm install``` or ``` apm install https://github.com/sjbertolani/atom-language-delve```

Then open any file ending in .delve that has code in it.

---

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
