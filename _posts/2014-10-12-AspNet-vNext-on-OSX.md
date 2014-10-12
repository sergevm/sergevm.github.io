---
title: ASPNET.vNext on OSX
layout: post_page
---
A couple of months ago I made a first attempt to get [ASPNET.vNext](http://www.asp.net/vnext) working on my Mac. It didn't work out very well, and at the time I didn't feel like putting a lot of effort in it, in particular because my experiments with [OpenIDE](https://github.com/continuoustests/OpenIDE) gave me the impression that Mono on Mac was very unstable.

While I was running through some bookmarked posts in [Pocket](http://getpocket.com) this morning, I stumbled upon a [post](http://weblogs.thinktecture.com/cweyer/) by Christian Weyer about getting vNext up and running on a Linux distrubution. He also had some issues to solve, which was not very encouraging, but as I'm slowly recovering from last night ([beer tasting festival](http://www.mechelen.be/events/15082/2de-bierfestival-mechelen.html), yummy :-)) in the couch, I thought that maybe now was a good time to make a new attempt. 

And yes, I got things working this morning without much of a hassle. I just want to take some quick notes for future recap, because touching new things and then leaving them behind for a couple of weeks always forces me to relearn things over and over.


### Tooling

1. kvm (k version manager)
  * With my previous attempt a while ago, I installed kvm as suggested in the docs, using Homebrew. As the docs indicate, it is a good idea to run `kvm upgrade` to make sure you have the latest version.
  * Before I touched anything, `kvm list` showed that I had currently 3 versions installed. The default version was 1.0.0-alpha3.
  * Running `kvm upgrade` did not install a more recent version. However, later on I cloned the [Home repo](https://github.com/aspnet/Home) for vNext, which uses 1.0.0-alpha4 at the time of writing this, and I had to take some extra steps as I'll explain soon.
1. kpm (k package manager)
  * Running `kpm restore` will have the package manager read your *package.json* file, and resolve the dependencies of your application.
  * I made the assumption that kpm would somehow invoke kvm to install a version that is not yet present on my machine (in *~/.kre/packages*), but apparently this is not the case, as shown further on when I talk about the samples.
  * To find out where the repository for your dependencies can be found, kpm relies on the presence of a *Nuget.Config* file in the root of your application. At the time of writing, this is what the file looks like:

~~~
<configuration>
  <packageSources>
    <add key="AspNetVNext" value="https://www.myget.org/F/aspnetmaster/api/v2" />
    <add key="NuGet.org" value="https://nuget.org/api/v2/" />
  </packageSources>
</configuration>
~~~

### Samples

The repository can be found [here](https://github.com/aspnet/home). While running the console went smoothly, running the HelloMvc sample did not, indicating that the Hosting dll could not be found. To resolve this, I had to do a couple of things:

1. `kpm restore` did not throw any errors, but the packages did not get restored either. Looking into *project.json* revealed a dependency on version 1.0.0-alpha4 of the framework, which was not installed on my machine when I checked.
2. `kvm install 1.0.0-alpha4-10353` fails, because it could not be found on the feed. Some research and I found that kvm.sh sets the KRE_FEED variable to the master branch if it has not been set. When I issued $KRE_FEED on my machine, it showed that the kvm configuration indeed pointed to [the master branch](https://www.myget.org/F/aspnetmaster/api/v2), while I actually needed the development branch. I updated the variable ( `KRE_FEED=https://www.myget.org/F/aspnetvnext/api/v2`) and then trying again resolved this issue.
3. When retrying `kpm restore`, packages still didn't get restored. The final step I had to make, is issuing a `kvm use 1.0.0-alpha4-10353` to ensure that k uses the version that is expected by the application. Alternatively, while installing this version, a could have used a `-p` flag, indicating that I want the version to be the default one.
