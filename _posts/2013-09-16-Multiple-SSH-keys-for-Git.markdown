---
layout: post
---

At work we are looking into moving to Git. I decided to generate a separate SSH key pair for my work environment, so not reusing the keys that I have been using for GitHub for example. First thing I bumped into was figuring out how to specify what key file to use in the work environment. This post is merely a reminder to myself.

Turns out that this is quite simple. All you need to do in the .ssh folder, is add a config file, indicating what key to use for what host. So that config file looks like this:

	Host git.company.com
	    PreferredAuthentications publickey
	    IdentityFile ~/.ssh/serge.van.meerbeeck
	Host github.com
	    HostName github.com
	    PreferredAuthentications publickey
	    IdentityFile ~/.ssh/id_rsa

And that is all there is to it.