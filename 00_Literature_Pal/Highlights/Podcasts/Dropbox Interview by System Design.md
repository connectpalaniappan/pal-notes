---
title: Dropbox Interview
full Title: Dropbox Interview
author: System Design
note: 
URL: https://share.snipd.com/episode/5611f21f-e21c-4aad-8517-cbf69a6c2698
published date: 
category: podcasts
source: snipd
note created: 2024-03-14
assigned to: people/pal
priority: P4
work: document
---
author:: [[System Design]]
note:: 
source:: [[snipd]]
url:: [podcasts URL](https://share.snipd.com/episode/5611f21f-e21c-4aad-8517-cbf69a6c2698)
image_url:: [podcasts image URL](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)
category:: [[podcasts]]
date:: [[2024-03-14]]
last_highlighted_date:: [[2024-03-06]]
published_date:: [[]]
summary:: None

![rw-book-cover](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)

## Highlights
### Time 0:00:00
[[2024-03-06]] 11:16
> Designing a Cloud Storage System like Dropbox
> Summary:
> The podcast hosts are conducting a mock interview to design a cloud storage system similar to Dropbox.
> The process involves discussing the functionality of Dropbox, which allows users to back up and retrieve files from anywhere. The mock interview will focus on designing a cloud storage system that replicates Dropbox's features.
> Transcript:
> Speaker 2
> Well, come back to the system design podcast with west and keven. To day, we're going to go back and do a little bit of what we started off the pocas series with, which is a mock interview. We got a request from a listener interested in, you know, listening to another mock interview, so we decided now would be a good time we have you heard about the service drop box?
> Speaker 1
> Yes, it's a tenatula. Lets you back up your files an folders, from your computer to this company's cloud storage, and you can then retrieve it from anywhere. You wan't to lok, from another computer, phone, whatever.
> Speaker 2
> Ye, that's exactly right. So to day we're going to be a mock interviewing and designing a cloud stora system similar to drop box. I'll be the interviewer to day, and west will be the interview so starting out, it's like you described a west, you know, drop box and other cloud service providers are fairly


### Time 0:00:41
[[2024-03-06]] 10:51
> Preparation for mock interviewing
> Summary:
> Preparing for mock interviewing is essential for success in upcoming interviews.
> Transcript:
> Speaker 2
> Ye, that's exactly right. So to day we're going to be a mock interviewing and


### Time 0:31:26
[[2024-03-06]] 11:16
> Choosing the Best Replacement Policy
> Summary:
> Considering the best replacement policy for an application, the least recently used(LRU) policy is often a suitable choice due to its efficient utilization of system resources.
> When evaluating complex systems like Dropbox, it is crucial to assess scalability and business requirements. While the topic is expansive and intricate, key points should be addressed with clarity and thoroughness during discussions and interviews.
> Transcript:
> Speaker 2
> M somesens, yes, that makes senseis this might be, you know, very implicit, but is there s replacement policy that would best fit our needs? I thinkle least recently used, is probably one of the vicsjus, at first thought, yes, that that certainly makes sense to me aso, well, i think this was, this was a good interview, a west. There's obviously, you know, a lot that we can talk about drop box. Drop boxes a lot more complex than any of the other systems that we've sort of talked through. But bengo, my fee back is, i think you hit most of the bulle points very cleanly and very well, as well as, you know, thinking through how we scale and the business requirements. Thanks.
> Speaker 1
> Ye em e, i will say, i have, like, washed a, you too, video of a guy explaining drop boxes architecture. I wasd tot, like six months ago, maybe so i might have had so much sletter information here, but and ame lot of things to think through a somt in. So ne right. Well, de in the interview. Sen cer in the pogesenc oge, i'm to stop now.


## New highlights added March 16, 2024 at 7:22 PM
### Time 0:00:00
[[2024-03-10]] 11:03
> Episode AI notes
> 1. Designing a cloud storage system similar to Dropbox involves discussing its functionality of backing up and retrieving files from anywhere.
> 2. Preparing for mock interviews is crucial for success in upcoming interviews.
> 3. The least recently used (LRU) policy is often a suitable choice for replacement policy in complex systems like Dropbox, focusing on scalability and business requirements.


### Time 0:12:59
[[2024-03-16]] 12:27
> Importance of Metadata in File Management
> Summary:
> In file management, metadata is crucial for tracking changes in files and ensuring synchronization between local systems and cloud servers.
> The client application is responsible for uploading and downloading files while detecting changes based on metadata. This metadata includes a manifest of all files, the last edit time for each file, and a log of every edit for accurate synchronization.
> Essentially, metadata plays a key role in maintaining file integrity and version control in cloud storage systems.
> Transcript:
> Speaker 1
> Riht o, im going the no, just to be cleared. And it takes a little further, you know, yat once you've decided that a part of a file is changed, you initiate the upload to your server, you probably need to pass in some associate. O mediata. Rihtlike no. So tell it. O, here's the file name. Here is the like offset of wak y. Now, this is the tenth block in the file. Am, and here the time stamp that you pulled the file. Ot, so like that. Semy sense.
> Speaker 2
> Yip, that make sense. Just to play a backright? For the client application essentially is responsible for up loading and down loading files, as well as detecting changes in each file based on, you know, some representation of meda Data it. Oh, is there anything that you can elaborate on in terms of what the meta data looks like? It sounds like, you know, you're getting to a key part of this climt application and our cloud star service, which is, we need to be keeping track of some sort of meda data in order to make Sure that our file system is insink with what is on the cloud, right?
> Speaker 1
> Yes, sir. I think yonow things sold what we usoner tstore, like kind of a manifest of all the files that we have. We nee, o, say, for every file, what was the last time that it was edited? And then we need it winchester actually, like every time that it was edited. Riht, so maybe yif tlike you think of a table with a primary key, it's like the primary key is a file name plus the time stamp.


---
title: Dropbox Interview
full Title: Dropbox Interview
author: System Design
URL: https://share.snipd.com/episode/5611f21f-e21c-4aad-8517-cbf69a6c2698
published date: 
category: podcasts
source: snipd
created: 2024-03-17
assigned to: people/pal
priority: P4
work: document
---
author:: [[System Design]]
note:: 
source:: [[snipd]]
url:: [podcasts URL](https://share.snipd.com/episode/5611f21f-e21c-4aad-8517-cbf69a6c2698)
image_url:: [podcasts image URL](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)
category:: [[podcasts]]
date:: [[2024-03-17]]
last_highlighted_date:: [[2024-03-16]]
published_date:: [[]]
summary:: None

![rw-book-cover](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)

## Highlights
### Time 0:00:00
[[2024-03-06]] 11:16
> Designing a Cloud Storage System like Dropbox
> Summary:
> The podcast hosts are conducting a mock interview to design a cloud storage system similar to Dropbox.
> The process involves discussing the functionality of Dropbox, which allows users to back up and retrieve files from anywhere. The mock interview will focus on designing a cloud storage system that replicates Dropbox's features.
> Transcript:
> Speaker 2
> Well, come back to the system design podcast with west and keven. To day, we're going to go back and do a little bit of what we started off the pocas series with, which is a mock interview. We got a request from a listener interested in, you know, listening to another mock interview, so we decided now would be a good time we have you heard about the service drop box?
> Speaker 1
> Yes, it's a tenatula. Lets you back up your files an folders, from your computer to this company's cloud storage, and you can then retrieve it from anywhere. You wan't to lok, from another computer, phone, whatever.
> Speaker 2
> Ye, that's exactly right. So to day we're going to be a mock interviewing and designing a cloud stora system similar to drop box. I'll be the interviewer to day, and west will be the interview so starting out, it's like you described a west, you know, drop box and other cloud service providers are fairly


### Time 0:00:00
[[2024-03-10]] 11:03
> Episode AI notes
> 1. Designing a cloud storage system similar to Dropbox involves discussing its functionality of backing up and retrieving files from anywhere.
> 2. Preparing for mock interviews is crucial for success in upcoming interviews.
> 3. The least recently used (LRU) policy is often a suitable choice for replacement policy in complex systems like Dropbox, focusing on scalability and business requirements.


### Time 0:00:41
[[2024-03-06]] 10:51
> Preparation for mock interviewing
> Summary:
> Preparing for mock interviewing is essential for success in upcoming interviews.
> Transcript:
> Speaker 2
> Ye, that's exactly right. So to day we're going to be a mock interviewing and


### Time 0:12:59
[[2024-03-16]] 12:27
> Importance of Metadata in File Management
> Summary:
> In file management, metadata is crucial for tracking changes in files and ensuring synchronization between local systems and cloud servers.
> The client application is responsible for uploading and downloading files while detecting changes based on metadata. This metadata includes a manifest of all files, the last edit time for each file, and a log of every edit for accurate synchronization.
> Essentially, metadata plays a key role in maintaining file integrity and version control in cloud storage systems.
> Transcript:
> Speaker 1
> Riht o, im going the no, just to be cleared. And it takes a little further, you know, yat once you've decided that a part of a file is changed, you initiate the upload to your server, you probably need to pass in some associate. O mediata. Rihtlike no. So tell it. O, here's the file name. Here is the like offset of wak y. Now, this is the tenth block in the file. Am, and here the time stamp that you pulled the file. Ot, so like that. Semy sense.
> Speaker 2
> Yip, that make sense. Just to play a backright? For the client application essentially is responsible for up loading and down loading files, as well as detecting changes in each file based on, you know, some representation of meda Data it. Oh, is there anything that you can elaborate on in terms of what the meta data looks like? It sounds like, you know, you're getting to a key part of this climt application and our cloud star service, which is, we need to be keeping track of some sort of meda data in order to make Sure that our file system is insink with what is on the cloud, right?
> Speaker 1
> Yes, sir. I think yonow things sold what we usoner tstore, like kind of a manifest of all the files that we have. We nee, o, say, for every file, what was the last time that it was edited? And then we need it winchester actually, like every time that it was edited. Riht, so maybe yif tlike you think of a table with a primary key, it's like the primary key is a file name plus the time stamp.


### Time 0:31:26
[[2024-03-06]] 11:16
> Choosing the Best Replacement Policy
> Summary:
> Considering the best replacement policy for an application, the least recently used(LRU) policy is often a suitable choice due to its efficient utilization of system resources.
> When evaluating complex systems like Dropbox, it is crucial to assess scalability and business requirements. While the topic is expansive and intricate, key points should be addressed with clarity and thoroughness during discussions and interviews.
> Transcript:
> Speaker 2
> M somesens, yes, that makes senseis this might be, you know, very implicit, but is there s replacement policy that would best fit our needs? I thinkle least recently used, is probably one of the vicsjus, at first thought, yes, that that certainly makes sense to me aso, well, i think this was, this was a good interview, a west. There's obviously, you know, a lot that we can talk about drop box. Drop boxes a lot more complex than any of the other systems that we've sort of talked through. But bengo, my fee back is, i think you hit most of the bulle points very cleanly and very well, as well as, you know, thinking through how we scale and the business requirements. Thanks.
> Speaker 1
> Ye em e, i will say, i have, like, washed a, you too, video of a guy explaining drop boxes architecture. I wasd tot, like six months ago, maybe so i might have had so much sletter information here, but and ame lot of things to think through a somt in. So ne right. Well, de in the interview. Sen cer in the pogesenc oge, i'm to stop now.


