---
layout: post
---
Choices ... choices ....

Holidays, so some time to play with tools outside of the comfort zone. I'm building a small trash application to get some hands-on experience with the stuff I'm picking up, and I'm currently at the point where I needs some styling of a web application. Now, I have used [Bootstrap](http://getbootstrap.com/) before to get some quick styling in application prototypes, and I was happy with the speed it offers to get a decent looking application, but today I followed a tutorial where [Zurb's Foundation](http://foundation.zurb.com/) is used. Time for a small comparison.

After about a quarter of an hour of surfing, these are some of the things to take into consideration. Keep in mind however, that I didn't verify these arguments yet.
* Bootstrap offers UI elements
* Bootstrap gives quick return initially, but customisation afterwards is a PITA
* Foundation uses Zepto, which is a kind of slimmed down jQuery, with a weight under 10kB
* Foundation focuses on mobile from the start, whereas in Bootstrap, mobile support was added in later releases
* This shows e.g. in the flexible grids in foundation, as opposed to a number of fixed-size grids in Bootstrap
* It seems that Foundations’ support for IE is less than Bootstrap support. Has something to do with uage of CSS3 selectors and pseudo-selectors that older versions of IE do not support
* Bootstrap is better documented, and has a wider community

