---
layout: post
title: How to use SmartOS / Joyent Cloud to deploy and run a fast, easily introspectable and debuggable hypermedia api.
---

How to use SmartOS / Joyent Cloud to deploy and run a fast, easily introspectable and debuggable hypermedia api.

So you are making a sweet new hypermedia api, and wanna use node cuz its hip with the kids. And since its going to be just an api, restify seems a lot more attractive than express. You deploy to heroku, and the api is beautiful. It is self-documenting, has a decent suite of tests, and is fast.

But since you are on herokus free plan and the free redis instance is running out of cache and is way more expensive than you can afford, you look for alternative hosting. And linode has great support and is certainly cheaper than heroku and easier and more performant and cheaper than S3 (according to people smarter than me). But you miss `heroku push`. In comes [deliver][], which is exactly what you want. It even comes with a node.js strategy that just works (thanks to foreman). Config is easy. Hooray Open Source!

So your api is EVEN FASTER and you have 250x the cache for 1/5 the price.

Until you start to hammer it with requests, and they start to time out.

And you realize unlike gdb in C or decoda for lua, you are new to debugging with node. Well nipster tells you about node-inspector, which helps you plug a memory leak, awesome. But it didn't exactly help fix the timeouts. 

The restify framework has DTrace support in its core, but it looks complicated so you search google for ways to see how much time is spent in each function. Again and again, result after result points to DTrace, flamegraphs. Even nodejs.org mentions `node-stackvis`, which is a flamegraph port. Developing in OSX, you figure it will work since you have DTrace, except for the not-so-teensy issue that Apple does not support the Node.js ustack helper, which was mentioned in a few other blog posts. However illumos does. And Joyent, the main company behind node.js has a Cloud, and that Cloud runs SmartOS, which is an illumos distro.

Now, you take a drink, because you have to make a decision. You have sheared sheep before. But this is full-blown yak shaving territory.

You are learning a new operating system, to run a specific profiling tool supported by a particular framework so that you can help debug. The framework will almost certainly be gone in 5 years, probably even node.js will be replaced in that time by better stuff. DTrace will probably be around for a while longer, and its always good to be familiar with a range of operating systems, and DTrace + Zones (not to mention KVM and ZFS) look particularly interesting.

So you bite the bullet, and realize this isn't *just* about getting your api performant - that is an end goal, but not the only goal. Its goal creep.

Fortunately, your API is a personal project, and that is the best place to learn. You are invested in making your API kickass in all the possible ways, and to grow your skills.

So thats the fluff, heres the crunch:

  Your [restify][] api is too slow, almost certainly because of [poor code][].
  You want more powerful profiling, debugging and the ability to scale.

  So learn [DTrace][], which will help debugging across a range of applications.
  And you begin with [flamegraphs][] to start profiling your api.

  Scaling / massive provisining from [illumos][] [Zones][]
  You love the ease [heroku][], but need more control to debug and its expensive.
  So learn [Deliver][] and [foreman][], so deployments are just as easy on any vps.

# So here comes the Yak shaving:


## Getting deployment to SmartOS as easy as Heroku

  The Deliver node.js [strategy][] only supports upstart, which is not on SmartOS.
  No matter what process monitor we use, Deliver will need to be extended. This is easy because its just bash.

  Deliver uses foreman, which can export to a number of different init services, but again, SMF, SmartOS' init of choice is not one of them.

  Foreman does support exporting service definitions to bluepill, which is a rubygem, and since pkgsrc, SmartOS' package repository of choice, supports ruby, we hope it will work.

  So we change the .deliver/config to set SUPERVISOR to bluepill, and `gem install bluepill` on illumos.

  Now extend the deliver node.js strategy by adding 3 lines of code to stop and reload the pill created by foreman.

  Also make sure your user SHELL is set to BASH, as deliver is bash-only.

## More about Deliver

  Should deliver just use foreman start and foreman stop? Should launch() be in libexec/common() and support all the foreman exports directly?
