---
layout: post
title: Integration testing with CasperJS
---
[1]: http://casperjs.org
[2]: http://phantomjs.org/

Inspired by a tweet by [@ToJans](http://github.com/tojans), I’ve started playing around with [CasperJS][1], which is, I quote, 
>>an open source navigation scripting & testing utility written in Javascript and based on PhantomJS — the scriptable headless WebKit engine. 

In brief, PhantomJS offers you a Javascript API that allows you to approach web pages, navigate the DOM, etc. without actually firing up a browser UI. On top of that, CasperJS offers an API that helps you with setting up navigation scenario’s, filling forms, follow links, etc.. For a far more accurate and complete definition of the capabilities, you should check the projects themselves.

So you need to install [PhantomJS][2] and [CasperJS][2], both offer downloadable packages that include executables. All that’s left is adding the libraries to your path variable, and you are done.

In my scenario, I have a [Dotnetnuke](http://www.dnnsoftware.com/) site set up, and added an entry to the host file, pointing the `dnndev domain` to my `localhost`. Now, what you’ll see is that because we use Dotnetnuke here, and thus classic ASP.NET, we don’t have very nice looking names on the elements. In other environments, you’ll see much less ugly testing code.

Anyway, the simple first scenario that I’m showing here, is logging into the Dotnetnuke site, and navigating to a page that is only reachable for authenticated users. The code goes like this:

	var casper = require("casper").create();
	 
	var getStartedUrl = "http://dnndev/GettingStarted.aspx", authenticatedPage = "http://dnndev/AuthenticatedUserPage.aspx";
	 
	casper.start('http://dnndev/login.aspx', function() {
	    this.test.assertHttpStatus(200, "The website is up and running");
	});
	 
	casper.waitForSelector("form#Form", function() {
	    this.fill("form#Form", {"dnn$ctr$Login$Login_DNN$txtUsername" : "user"});
	    this.fill("form#Form", {"dnn$ctr$Login$Login_DNN$txtPassword" : "pwd"});
	});
	 
	casper.thenClick("#dnn_ctr_Login_Login_DNN_cmdLogin", function() {
	    this.test.assertEquals(this.getCurrentUrl(),getStartedUrl, "We have successfully logged in ...");
	});
	 
	casper.thenOpen('http://dnndev/AuthenticatedUserPage.aspx', function(){
	    this.test.assertEquals(this.getCurrentUrl(), authenticatedPage, "Navigated to the target page ...");
	});
	 
	casper.run(function() {this.test.renderResults(true);});
A
nd that’s all there is to it … We require Casper, and navigate to the login page. We wait for the form, and when it is present, we simply fill some fields on it, using the name of the elements. I did try using the `fill()` function where you ask for submission of the form, but that didn’t seem to work very well. Therefore, I switched to the 'thenClick()' function, using the name of the login link. Finally, after logging in, we open the page that requires the user to be authenticated.

A small side note, is that – unfortunately – coloring of the test results is not supported on Windows. I believe that there are some solutions suggested, but these involve installation of dll’s that I don’t know the trustworthiness of.
Maybe the next couple of days, I’m going to play some more, and see how things go in somewhat more involved scenarios. In that case, I may follow up on this short intro post.