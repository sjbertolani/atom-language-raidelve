# language-delve package

## To install, from the command line run:

0 - In order for the apm install command to work, you must have python 2.7 in your PATH. You can check what version is available by typing ```python --version``` . If it is another version, consider modifying your path just for installing this package. You could do something like ```echo $PATH``` and remove any path that leads to another python version ( i.e. ~/anaconda3/bin ). Alternatively, you could do ```export PYTHON=/usr/bin/python2.7```

1 - ``` apm install https://github.com/sjbertolani/atom-language-delve``` This installs the atom package in ~/.atom/packages

2 - Start Atom

3 - Add the contents of styles.less from this package into the global stylesheet. You can either find the menu to open "Stylesheet" and paste the contents there. Or you can use the command palette ( ctrl-shift-p ) and search for "Open Your Stylesheet". This is the global style settings for Atom. *If you can help to remove this step, please do it!*

4 - In Atom, open a file containing Delve code that has the file extension ".delve". Ideally, you will see some code now highlighted. 

You may also need to do the following things depending on your computer.

5 - Restart Atom after setting the stylesheet.

6 - You may have to set the language in Atom to recognize the file as Delve code. It is supposed to autodetect if the file ends in ".delve" but that has not always worked. See the bottom right hand corner of the Atom editor for the language setting.

## Debugging why the styling doesn't work

### Check the parsing is working
Open a .delve file, set the language to delve. Then place your cursor in front of a keyword ( ex. and ). Then use the command palette ( ctrl-shift-p ) and search for 'Log Cursor Scope'. Select that function and you should see a popup in the editor. If the parser is working correctly, you should see " delve " and "keyword.control". If you see "delve" and something else, you may not have your cursor in front of `and`. If you do not see the word "delve" in the popup, the parser is not working. See step 1. 

### Check the CSS styling is working
On some machines, you can edit the colors in the styles.less file ( in Atom ) and the colors change immediately. However, I'm not convinced that always works. If the colors change in the delve file when you change them in the styles.less, then your style selection is working. 

If the colors do not change, or if there are no colors for left-hand-side variables ```def sales_event_type[salesevent]``` <- In this piece of code, if everything is working the ```def``` should be blue and the ```salesevent``` should be green. 

Ways to troubleshoot this are to a) check that the contents of styles.less from this package are saved in the Atom global styesheet ( see step 3 ) or b) restart Atom after you save the contents into the stylesheet. 

If parsing is working correctly, but the styling is not, you may still see some highlighting. This is because Atom has some generic CSS defined for certain keywords that overlap with some of the output from this package.

---

## Background


You don't need to do these steps -> unless we need to debug the npm parser. This may happen if we change the grammar and need to update the parser.

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
