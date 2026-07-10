+++
draft = false
date = 2026-07-10T10:00:00+01:00
title = "I passed CKAD exam!"
description = ""
slug = "i-passed-ckad-exam"
authors = ["Łukasz Siedlecki"]
tags = ["kubernetes", "certification", "ckad"]
categories = ["Certifications"]
externalLink = ""
series = []
+++

After weeks of preparing, I finally passed the CKAD exam. CKAD consists of 16-20 hands-on tasks. I've read that time management is the most important thing on this exam. I have to agree with that.

## How did I prepare?

Firstly, I started with Certified Kubernetes Application Developer (CKAD) by Mumshad Mannambeth on Udemy. There I realized how K8s works in general. Later I read "The Kubernetes Book" by Nigel Poulton to keep an eye on the details.
In the meantime I started to set up my own Talos Linux K8s cluster, and experimented there, but this is a story for a separate post. Eventually, I ended up with "Ultimate Certified Kubernetes Application Developer (CKAD) Mock Exam Series" on KodeKloud and I put effort into doing hands-on labs. I wasn't aware it wasn't my final boss yet.
I did every KodeKloud mock exam twice. My scores were high enough so I was happy. It was time to book my exam. It would be in two weeks. More than enough.
Only after that I remembered that I still had two attempts on killer.sh. I started doing my first attempt. My surprise was huge. Tasks were much harder than KodeKloud ones. Or maybe not harder at all, but more time-consuming. I had to pay attention to more details in one task. When I was doing KodeKloud mock exams, I always had some time left (about 20-30 minutes, depending on the test).
Killer.sh was different. I had 10 minutes left and still hadn't resolved every task. I felt like I was struggling. I didn't pass my first attempt. And after that I realized what I had written earlier was right - time management.
Of course, I've heard that the real exam is a little easier than killer.sh. But it didn't convince me. I decided not to study more, and instead decided to manage my time better. I spent the next two weeks doing my regular things, and then...

## The day before the exam

I ran killer.sh again. I expected what I would find there. I didn't do every task in order. Firstly I did the easiest ones, later I moved to harder ones. And this was a good strategy. I passed that mock exam 10 minutes before the end. I achieved a high result (99/113 points) so I felt ready to go live.

## Exam day

I didn't stress at all about the exam content. I did stress about my environment for the exam. The exam could be taken only online, in your own place, but the environment should be well-prepared. No bargains, nobody in the room, no noise, etc. I prepared one room very well. I kicked everyone out of the house, including the dog.
My pre-exam check went smoothly. Of course, I carefully read the whole instructions before the exam day, and later I followed the proctor's instructions exactly.
And my exam started... And that was when I started to worry. (It's worth mentioning that at exactly that time my neighbor decided to cut the grass with a very noisy mower, and I was afraid my proctor could hear that :D)
The first question was very time-consuming. I spent about 12 minutes doing it. I knew that I should start with the easiest, but I wondered if there would be any. So I ended up doing this first task, which had a lot of Deployment stuff to do. There was a notification that I couldn't delete and recreate the Deployment to pass this task. Luckily just before the exam I repeated how to edit a deployment on the fly.
But ok, I did it, and moved to the next. The next questions were a little easier. After 10 (of 16) questions I decided to start skipping the hardest ones, and I would come back if I had enough time. I went through every question, skipped 3, and still had about 30 minutes.
That was fair enough. I could take a breath and continue. I did every task I skipped, and still had 10 minutes. I started to check the most difficult tasks. And it was a good idea, because I found some mistakes, and incomplete tasks there. When I finished I had 3 minutes till the end of the exam.

## Conclusions

The results are available 24 hours after you finish your attempt. That was the longest 24 hours in my life :) But eventually, I passed with 90%, where the score needed is 66%.

![CKAD exam score](/images/ckad_score.png)

### The most important things to remember:
1. Learn K8s commands well, especially how to generate YAML using imperative commands. There is not enough time to write YAML from scratch!
2. Learn how to effectively use K8s documentation, since it is allowed on the exam. It helps a lot with small tuning, which is impossible to remember.
3. Flag and skip a question if it seems difficult, and do the easiest first. As far as I know, it's common for the first question to be the hardest one, so watch out for that trick :)
4. Prepare your environment well.
5. Good luck and have fun :)