---
layout: post
title: Jasmine in Sublime Text
---

I’m learning Javascript, as I’ve told before. And I’m using [Sublime Text 2](http://www.sublimetext.com/), because it is lightweight in the first place, and – to be honest - the hype surrounding it is making me curious. It turns out to be blazing fast, and it is quite easily extensible via the packages and the customizable build system.

While coding a bit to get the hang of some javascript patterns, I thought is would be nice to try if I could easily use [Jasmine](http://pivotal.github.io/jasmine/) to test that code from within Sublime Text. It turns out it is not so hard to do, although there are some limitations. This is how I did it:

The first step is to install [jasmine-node](https://github.com/mhevery/jasmine-node) via node package manager: 
`npm install –g jasmine-node`. 

This makes the package globally available. For instance, you can simply run your tests from the Windows command prompt:

![Jasmine-node via command prompt](/img/jasmine-node-via-command-prompt.png)

As the next step, I added a custom build system to Sublime Text. It’s not complicated, and maybe a little fragile, but it works:

![Sublime Text build system for jasmine-node](/img/sublime-text-build-system-for-jasmine-node.png)

I call it a bit fragile, because of the “file_regex” setting. Basically, with this setting you identify the file and line number that the editor should navigate to when pressing F4. It is not required in the build system, but it’s quite helpful.

And this is the result:

![jasmine-node output - no failures](jasmine-node-output-no-failures.png)

When the test fails, pressing `F4` takes me to the relevant line:

![jasmine-node output - with failures](/img/jasmine-node-output-with-failures.png)

I think it is quite nice.

The limitation I talked about earlier involves the usage of colors in the test output. As you may have notices in the custom build system, I specified the –noColor option. It turns out that the jasmine-node reporter writes color codes that are not rendered as color but as literals. But I’m ok with that for now.