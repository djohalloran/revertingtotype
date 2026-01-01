---
title: "Syntax Highlighting in Joomla"
subtitle: 
summary: 
author: "Dermot"
date: 2012-03-20T06:57:24Z
draft: false
tags: ["joomla"]

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view: 3

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 3
  caption: ''
  focal_point: "Center"
  preview_only: false

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: "ftth-01.jpg"

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Code listings are often rendered badly in online articles and blogs making them difficult to read and understand. A nice utility to help format and display code within HTML is [Alex Gorbatchev's widely used SyntaxHighlighter](http://alexgorbatchev.com/SyntaxHighlighter/). It is developed in JavaScript so runs in any modern browser. Numerous Joomla implementations of SyntaxHighlighter exist in the form of plugins (have a look here: [http://extensions.joomla.org/extensions/core-enhancements/coding-a-scripts-integration/code-display](http://extensions.joomla.org/extensions/core-enhancements/coding-a-scripts-integration/code-display). The one I used is called Joomler SyntaxHighlighter and was developed for Joomla 1.6 but works in Joomla 2.5 also. It enables you to display nice code listings like this:
```
function foo()
{
 if (counter & lt;= 10)
 return;
 // it works!
}
```
Simply install and enable the plugin in your Joomla installation and highlight any of your code snippets by including some properties within the `<pre/>` tag while in HTML editing mode. For example:
```
<pre class="brush: js; gutter: true;"}
 function foo()
 {
  if (counter &amp; lt;= 10)
  return;
  // it works!
 }
</pre>
```
The SyntaxHighligher supports a whole bunch of brushes including JavaScript, PHP and even Bash. it also includes an auto brush facility which can automatically analyze the code listing to determine what brush to use if you don't specify one (it defaults to plain text).

Note that when using the preformatted style (i.e. the `<pre/>` tag) you will need to escape all right angle brackets must be HTML escaped (meaning all `<` must be replaced with `&lt;`).

Here's a bash example:
```
sudo ./make_me_a_sandwich.sh
```
Some links:

[http://www.webresourcesdepot.com/11-syntax-highlighters-to-beautify-code-presentation/](http://www.webresourcesdepot.com/11-syntax-highlighters-to-beautify-code-presentation/)