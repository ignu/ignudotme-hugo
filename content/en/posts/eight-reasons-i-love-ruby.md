
---
title: "8 Reasons I love Ruby"
date: 2009-01-14T12:00:06+09:00
description: "My skepticism of Ruby's productivity claims completely shattered"
draft: false
hideToc: true
enableToc: true
enableTocContent: false
tags: 
- ruby
---

I've been in the Microsoft ecosystem nearly a decade. I had heard that Ruby was more productive for years. Each time I rolled my eyes, confident these developers lacked my  [Resharper/Automocking/Generics/Fluent API Magic](http://geekswithblogs.net/ignu/archive/2009/05/31/automocking-and-bdd-style-tests-with-nunit.aspx) . Then I developed in Rails at  [GiveCamp](http://givecamp.org/)  last year and dear god I was nearly as productive in this framework I barely knew as I was in ASP.NET MVC, a platform I knew inside out. What was I doing with my life?

I am not an outlier in feeling this way. Never has a software developer said "I'm stuck doing Ruby for my day job but I'm really hoping to find a job in .NET or Java."

{{< youtube WQ9XacFIfjc >}}
{% youtube 6Rprx1gY9Ps %}

 [Thoughtworks](http://www.thoughtworks.com/)  conducted [ a survey on the productivity of their Ruby projects](http://martinfowler.com/articles/rubyAtThoughtWorks.html#IsRubyMoreProductive) . Out of 30 projects surveyed, **80% reported being at least 50% more productive because they used Ruby** instead of Java or .NET with more than 60% claiming a productivity increase of 2x or greater. (Only one project (3.3% of projects) reported actually being slower for using Ruby, while  [90% of projects reported some increase in productivity.](http://martinfowler.com/articles/rubyAtThoughtWorks.html#IsRubyMoreProductive) )

In my own estimation, I'd say Rails is somewhere between two and three times more productive than ASP.NET (MVC or Webforms).
Yes, that means I believe a 5 month .NET project could be done in 2 months in Ruby.
Why is Ruby so many times more productive than .NET or Java?

### 1) Gems
What makes Ruby Gems awesome is that, for various reasons, there are gems for everything. So many problems are already solved!
*Video of me whenever I run "gem install"*
Some recent requirements I solved with a simple "gem install":
* PDFs. gem install  [pdfkit](http://github.com/jdpace/PDFKit) , add two lines of code and bam, I can add ".pdf" to a route and get a pdf version.
* Excel. just setup the mime type with one line of code, call . [to_xls](http://arydjmal.com/2009/1/11/to_xls-plugin-export-to-excel-in-rails-the-easy-way)  on any collection and I get an excel doc returned!
* Verb conjugation. I need to figure out how to get the past perfect test of a verb. "gem install verbs"
* Here's a hard one: I'd need profile pictures uploaded to amazon s3 and cropped to three different thumbnail sizes. I also need to run asynchronously so my user doesn't wait 30 seconds after updating their profile. And I should show a default picture of the appropiate size if they haven't uploaded one. This would take how many days in .NET? In Ruby I just had to gem install  [delayed_paperclip](http://jstorimer.com/ruby/2010/01/30/delayed-paperclip.html)  and just call  [one method in my model](http://gist.github.com/491822) . I had this working in minutes.
Then there’s  [twitter](http://www.google.com/url?sa=t&amp;amp;source=web&amp;amp;cd=3&amp;amp;ved=0CB8QFjAC&amp;amp;url=http%3A%2F%2Fgithub.com%2Fjnunemaker%2Ftwitter&amp;amp;ei=1XdOTOefFtC2ngee6ZyYAw&amp;amp;usg=AFQjCNEy-buvYblBH4m2dylgfHCIqUmF2A&amp;amp;sig2=muHlH6lBy_wjL6P0cX0wpg) ,  [devise](http://github.com/plataformatec/devise) ,  [pickle](http://github.com/ianwhite/pickle) ,  [formtastic](http://github.com/justinfrench/formtastic) ,  [friendly_id](http://github.com/norman/friendly_id) …
### 2) Consistency
Ruby tools evolve naturally. Survival of the fittest. The best tools rise to the top; bad tools get ignored. There are different ORMs, view engines, etc, but they usually only exist when they solve a different need. Ruby tools are crafted to fulfill actual needs and don’t have to compete with tools dreamed up to be marketable. There is no split in the Ruby community where half the developers use MSRake or MSSinatra. Every single developer knows and uses Rake.
Because everyone knows Rake, ActiveRecord, Cucumber and RSpec, being a “Rails Dev” actually means something. I have to be very skeptical when interviewing a “.NET developer” and figure out what kind of .NET dev they are.
Every .NET project reinvents the wheel with deployment, ORMs, Migrations, project structure, while every Rails project is nearly identical. This might sound boring, but these inconsequential decisions are already made and free you to solve the actual business problem. (This consistency is also what allows so many gems to integrate so seamlessly) It also lets me be confident any experienced Rails Dev is a good fit for my project. In fact, I hired someone on oDesk this month to help out on a Rails side project. I looked at his github, saw he knew his stuff and he was able to dive in with no ramp up time at all. I would never dream of doing that in .NET.
### 3) Git/Github
With DVCS and the ubiquitness of github, if I need to add functionality to a project, I just can. I just fork, reference my fork in my GemFile (this lets my repository build my version of the gem instead of the one at rubygems.org) and issue a pull request to the project’s owner. Hopefully my change gets pulled into the main repo and I can go back to referencing the main gem. It’s not the end of the world if that doesn’t happen, thanks to the beauty of git, I can keep pulling in new changes from the main repo. The fact that this project will actually have automated tests lets me be comfortable that my patch did not break any functionality.
On that note…
### 4) Testing
Testing isn’t controversial in the Ruby community. Projects without tests are seldom taken seriously. On Codeplex, it’s difficult to find a .NET project with unit tests.
Unit testing in a static language is much harder. For example, you can not use the ActiveRecord pattern, because you would have no way to mock your database operations. You have to wrap every single service in an interface and inject every depdenency. That means wraping things that seem outright silly, like having a class and interface just to wrap DateTime. Now so you can stub it for your tests. In Ruby, you can mock anything at any time. (And for the usecase I just mentioned it’s of course solved, simply *gem install* [timecop](http://github.com/jtrupiano/timecop) *.)*
### 5) Ruby, The Language
 [Much is made of this](http://blog.wekeroad.com/thoughts/why-i-like-ruby-blocks) , so I won’t dwell here.  However the power, the beauty, expressiveness and openness of the language is what allows this community to thrive in the first place, so it definitely shouldn’t be overlooked.
### 6) Things just work
The Ruby community hates configuration and complexity. When I install a gem, it usually Just Works.
Ruby developers seek to ease the pain .NET developers don’t even think about.  Ruby has made great progress in  [removing the pain of XML](http://www.yaml.org/) ,  [CSS](http://sass-lang.com/) ,  [JavaScript Includes](http://documentcloud.github.com/jammit/) ,  [running unit tests](http://ph7spot.com/musings/getting-started-with-autotest) ,  [managing dependencies](http://gembundler.com/) ,  [automating deployment](http://www.google.com/url?sa=t&amp;amp;source=web&amp;amp;cd=1&amp;amp;ved=0CBgQFjAA&amp;amp;url=http%3A%2F%2Fwww.capify.org%2F&amp;amp;ei=WdVOTObpCuTnnQfKy7HnBw&amp;amp;usg=AFQjCNHIYX-Xv1Ae7yf0FkYd5VJX30olVw&amp;amp;sig2=pk8atDYpG23cU5B0NgdkDg)  and even  [JavaScript testing,](http://www.google.com/url?sa=t&amp;amp;source=web&amp;amp;cd=1&amp;amp;ved=0CBgQFjAA&amp;amp;url=http%3A%2F%2Fvisionmedia.github.com%2Fjspec%2F&amp;amp;ei=BoBOTMiiGaDtnQf18Ym0Bw&amp;amp;usg=AFQjCNEcG-gY8FstGZLlDsoZRlfjqHx7_Q&amp;amp;sig2=ZPWS0_LeVdYUU60ajvr0Dw) 
### 7) Heroku
This fits in the Things that Just Work bullet, but no place on this planet can you  [set up a website in 30 seconds with three lines of code.](http://heroku.com/)  Then once you’re set up, you can just click a checkbox  [to get email notifications of exceptions, or code analysis, or a MongoDB database or a bulk email service](http://addons.heroku.com/) . And deployment is just “git deploy heroku.” Oh yeah, and its all free until you start doing signficiant traffic. I never dreamed of hosting so many websites so painlessly.
### 8) Simplicity
Have I mentioned that all these problems are solved and all this shit just works all the time?
I realized how far I had strayed from .NET when a .NET friend told me “Yeah, I got Azure set up in two hours.”
I replied, “Ouch, I’m sorry.”
“What? I thought that was pretty good.”

