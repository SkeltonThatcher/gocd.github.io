---
layout: post
title:  It’s not Continuous Delivery if you can’t deploy right now.
status: public
type: post
author: Ken Mugrage
excerpt: <p>I hear people say all the time that they're practicing continuous delivery. This declaration is often followed by something like,  “I can let the security team know anytime”, or “I just have to run the performance tests". If you can't push your software to production right now, you're not done with your continuous delivery journey.</p>
---


<div>
  <div class="float-image float-right">
    <img src="/images/blog/deploy-now/but_it_just_needs_oven.png" class="pad-left">
  </div>

  <div class="float-article float-left">
    <p>
      This is the first in a series of articles that will cover the types of pipelines you should implement to ensure your software is truly ready for production at any time. The culture changes required in most organizations are incredibly important, but I’m going to focus on some technical practices in this series.
    </p>

    <p>
      Years ago, when I was in management, I had a favorite rule. If asked “is something done?” the answer could not include the word “except” or any of its synonyms. 
    </p>

    <p>
      "It’s done except for…" = "no".
    </p>

    <p>
      I hear people say all the time that they're practicing continuous delivery. This declaration is often followed by something like,  “I can let the security team know anytime”, or “I just have to run the performance tests". If you can't push your software to production right now, you're not done with your continuous delivery journey.
    </p>
  </div>
  <div class="clear"/>
</div>

##Some of the things you might not be running but should…

In this article I'm going to give an overview of some of the types of pipelines that you should be running if you want your software to be ready to ship at all times. Of course this is not an exhaustive list, there are most likely things that are specific to what you're doing that you should have, just as there are probably things that I will list that don't make sense for you. The point is that everything possible should be automated as part of your deployment pipeline.

Over the next several weeks I'll be writing more about each of these types of pipelines, follow me on Twitter if you would like to know when new articles come out at <a href="https://twitter.com/kmugrage">@kmugrage</a>.

###Security testing

<div>
  <div class="float-image float-left">
    <img src="/images/blog/deploy-now/but_it_just_needs_recorded.png" class="pad-right">
  </div>

  <div class="float-article float-right">
    <p>
All too often this is the primary category of tasks that don’t get run until everything else is “done”. This often results in issues that are very hard to track down since the time between tests has been very long. By writing these tests all the time you’ll have a much easier time tracking down issues before they become too hard to fix.
    </p>

    <p>
Many people feel it's not the greatest idea to have the same person writing the security tests who is writing the code. There’s also the question of skillset; great security people are not common. It’s important that you use a Continuous Delivery server that is capable of using more than one build material for a single pipeline. That way these tests will run whenever the code or the tests are updated.
    </p>
  </div>
  <div class="clear"/>
</div>

###Performance testing

This one is probably the hardest to run all the time if for no other reason than hardware costs. To properly performance test many applications takes a serious dedication of resources. Luckily public and private cloud infrastructures have made this somewhat easier. Consider having a pipeline where the first stage spins up the machines you need either as virtual machines or containers, runs the tests, and then shuts down those machines.

In this day of “search for a term, hit the link, wait no more than 2 seconds for the page to load” performance is critical. To make matters worse, performance issues are often very hard to track down. You want to know as soon as possible if you’ve introduced a problem.

###Management of the environments

It’s been said many times that it’s much easier to break an application by messing up the environment that it is by doing something wrong in the source code. If something like the security advisory comes out and you need to update systems as soon as possible, you should be able to commit the change to a configuration management tool, have that change picked up by your continuous delivery system and run it through exactly the same process as a code change.

###Testing of the deployment itself

<div>
  <div class="float-image float-right">
    <img src="/images/blog/deploy-now/but_it_just_needs_paint.png" class="pad-left">
  </div>

  <div class="float-article float-left">
    <p>
      This isn’t really a type of pipeline all by itself. This is the concept that you should be deploying the software exactly the same way in every environment that you plan to deploy in production. Unfortunately it’s still not uncommon for people to copy over files to a QA server run test and only then run the actual deployment tool that pushes the same software to a production server.
    </p>

    <p>
      No matter how you’re doing your actual production deployment, whether that is shell scripts, dedicated tools, configuration management tools, or others, you should be deploying in exactly the same way everywhere else. Consider using tools that can read environment specific details from environment variables or other inputs.
    </p>
  </div>
  <div class="clear"/>
</div>


###Why wouldn’t you do this?

One of the biggest objections I hear to running all of these types of pipelines on every change is that the pipeline will take too long to run. This is why having a continuous delivery server that’s capable of running multiple pipelines in parallel while ensuring that software doesn’t go any further if any of those pipelines fail is so important.

The other objection I hear the most is that people simply lack the automation around these areas. This is certainly valid, and I don’t want to pretend that any of this is easy to do. Don’t be afraid to start with what you can, and then add other things your pipeline as your capabilities grow. A continuous delivery pipeline is a bit of a living system it should be evolving along with your processes.

###What are the other big ones? 

I'm very interested in hearing other types of pipelines that you find useful. 

<style type="text/css">
.float-image {
  max-width: 25%;
}

.float-image img {
  max-width: 100%;
}

.float-image img.pad-right {
  padding-right: 10px;
}

.float-image img.pad-left {
  padding-left: 10px;
}

.float-article {
  max-width: 75%;
}

.float-left {
  float: left;
}

.float-right {
  float: right;
}

.clear {
  clear: both;
}

@media (max-width: 699px) {
  .float-left, .float-right {
    float: none;
  }

  .float-image {
    max-width: 100%;
  }

  .float-article {
    max-width: 100%;
  }
}
</style>
