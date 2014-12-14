---
author: John Lockwood
layout: post
title: "Post-mortem of our first ScalaUserGroup.org meeting" 
excerpt: "What if we held a Scala User Group and nobody came?  Well, in that case, we'd have more time to write some code!"
description:"What if we held a Scala User Group and nobody came?  Well, in that case, we'd have more time to write some code!"
page.description:"What if we held a Scala User Group and nobody came?  Well, in that case, we'd have more time to write some code!"
categories:
- Miscellaneous
- Scala
- Scala Community
---

Our first meeting of [ScalaUserGroup.org](http://ScalaUserGroup.org) was a very close knit group, inasmuch as it featured me as speaker, and me in the audience. I kept the video of me and the audience on from a few minutes before our appointed time until a half hour afterward. For the first ten minutes or so I said things like "Welcome" (at first) followed by "Is anyone there?" and the like. Then after a bit I turned on some Christmas music. Around 9:20 I said I'd be taking off at 9:30 if no one showed up. For the latter part of my half hour and beyond, I had the fun of standing up a preliminary restful API as the entry point of a Scala and akka based third party ordering system [proof of concept](/asynchronous-order-processing-in-play/) I wanted to work on.

So anyway, by hacking on this I began to get a better feel for restful APIs in akka, and I also learned that if you want to tweak the "constructors" of a case class, you don't overload the constructor since it isn't the constructor you're really dealing with, you overload the apply method of the companion object, as it says in [this stackoverflow answer](http://stackoverflow.com/questions/2400794/overload-constructor-for-scalas-case-classes). The fun thing about new languages is that there are always cool tidbits like that.

By way of conclusion, to all you smart but impatient developers who would rather go hack on your own than hang out in granfalloons like ScalaUserGroup.org, I salute and validate your instincts in this regard, which for my part are generally the same as yours. [Blathering about it on LinkedIn](https://www.linkedin.com/groups/Just-purchased-ScalaUserGrouporg-746917.S.5942076205380427777?view=&gid=746917&item=5942076205380427777) will buy you a recruiter who'll call you to discuss her "many Scala opportunities", leading in the fullness of time to her doing no such thing and trying to strong-arm you into some leftover Rails gig. Starting a user's group online is a good exercise in Vagrant and EC2, and a good excuse to hack on an akka restful API since you cleared a Saturday morning. 

If you're smart you can learn Scala on your own. If you're looking for a friend, buy a puppy.