---
layout: post_page
title: Getting acquainted with NodeJS
---

Once again, I have set a personal goal to study the foundations of javascript. It goes without saying that I have done my share of  DOM element manipulation, be-it based on some raw `getElementById()` navigation in the past, be-it with invaluable libraries such as [jQuery](http://www.jquery.com) in more recent years. However, that kind of javascript barely reveals the real power of the language (which in that context typically is ‘hidden’ by the libraries you use) with features such as prototypal inheritance etc., and I believe the time is right to learn about them. After all, javascript is gaining importance on the client-side as well as on the server side, proven by  the rapidly growing popularity of [NodeJS](http://nodejs.org), the emergence of lots of useful client-side libraries such as [jQuery](http://jquery.com), [Backbone](http://backbonejs.org), [KnockoutJS](http://knockoutjs.org) to name a few, and more recently the introduction of [TypeScript](http://www.typescriptlang.org/) by Microsoft.

I’m one of those old-fashioned guys who like reading books on technical topics I want to get to know. Of course I’m aware of the fact that some Google foo will lead you to plenty of resources, but I still prefer the structural learning that good books seems to offer. To learn the foundations of javascript, I have read [Javascript: The Good Parts](http://shop.oreilly.com/product/9780596517748.do), and [Javascript Patterns](http://shop.oreilly.com/product/9780596806767.do), two books I certainly recommend.

Anyway, after reading up on a topic, I need to get my hands dirty fiddling around some code. And this time, I’m taking the opportunity to get acquainted to [Sublime Text 2](http://www.sublimetext.com/) for editing .js files. Because I’m studying the basics, I’m writing and executing lots of scripts that do not involve DOM manipulation. In Sublime Text 2, you can use the nodejs package to execute code, and e.g. write some stuff to the console. All fine and dandy, until you run into a problem and need to debug. As there’s no html page that runs in the browser, you cannot simply use the well-known and excellent browser developer tools.

I started to look around for ways to solve this, and I learned the existence of [node-inspector](https://github.com/node-inspector/node-inspector). This is how I got it working on a Windows 7:

* You should have node installed.
* Install node inspector with npm (node package manager): `npm install –g node-inspector`
* Navigate to the folder containing the script you want to debug, say test.js. Start the script, but let the debugger break on the first line: `node –debug-brk test.js`
* You get a notification that the debugger is listening on port 5858
* You can check this by navigating to http://localhost:5858
* In another console, start node-inspector. You get a message saying that you should navigate to http://localhost:8080/debug?port=5858 to start debugging … and bingo!

In Sublime Text 2, with the nodejs package installed, you execute a script using the Alt-R shortcut. I’m aware that there’s also Alt-D to execute the script in debug mode, but I need to find out how to use this mode. More on that in another post maybe …

![Start NodeJS in debugging mode](/img/starting-node-with-debugger.png)

![Starting up node-inspector](/img/starting-up-node-inspector.png)

![Node debugging is activated](/img/node-debugging-activated.png)

![Debugging NodeJS with node-inspector in action](/img/debugging-with-nodejs-in-action.png)

