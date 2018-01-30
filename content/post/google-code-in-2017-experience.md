---
title: Google Code-In 2017 Experience
date: 2018-01-30T17:01:01.309Z
draft: true
categories:
  - Google Code-In 2017
tags:
  - gci
  - google code-in
  - scorelab
keywords:
  - gci
  - scorelab
autoThumbnailImage: false
coverImage: /images/uploads/cover.jpg
---
30 days, 140+ hours of hard work, many sleepless nights, a lot of missed classes in school and a hell lot of excitement, that is how I can sum up my Google Code-In (GCI) experience for you. Let me tell you, this article itself took 6+ hours to compile and write. Enjoy reading...

![](/images/uploads/gci experiecne.png)

# About me

For all those who don't know me, I am Adhyan Dhull, a 16 year old tech enthusiast from India with a little knowledge of code, a blogger and an open source contributor(thanks to SCoRe and GCI). I am also an avid Physics enthusiast especially in the field of Quantum Mechanics. There is one thing peculiar about me: I do everything up to perfection. I am in Grade 11 and currently enrolled in [Delhi Public School, Sonepat](https://dps.in). I am currently the Head-Boy and lead the Executive Body at my school. I am also a good speaker, I often give presentations and stuff...

# The Beginning

I got to know about Google Code-In from my school's Computer Science teacher Mr. Prabhuji Gupta. Shout out to him as if he wouldn't have  I could not have come this far in the competition. It was 18th December 2017 when it all started and I completed my first task, I was quite late as the competition had already started on 28th November 2017. My sole purpose of enrolling for the competition was to expand my knowledge and start contributing to open source programs. 

# Choosing an Organisation

The first thing you do once you have registered is to choose an organization for which you want to work with and do tasks for. At first, I had a little difficulty in choosing the right organization I stumbled across a few organizations but then settled for one - SCoRe. 

Let me tell you a bit about the Organisation - SCoRe,  Sustainable Computing Research Group at University of Colombo School of Computing is a research group that seeks sustainable solutions for various problems developing countries like Sri Lanka. 

The moment I saw tasks from SCoRe, I figured out they were quite do-able and good quality of tasks to start with. This is where the biggest turn comes in my GCI experience, working with SCoRe completely changed my perception of Google Code-In. The tasks from SCoRe were such well organized that even an inexperienced like me could figure out a way from easy tasks to a bit tough ones. SCoRe opened me to the new world of Open-Source and I would never like to exit it again, I'll keep contributing to the numerous projects under SCoRe Lab.

# Why Open Source?

Wait, you would be thinking - Why does Google Code-In give emphasis on Open-Source? I would just say a line "Open-Source is the future of all programs", It already has set many milestones and much more to go. For a list of advantages of Open-Source checkout [this link](https://opensource.com/article/17/8/enterprise-open-source-advantages).

# The Blog: [gci2017experience.ml](https://gci2017experience.ml)

I created this blog as to provide the upcoming SCoRe or even GCI enthusiasts with a platform of complete experience. I also had to devote time to this blog other than doing GCI tasks but it always helps, I feel happy I would be able to provide others the help I could not get, so do share the blog for others to read.

# An insight of what all I did in this iteration of Google Code-In

## Bassa :

![](/images/uploads/687474703a2f2f676475726c2e636f6d2f3758594b (1).png)

This was one of the most intriguing projects I worked on, and I put a lot of time setting it up. I definitely learned a lot, most important being - shift to any Linux distro in case you want to regularly contribute to open source. I have also now installed Ubuntu 17.10.1 on my machine as I would like to continue contributing to more such awesome projects. I had some problems setting up Bassa in Windows but with the impeccable guides and a lot of useful help from my mentors, I could finally set it up. I also created a complete video tutorial and screencast on how to setup Bassa on a Windows machine (I recently got to know from a few students that my video helped a lot). I also created a detailed description troubleshooting some problems faced and submitted it as an issue. In addition to that, I created an issue and pull request to update the .gitignore file. I also learned a lot about using Python as a backend and also learned how to communicate with SQL using Python. 

I have also written an article on Bassa. Check it out [here](http://www.gci2017experience.ml/2018/01/bassa-automated-download-queue.html). Also [here](https://youtu.be/QAQaThaUOgE) is the link to my YouTube video on "How to  Setup Bassa"

## GoCloud :

![](/images/uploads/logo (3).png)

Okay, so this was another project which quite grabbed my attention and drew me to work on it. I first came across this mastermind project when I saw a task of research about the trending cloud providers. I started to then read about different cloud providers and their API implementations, honestly, it was fun researching, then I created a detailed issue as a report to my research. I also suggested changes in the Wiki and created a PR for corrections in the ReadMe file. 

In addition, I wrote a blog on GoCloud [here](http://www.gci2017experience.ml/2018/01/gocloud-cloud-services-library-for-go.html) and on "How to Set-up GoCloud" [here](http://www.gci2017experience.ml/2018/01/gocloud-how-to-set-it-up.html). I created the Architecture Diagram for GoCloud which reflected the functionality of GoCloud at a glance and was appreciated by my mentor too. 

Next is the most interesting part of my working with SCoRe Lab, I conducted a session on GoCloud in my school. YouTube video for same can be found [here](https://youtu.be/dx8_lcbsb8c). The students were intrigued by the presentation and they cleared all their doubts regarding GoCloud with me. They asked many questions regarding the working and functioning of such services and I was happy to answer them all from my knowledge and research on GoCloud and service providers. Overall, it was wonderful to work on GoCloud.

Here is the Architecture Diagram I created for GoCloud:

![](/images/uploads/gocloud architecture diagram.png)

## ASSET :

![null](/images/uploads/asset_logo.png)

I created a new Homepage for Asset - An Adaptive Sensor Actuator System for Elephant Tracking after doing some research and taking inspirations. [Here ](https://github.com/scorelab/ASSET/issues/20)is the link to the issue I created with the idea.

## NodeCloud :

![](/images/uploads/logo (4).png)

Well, NodeCloud is a wonderful Node.js library aiming at providing unified APIs from different cloud providers. I wrote a detailed blog on NodeCloud here. I also created a Git Pre Commit Hook to run ESLint and fixed linting errors in the google.js file. It took a little time and research on linting errors and the Git Pre Commit Hook but was easy thereafter.

## Git :

![null](/images/uploads/849dac53ec386861333e6f24be7ce33f.jpg)

One of the most important thing when contributing to open source is the mode through which you do it and GitHub just serves the purpose and is correctly called the coders' abode. I had heard about GitHub before but never used it. GCI helped me explore various functionalities of Git command line, creating upstream, fixing linting errors, cherry picking, feature branches and lot many small things which matter a lot.

## D4D - Drone for Dengue :

Another impeccable piece of thought put into working, D4D was the project wherein I wrote officially my first piece of code in Python (considering writing and editing different). I wrote a simple code to resize images from one directory and create a separate directory for the output images. Then I also changed the config file and then successfully ran the extract_features.py file without any errors with a little help from my friend Moses Paul.

## DroneSym :

I created a nice and neat logo for DroneSym which was my first project with Adobe Illustrator. I also researched on alternatives for Firebase Real-time Database and created a detailed report which included how can they be used for real-time based tracking, why were they effective for Dronesym and how they worked. Later, I also suggested an important and crucial feature for Dronesym an issue for which can be found here.

Here's the logo I made for DroneSym :

![](/images/uploads/dronesym logo(1).png)

## Kute :

I really liked the idea of Kute app and the functionality. It has a lot of potential and is the need for the modern always traveling generation. I created impressive icon and logo for the Kute app both of which were appreciated. I also wrote an article titled "Kute: The Next Big Thing?"

Here is the Logo and Icon I made for Kute:

![Logo](/images/uploads/kute logo version 3.png)

![Icon](/images/uploads/kute logo version 2.png)

## ELOC :

I made a logo for this project. The logo describes itself how much of hard work I have put into it. Here is the logo I made :

![](/images/uploads/eloc logo.png)

\*There were also other projects I worked on like [Dengue-Stop](https://github.com/scorelab/dengue-stop), [Stackle](https://github.com/scorelab/stackle), [Androphsy](https://github.com/scorelab/androphsy), [Drola](https://github.com/scorelab/drola) and a few more...

## My Journey to SCoRe LeaderBoard...

It was 20th December 2017 when my friend Sagar Khatri made it to the leaderboard of Drupal(another GCI Organization), and I remember it was one reason for which I became competitive in the competition. Within two days I had completed over 6 tasks and I was on the SCoRe LeaderBoard on 22nd December 2017. Ever since then I never looked back and just put in hard work to make it big. Making it to the leaderboard further pushed me to compete harder for the Finalists or Top 5 and even for the Grand Prize Winners or Top 2.

This is the LeaderBoard as of 18th Jan 2018 :

![null](/images/uploads/capturel.jpg)

The competition ended on 17th Jan 2018, and I was constantly on the leaderboard since 22nd December 2018. Also in this iteration of GCI, I completed a total of 47 (44 SCoRe + 3 others) tasks!

![null](/images/uploads/tasks.jpg)

I do believe in 'Quality over Quantity' and thence I have tried to put the best of my efforts to do all of my tasks.

Another thing which I would like to add which separates me from my competitors is that I had no previous knowledge of Web Development or Android Development or even Designing. Coming from the absolute bottom and competing for the best with the best was absolutely thrilling. This is the reason which still arouses in me a little hope that I can still win GCI 2017 and meet my amazing mentors from SCoRe.



# What did I learn from GCI?

Well, first of all, I would like to thank Google for providing such platforms to students from all around the globe to compete and learn a lot. It helps us interact socially with people worldwide. Competing with students like you and better than you always creates a feeling of competition which is very important in today's terms.

GCI taught me a lot. To start with, we have GitHub; with the help of my mentors and from my research I can now create and handle any GitHub Repository and also perform basic functionalities on the Git command line. I can also now write simple python programs and make them perform simple functions. It is rightly said that one can't learn code but can feel it.

After GCI I can proudly say I have developed a good feeling about code and would definitely like to upgrade my skill-set in 2018. I also learned a lot about the React-Native, Gradle, and Android Studio environment and I hopefully will be creating an android application soon.

I am now also acquainted a bit with machine learning and how to use Node.js libraries. I have become familiar with Jekyll, Ruby on Rails, HTML and CSS and I soon will be creating my own website and a GitHub repository for it to be hosted as {[adhyandhull.github.io](https://adhyandhull.github.io)}. It's live now!

And now the most important part of any program/code compilation: Debugging. I have successfully debugged a lot of files during my GCI journey and hope can do so thereafter too. 

I had absolutely no idea of designing using Adobe Illustrator or Adobe Photoshop, it was when I saw "Begin as a Designer" a set of videos on YouTube made by Ansh Mehra. A big shout out to him as his videos inspired me to start with designing. Do check out the playlist here. I then saw tutorials and started using Illustrator and created some good and appreciable logos/icons.

All-together I can say that I have learned a lot during this 28-day journey and wish to learn in future too because you don't need any competition to start learning :)  it's just your interest which drives you to learn something new.

As images speak more than words, here's a line graph which shows my skill progress :

![](/images/uploads/my skills.png)



# Managing GCI with everyday life

Okay, So I want to discuss this point as it is very important. GCI will hinder with your normal schedule like school, practicals, exams or other competitions. But it depends on your priorities, you need to manage your time well and coordinate with all happening. Sometimes it becomes difficult to manage it well and this creates a problem. I could efficiently manage my time and devote more time to GCI because it was my priority. Also a very big thanks to my parents who understood me and supported me even though I could devote less time to my studies, after all, Indian Education System mostly requires a student to score well.

I have also enrolled into a Coaching Institution and I am busy all day long on the weekends, but let me tell you I was so engrossed into Code-In that I would often try to even check my dashboard for if I got a review from any mentor in the middle of those classes. That is the level of dedication and hard work I have put into GCI. But the great mentor-ship from mentors at SCoRe Lab made it easy for me to compete.

Also, there was a time I would wake-up to Facebook and Instagram notifications but during GCI I could only see my E-Mail notifications, for "has the task been reviewed?", "what comment did the mentor make?" and also "has my pull request been merged?" or "has my issue been responded too?". This enthusiasm kept me going on throughout the GCI and I prefer to keep this enthusiasm for the rest on my life. 



This one month of my participation in GCI made me grow as an open source contributor a more learned and humble person. I made good friends like Padam Chopra, Moses Paul, Raghav Puri, Shlok Jhawar and many more. After all, how can't you be good friends after having the same goal?

Also a special mention for my school-mate and friend Sagar Khatri for making the Dedicated Lab Sessions for GCI in School a fun and informative and also for introducing me to Netlify CMS and helping me set-up this blog.



# Surprise, Surprise!!

So there was a nice surprise for all of the students doing the Git Cherry Picking Task. Yes, It was an Easter Egg - the mastermind from our very own "agentmilindu";). First, as I just aimed at completing the task, I completely missed the message which showed up when I had completed the task. The message read as following and was stored in the secrets.map file.

```
The secret map to the treasures! aHR0cHM6Ly9nb28uZ2wva********
```

Now I would also like to take you to through my treasure hunt for the final Easter Egg.

The string intrigued me, thanks to my interest in cryptography that I could easily figure out that it had been encoded by Base64 encryption. I decoded the string and as I had expected, It revealed this link - 

```
https://goo.gl/hL98**
```

On opening the link, it read "Nothing is here. Nothing was here." Weird right? Why would I find something like this when I am on the right path. Then I found the following string in revisions section

```
 IyBXaGVuIHlvdSBwdXQgc29tZXRoaW5nIG9uIHRoZSBpbnRlcm5ldCwgaXQgaXMgaGFyZCB0byByZW1vdmUgdGhlbS4gVGh1cyBiZSBjYXJlZnVsIHdoYXQgeW91IGNvbW1pdCBhbmQgcHVzaC4gDQoNCjAxMTAwMDEwIDAxMTAxMDAxIDAxMTEwMTAwIDAwMTAxMTEwIDAxMTAxMTAwIDAxMTExMDAxIDAwMTAxMTExIDAwMTAxMTEwIDAwMTAxMTEwIDAwMTAxMTEwIDAwMTAxMTAxIDAwMTAxMTAxIDAwMTAwMDAwIDAwMTAxMTEwIDAwMTAxMTEwIDAwMTAxMTEwIDAwMTAwMDAwIDAwMTAxMTEwIDAwMTAxMTAxIDAwMTAxMTAxIDAwMTAwMDAwIDAwMTAxMTEwIDAwMTAxMTAxIDAwMTAxMTEwIDAwMTAxMTEwIDAwMTAwMDAwIDAwMTAxMTAxIDAwMTAxMTAxIDAwMTAxMTEwID*******************
```



Again, lets back to Base64. So this decrypts to



```
# When you put something on the internet, it is hard to remove them. Thus be careful what you commit and push. 01100010 01101001 01110100 00101110 01101100 01111001 00101111 00101110 00101110 00101110 00101101 00101101 00100000 00101110 00101110 00101110 00100000 00101110 00101101 00101101 00100000 00101110 00101101 00101110 00101110 ******** ******** ******** P.S Something you earned hard should not be shared with the lazy.
```



Nice, we got a binary there!! And the Binary translates to :



```
bit.ly/...-- ... .-- .-.. ********* 
```



And let me tell you, my cryptography knowledge again came to use :). Now you can see this is a shortened link but it wouldn't open to anything! Actually the part after the slash is "Morse Code". The morse code decodes to 

```
3SWL**
```

Well, bit.ly is case sensitive so it would be 

```
bit.ly/3swl**
```



Boom! We just uncovered the treasure. The URL leads you to a Google Forms page - "Treasures of Bassa" wherein the treasure hunters could fill their information and get some Bassa Swag from SCoRe Lab.

That was quite an interesting Treasure Hunt, wasn't it? Thanks to Milindu for this Easter Egg :)

I have hidden some part with asterisks so that the Google Forms Page is not spammed.

This easter egg also taught me to always look around once you are done doing your task, and be a good observer, rushing is never good. Lesson Taken!



# Mentor-ship at par 

GCI gave me an opportunity to work under great mentors from SCoRe Lab who made my first and probably only Code-In memorable -  Milindu S. Kumarage, Rumesh Eranga Hapuarachchi, Malith Senaweera, Dinith Minura, Deniz Karakay, Bhathiya Perera, Vihanga Liyanage, Akarshani Amarasinghe and all others. If it weren’t for these very talented and helpful people I would not have been able to compete. Their constant guidance and support was the fuel to the hard-work I put into the tasks. I honestly bow down to all you guys for showing such humbleness and guiding us throughout the competition.

![](/images/uploads/mentors collage.png)



SCoRe Lab is not only a Research Group but a collection of pretty witty and cooperative people, they turn what they have learned into something of great practical use, that's what I love about SCoRe Lab. I would love to remain in contact and keep contributing to the projects in all possible ways I can :)

A big shout out to Milindu sir for helping at all times be it day or night and constantly guiding even with the dumbest of problems on my part, Malith sir for putting so much of his time and teaching me (indirectly) the most essential part of any coding process - debugging. Also Deniz for being an inspiration for me.



# Should you do Google Code-In?

Coming to the last part of this humongous blog, I would address the most common question - "I am not good at coding! Should I participate in Google Code-In?". In my opinion - Yes, you should! Not knowing coding should not stop you from participating and doing tasks in GCI but your thought that you can't do might stop you! So don't worry and just start doing it, different paths start opening once you take initiative and after all, we always have got Google and YouTube to help us.



With all that said I am aiming for the stars as the results aren't out yet. They will be out by 31st Jan 2018 at 16:00 UTC on the Google Open Source Blog.

Hope my experience provided you a detailed insight of Google Code-In



That's all folks! 

Thank you for reading and do provide your valuable feedback in the comment section.
