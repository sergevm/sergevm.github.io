---
layout: post
---

The last couple of years, I have been working on a little Android development learning project. Well, in the end it has become a considerable code base, because I always enjoy working on a realistic feature set, even in this kind of setting (learning, that is). I have pushed the code to GitHub this evening, as I don't intend to work on it anymore (hey, I bought myself an iPhone a couple of months ago :-)). You find the unfinished code here.
[1]: http://developer.android.com/sdk/index.html
The project has been quite a learning experience in many ways:

* The last time I wrote some java code must have been more than 10 years ago. Java has evolved quite a bit since then, and e.g. the use of generics differs quite a bit from the generics I know and love in C#.
* I used [Eclipse](http://www.eclipse.org) as an IDE for the first time. The last time I wrote some lines of code in java, I used [VisualCafé](http://en.wikipedia.org/wiki/Visual_Caf%C3%A9). You need to learn to work with work spaces, manipulate build paths, etc.. Further more, over the nearly 2 years I occasionally worked on the project, the IDE as well as the [Android SDK](http://developer.android.com/sdk/index.html)[1] and other tools went through some revisions. If you look closely at the commits on the project, you will see that I struggled with these revisions quite a bit.
* Of course, the [Android SDK][1] was totally new for me, and I had to learn the controls, the advised UI flows, localization etc. from the ground up. As often, Google was my friend in these learning days.
* I learned a dependency injection framework ([Google Guice](https://code.google.com/p/google-guice/) and [Roboguice](https://code.google.com/p/roboguice/)). The latter helps a lot in setting up views, and really is a productivity booster. The links to the libraries are included in the readme on GitHub.
* I learned [JUnit](http://junit.org) to write my tests. I used [Mockito](https://code.google.com/p/mockito/) for mocking purposes. I didn't really get into using the Android SDK support for UI tests, and sticked purely to "domain" tests. It was the testing bit that led to experimentation with a DI framework in the first place.

Oh, I almost forgot to introduce the functionality of the application. 

The app is a stereotypical todo list manager (oh no, not another one), that works with a local database ([Sqlite](http://sqlite.org)), and that offers synchronization with [Toodledo](http://www.toodledo.com/). It integrates with the Android OS using the alarms infrastructure in order to display reminders (e.g., remind me once, or remind me every 2 hours). Periodic tasks can be defined (e.g. "Send invoice", each 1th of the month). 

When you read the code, bear in mind that this is an informal learning project. Because of this, and as the code base has become quite large, there are - without a doubt - several inconsistencies in the code. That's okay for me, it was never intended to be production code. At some places, the code may feel a bit overcomplicated, and it probably is. Finally, I'm sure I did not always write idiomatic Java code. 