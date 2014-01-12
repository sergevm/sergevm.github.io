---
layout: post_page
---

It's been more than a year ago since I took a stab at [Node.js](http://nodejs.org). At the time, I was looking into [node-inspector](https://github.com/node-inspector/node-inspector) for the debugging of node.js applications. I didn't pay much attention to setting up a dev environment for node applications, as I was focusing on learning more about Javascript.

[1]: http://expressjs.com/
[2]: http://jade-lang.com/
[3]: http://learnboost.github.io/stylus/

Today things are different. During the weekend, I learned some of the basics of node development with [Express][1], [Jade][2] and [Stylus][3]. And I like it. I guess no one can deny that using the same language over client and server-side seems very attractive. Also, I have to admit that one of the compelling elements is that it is no Windows specific development, i.e. the daily development I do to gain a living. I like to expand my horizon from time to time. 

I guess my appetite for digging into node is triggered by [Rob Ashton's series](http://codeofrob.com/entries/grunt+browserify+npm+application=success.html) on how he gets started on a node development project, and while I'm writing this, Rob Conery has started a [series](http://www.wekeroad.com/tags/minty/) on the way he sees nodejs development. Nice timing. Thanks to both of these guys for the extremely useful hints, tips and tricks. Especially Rob Ashton's post was very inspiring for the setup I describe here, as will be obvious from my notes here.

Of course, I still have to find out how well things go when moving beyond the Hello world-ish applications I have seen this weekend. But the modular style that is part of the node DNA is a kind of reassuring at the moment. What I should do (note my careful words :-)) is start developing an application in node that forces me to think about the structure I think a node application should obey to.

The goal of this post is primarily to serve as a reminder of the tooling etc. I looked at this weekend and hopefully the coming days. This should help me get up to speed in the event that I get distracted again, and come back to node after a couple of weeks / months.

So these are the tools that I ran into:

* [express][1]
* [jade][2]
* [stylus][3]
* [browserify](http://browserify.org/)
* [grunt](gruntjs.com)
* [grunt-browserify](https://npmjs.org/package/grunt-browserify)

By the way, as I'm setting up the node environment in OSX, I had to look for a blog editor on OSX as well. It seems there's no excellent editor on this OS, I'm writing this with [MarsEdit](http://www.red-sweater.com/marsedit/), which offers a mediocre experience when compared to [Windows Live Writer](http://en.wikipedia.org/wiki/Windows_Live_Writer).

Anyhow, I'm going to start developing a small project that will never be completed, and to underline this fact, I'll go for the stereotypical blog application. Underneath you find a log on how I got started.

    express blog
    cd blog
    npm install express --save-dev
    sudo npm install -g grunt-cli
    npm install grunt --save-dev
    cp ~/.jshintrc .jshintrc
turn on jshint options for node, remove the indentation rule in the copied .jshintrc
    npm install stylus --save-dev
    npm install jade --save-dev
    npm install grunt-contrib-watch --save-dev
    npm install -g nodemon
    npm install grunt-concurrent --save-dev
After these dependencies are installed, we need to add some configuration. First of all, grunt itself uses a GruntFile.js file, which is a module that exports a function that looks like this in a first basic form:

    "use strict";
 
    module.exports = function(grunt) {
        grunt.initConfig({
            pkg: grunt.file.readJSON('package.json')
        });
    };
 
But we installed a bunch of  other packages, which I believe will be extremely useful when actually starting developing (as opposed to all the configuration stuff). In full fledged form, this is what my GruntFile.js looks like for the moment:

    "use strict";
 
    module.exports = function(grunt) {
        grunt.initConfig({
            'pkg': grunt.file.readJSON('package.json'),
            browserify: {
                'public/app.js': ['client/app.js']
            },
            watch: {
                        files: ['client/**/*.js'],
                        tasks: ['browserify']
                   },
            nodemon: {
                dev: {}
            },
            concurrent: {
                dev: {
                    tasks: ['nodemon', 'watch'],
                    options: {
                    logConcurrentOutput: true
                    }
                }
            }
        });    
        grunt.loadNpmTasks('grunt-browserify');
        grunt.loadNpmTasks('grunt-contrib-watch');
        grunt.loadNpmTasks('grunt-nodemon');
        grunt.loadNpmTasks('grunt-concurrent');
    };
[Grunt-concurrent](https://github.com/sindresorhus/grunt-concurrent) allows for multiple tasks to run concurrently, in my case here both the services offered by [grunt-nodemon](https://github.com/ChrisWren/grunt-nodemon) (restarting the server upon file changes) and [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch), which monitors app.js in the client folder, and triggers grunt-browserify when the file is changed (generate a client-side javascript file from server-side node modules). More on the latter is possibly coming in a future post.
So that's the setup I am going to start with. 
