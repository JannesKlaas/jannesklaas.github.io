---
layout: post
title:  "Review: Udacity Data Engineering Nano Degree"
date:   2019-08-23 00:00:00 +0000
categories: Engineering
---


![Udacity Cert]({{ site.url }}/assets/udacity_cert.png)

Being long time curious about the future of education and MOOCs, I have taken a lot of online classes. In some ways, what I learned in online classes has become more relevant to my career in data-science than what I learned in college. One portal that I was pretty curious about is [Udacity](https://udacity.com). For those unfamiliar, Udacity offers MOOCs on technical topics from data science to flying cars. It aims to distinguish itself through more polished courses, a "mentor" system and personal support as well as career services. In return, it charges a lot more with a typical "nano degree" as going for $1000. When I saw that they offered a [data engineering nano degree (DEND)](https://www.udacity.com/course/data-engineer-nanodegree--nd027), a topic that I was curious about and felt I wanted to learn, I signed up straight away.

## TL;DR
I learned a lot of practical stuff. It is a great program if you have little time and want to get up to speed with some specific technology quickly. I can see why enterprise customers love this. For individual learners, it lacks theory and may not be worth the money compared to alternatives. Udacity's differentiating "human touch" does not add much value. 


## What is a data engineer?
Similar to data science, data engineering is a vague term and has overlap with backend-engineering or devops. Many data engineers work in Java or Scala. They are often experts in specific technologies that are central to the businesses stack. I have met engineers at big banks making $$$ nursing some 30-year-old pipeline without which the bank would have to shut down. There are a lot of adjecent academic fields, most importantly high-performance and distributed computing, both growing branches of computer science. 

## What expectations did I have?
I was curious about data engineers, because I had worked alongside them as a data scientist. I had looked through some courses on high performance computing including a [free course by georgia tech on udacity](https://www.udacity.com/course/high-performance-computing--ud281) and was looking for a rigorous course that would combine high performance and distributed computing theory with practical applications. Since the marketing materials emphasized career readiness and I knew a few data engineers, I felt udacity would have to offer an extremely strong program with a mix of computer science and practical methods.

## The content
Udacity opted for a vocational training approach, introduced a few popular technologies: Postgres SQL, Apache Cassandra, Amazon Redshift, Apache Spark and Apache Airflow. All code was in either Python or SQL. Each of these technologies was introduced in a module demonstrating it in a case study setting. Each module ended with an assignment which was reviewed and which you had to pass. The first modules assumed absolutely no background knowledge beyond basic python and SQL, while later modules did assume the content of earlier modules. 

Unfortunately, there was no significant theoretical component. There were a few, very introductionary explainers showing e.g. that "distributed" means that software runs on multiple machines and that reading data over a network is much slower than reading data from disk or RAM. 

The video content was of pretty standard MOOC quality, although that standard has risen dramatically I think. The assignments were usually somewhat more difficult, although it rarely took me more than an afternoon to solve them. I liked that they required creative thinking and looking up documentation which aided the learning. While the instructions did encourage to take the projects beyond the requirements, there was no reward for it. In my eyes, it was advantageous to get a general overview through one MOOC, but if you are on a budget, you can get the same content for free at other places.

## The human touch 
Udacity prides itself on it's mentors, community and services. I was especially curious about this, as it is something other MOOC providers do not usually offer. Udacity sits in an odd spot where they want to provide good guidance but do not have the budget to do it properly.

#### Mentors 
"Mentor" is a big and very much overused word these days. [Udacity mentors are relatively low paid, remote workers](https://www.quora.com/How-much-do-Udacity-mentors-make) [whose key qualification is that they themselves have completed the nano degree](https://www.quora.com/What-does-it-take-to-become-a-Udacity-mentor). Do not expect mentors to answer complex queries or give you personalized food-for-thought as a mentor at work might as this is not actually their job. That said, they do provide a bit of extra motivation, and nudge you to actually complete the program.

#### Community 
Udacity has a Stackoverflow-style Q&A forum for people stuck with assignments but it also has a pretty large slack, with channels for individual assignments and nano-degrees. As typical with MOOC forums, the conversations usually rotate around help with assignments and complaining about the course. It is a good thing to have but nothing that sets you apart. I have not yet interacted with the alumni community, but I have seen Udacity staffers post events featuring alumni's so I guess they stay in touch somehow.

#### Career services
Together with your course, you get career services, which mostly consist of some content on e.g. how to navigate the job market as well are LinkedIn and Github reviews. There seems to be interview help, too, although I did not see or search it since I already have a job. The content is basic and strongly targeted to juniors entering the job market for the first time. The reviews are very checklist-heavy, making sure you follow best practice (a professional picture on LinkedIn, say) but do not go in depth on how to present yourself to a very specific audience or how to effectively work with recruiters. Since they have students around the world, they of course can not give too specific advice and I felt that much of the material covered would have helped me had I not seen it somewhere else before.

## Is it worth it?
It depends on how much you value money and time and what exactly you want to learn. I certainly learned a number practical tools that will help me at work. I would have liked to see some more theoretical depth. If you are looking to work as a data-engineer, the DEND might be a small first step, to get a smell of what is going on, but it by no means qualifies you for most data engineering jobs. If you want a curated overview and do not want to spend time searching, this course is for you. Otherwise, there are better options. I would take the course again and generally recommend it to e.g. data scientists that want to get up to speed with data engineering and whose company uses much of the stack from the course.
