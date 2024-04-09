---
title: SQL vs noSQL Databases
full Title: SQL vs noSQL Databases
author: System Design
URL: https://share.snipd.com/episode/6a85d2be-3f8c-499d-a36b-53cf6600e390
published date: 
category: podcasts
source: snipd
tags: [medium/podcasts, author/System_Design, reader/snipd, date/2024-04-07, area/reader]
created: 2024-04-07
assignedTo: people/pal
priority: P4
work: document
---
author:: [[System Design]]
note:: 
source:: [[snipd]]
url:: [podcasts URL](https://share.snipd.com/episode/6a85d2be-3f8c-499d-a36b-53cf6600e390)
image_url:: [podcasts image URL](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)
category:: [[podcasts]]
date:: [[2024-04-07]]
last_highlighted_date:: [[2024-04-07]]
published_date:: [[]]
summary:: None


![rw-book-cover](https://wsrv.nl/?url=https%3A%2F%2Fstorage.buzzsprout.com%2Fvariants%2F8nk8itdhc6oegfm9zrjzo9f5gh4k%2F60854458c4d1acdf4e1c2f79c4137142d85d78e379bdafbd69bd34c85f5819ad.jpg&w=100&h=100)

## Highlights
### Time 0:00:00
[[2024-04-07]] 05:38
> Introduction
> Summary:
> The snip discusses the difference between sequel and no sequel databases.
> It defines sequel as structured query language used by relational databases like MySQL and SQLite, where data is stored in tabular format with relationships between tables maintained through foreign key relationships. Sequal databases are suitable for maintaining data integrity but may not always be necessary, based on use cases.
> Transcript:
> Speaker 2
> Well, welcome back to our third episode of the podgast, it's fairly we were helping to talk about, ohge, let's tort olows the passoeover. O, welcome back to the show. To day, we were thinking that we would take a break from the mock interview formet and jump into some kind of backing ideas of, like, basely sequel data bases versus new sequel data bases, The trade offs. Which one gives you what we thought we'd talk through that to day.
> Speaker 1
> Ye, if you remember from the last podcast, when we talked about ou designing the system for the facebook feet, we had mentioned no sequel as an alternative to storing the data of a news Feet. And so we wanted to just elaborate on what that exactly means, and just expand upon the advantages and disadvantages sequel verses no sequel.
> Speaker 2
> Qo am, so let's, i guess, jump right in. And we'll start with, i think we are gingto kind of assume a bit of knowledge from the listener in terms of sequel data bases, but we will give some like thought to the features that make Them unique, especially as compared sequalso, you know, i hik have in order some key features of a sequal relational data base to you, yes.
> Speaker 1
> So starting out, let's define what sequel is. Sequal is structured query language. It's not actually like a data base. Its so language that a lot of uno relational data bases used. So any time you see something like, select star from table, that would be useng, you know, sequel syntax. Some examples of sequal data bases would be like my sequo andmsequel. And you can generally think of these data bases as having tabular, formatic data, that is relation one another. So for example, you know, going back to our facebook feed, if you wanted to store that data in a relationa data base, you'd have separate tables, you know, for your users, separate tables For your posts, and you'd have foreign key relationships between those two tables. So that basically what sequel is. And it's pretty useful for if you want to maintain data integrity across, you know, the data that you're storing. But it sometimes isna't over kill, and we'll go into use cases for when that's the case.


### Time 0:07:22
[[2024-04-07]] 05:44
> Is There a Downside to Sequal Data Base?
> Summary:
> The downside of sequel databases lies in their ACID compliance, specifically in terms of performance issues and limitations in distributed systems.
> While sequel databases are efficient in enforcing foreign keys and facilitating operations like joins, these functionalities can lead to slow performance due to the computation of hash tables and query plans. Additionally, the complexity of managing data across multiple tables makes it challenging to replicate and shard data in a distributed system, impacting the scalability and efficiency of the database.
> Transcript:
> Speaker 1
> And if, you know, a transaction is said to have succeeded, that that success won't revert ale latrlet ices at super quick regap, a atomic meaning h transactions succeed hor fail entirely
> Speaker 2
> C, consistency, going from one valid state to the next. Isolation. You don't have like concurrent queries causing weird effects. D for durability, things like stay done when they're done. So can you tell me a bit about, like, of all the properties you just described, like acid compliance in particular, what is there about a sequal data base that is considered a downside? Why do we even need no sequal data basis?
> Speaker 1
> Yes, if the question is, like, what is wrong with sequal data basis, then i think a good analogy that i have off the top of my head, cause i was recently doing a bit of driving lately, is, You can think of sequel data pasis similar toike an automatic transmission in your car. Recently ran into, like, performance issues with my automatic transmission vehicle. I was travelling up to fairbanks, alaska this week. And and on my way up to fairbanks, there's a lot of mountains and hills, and i was driving an older model of car. And i was running into what i thought was transmission issues, because when i was moving up up a steep hill, my car would drop from 70 miles per hour to 50 miles per hour. Ad later, took it into shop and realized that it was because the automatic transmission was not properly computing whether it needed to let down shift gears. And so with sequel tables, you can sort of think of it as the same, right? Like sequel is really smart when it comes tono inforciing, you know, your foreign keys and helping you, you know, do operations like joins against multiple tables. But that that usefulness kind of comes with the cost. Joins are sometimes very slow under the hood. You know, sequel has to compute hash tables, row estimates and come up with his own query plans. And sometimes those query plans off and lead to performance implications. And so just like an automatic car, right? Thereis sometimes performance issues when you don't necessarily might be an over kill a for its use case. The other issue with sequal data basis is, because, you know, you have data living on multipl tables a, it's really difficult to, uknow, repocate and chard thi data across different Notes in a distributed system. So i think something that might be worth going into a little bit west is like the cap theorem.


### Time 0:19:36
[[2024-04-07]] 05:53
> How to Store Denormalized Data With No Joins?
> Summary:
> Storing denormalized data without joins requires a shift in thinking towards storing all the data needed for an operation within a single document at the application layer.
> This approach eliminates the need for joins but results in a heavily denormalized database with fields duplicated in multiple places. To maintain data consistency, the application layer must ensure that every write operation updates the entire denormalized dataset.
> This method is suitable for use cases where high consistency is crucial, despite the database lacking constraints.
> Transcript:
> Speaker 2
> I'm seri tosly isi understand the carinalogy. O, like, basly all the things the data basin forces we caind hovf had to do ourselves, right? So there's some more work on the application layer ourselves, right? Right? Coal, themesons, so i think you might have mentioned a that we don't have any joins. It's not a feature like ilis in general, knows, equal data bases offer you joins. How do you get around that? Like, what if i have, you know, a table of usurs, and i have a table of, like, face wit posts, or, ight, like, how do i come actuall e usuer to a post? Or if i, if you tell me, like, here's a post idea and like, post information, how do i know about who the usurer is? R, things like that.
> Speaker 1
> Yes, it's different way of thinking about how to store your data rit with what h sequel. Your you know, you're naturally thinking about how to wie, normalize my, my data and store things into different tables with no sequel. You'r sort of thinking from the perspective of the application. You're thinking like, this operation that my application neesed to rite, what data does it need to store? And an you would store all the data that you would need for that operation within a single documentt that's how you get rid of the need to do at join. What that does mean is that you often end up with a verily, very demore denormalized data base with, you know, ted of fields in multiple places that you'd have to keep consistent. That's why, you know, we go back and say, like, with no sequel data bases, you want to make sure that you have a very weed heavy use case, because every right that you're doing, your application Layer needs to make sure that data is consistent. As you up data cross youare entire denormalized data set.
> Speaker 2
> It sotti like your bersea demoralized, tired, itisatis. Done.
> Speaker 1
> It's got no constraints.
> Speaker 2
> Co co asom.


### Time 0:21:37
[[2024-04-07]] 05:55
> MongoDB - Is There a Sharting?
> Summary:
> In MongoDB, sharding is a fundamental concept natively supported, enabling the distribution of documents across a distributed system.
> Documents are designed to be denormalized to avoid the need for complex joins. Sharding in MongoDB involves assigning a shard key to each document, allowing MongoDB to determine the node where the document belongs.
> The sharding key should be carefully chosen to ensure even distribution of data across servers, and best practices for determining a shard key can be found in the MongoDB documentation.
> Transcript:
> Speaker 2
> So, yes, my next question would be about, like we talked about, one of the cor pams we had with sequal data bases, is it they aret only shard very well, only get too big for one server. See, wil os ron have a great solution for that. Is hepill help wit that? And how do help that? Yes.
> Speaker 1
> O for mango di tibe specifically, charting is a first class concept. It is natively supported. And the reason why it happens so naturally is because, for the most part, if everything here comes with he bastricsthat for the most part there is no ability todo joins. And so your documents are more or less unitized, right across an entire collection. You can split up your documents into, you know, different notes within your distributed system. For sharting specifically in mongo d b, there's a concept of, like a sharting that you can provide and assign to each document within your collection. And mongo deb is going to take care of, you know, determining which note a specific document falls in, ok?
> Speaker 2
> Grey, asbato ask hoinow we're to look for a particular owich eve to look on. But it sounds like the sharting keys, i'm guessing ther're something lic master table. They have bin scenes of, you know, keys a through f live on the server. Sir.
> Speaker 1
> Ye. And if, you, if you 're interested in learning more about how sharding works, i would definitely point you towards, you know, the mongo d b documentation, which we can link theres you Know, specific details about, you know, what are the best practices for determining a shark key? You definitely want to make sure, you know, the star key that you define is spread out across, you know, the right set of emit allows your data to be spread out equally distributed.
> Speaker 2
> Well, sure, yet you don't no that distribution of data across servers?
> Speaker 1
> Ye, cose.


### Time 0:21:37
[[2024-04-07]] 05:55
> MongoDB - Is There a Sharting?
> Summary:
> In MongoDB, sharding is a first-class concept with native support.
> It occurs naturally due to the absence of the ability to perform joins, which leads to documents being unitized across an entire collection. Sharding in MongoDB involves assigning a sharding key to each document, allowing the system to determine the node where the document belongs.
> It is essential to spread out the sharding key evenly across servers to ensure equal distribution of data.
> For more information on best practices for determining a sharding key in MongoDB, referring to the MongoDB documentation is recommended.
> Transcript:
> Speaker 2
> So, yes, my next question would be about, like we talked about, one of the cor pams we had with sequal data bases, is it they aret only shard very well, only get too big for one server. See, wil os ron have a great solution for that. Is hepill help wit that? And how do help that? Yes.
> Speaker 1
> O for mango di tibe specifically, charting is a first class concept. It is natively supported. And the reason why it happens so naturally is because, for the most part, if everything here comes with he bastricsthat for the most part there is no ability todo joins. And so your documents are more or less unitized, right across an entire collection. You can split up your documents into, you know, different notes within your distributed system. For sharting specifically in mongo d b, there's a concept of, like a sharting that you can provide and assign to each document within your collection. And mongo deb is going to take care of, you know, determining which note a specific document falls in, ok?
> Speaker 2
> Grey, asbato ask hoinow we're to look for a particular owich eve to look on. But it sounds like the sharting keys, i'm guessing ther're something lic master table. They have bin scenes of, you know, keys a through f live on the server. Sir.
> Speaker 1
> Ye. And if, you, if you 're interested in learning more about how sharding works, i would definitely point you towards, you know, the mongo d b documentation, which we can link theres you Know, specific details about, you know, what are the best practices for determining a shark key? You definitely want to make sure, you know, the star key that you define is spread out across, you know, the right set of emit allows your data to be spread out equally distributed.
> Speaker 2
> Well, sure, yet you don't no that distribution of data across servers?
> Speaker 1
> Ye, cose.


### Time 0:21:37
[[2024-04-07]] 05:55
> MongoDB - Is There a Sharting?
> Summary:
> Sharding in MongoDB is a first-class concept natively supported, where documents are unitized across collections to be split into different nodes in a distributed system.
> MongoDB has a sharding concept where each document can be assigned a sharding key, and the system automatically determines the node for each document. Sharding keys are like a master table that ensures data distribution across servers is evenly spread out for optimal performance and scalability.
> Transcript:
> Speaker 2
> So, yes, my next question would be about, like we talked about, one of the cor pams we had with sequal data bases, is it they aret only shard very well, only get too big for one server. See, wil os ron have a great solution for that. Is hepill help wit that? And how do help that? Yes.
> Speaker 1
> O for mango di tibe specifically, charting is a first class concept. It is natively supported. And the reason why it happens so naturally is because, for the most part, if everything here comes with he bastricsthat for the most part there is no ability todo joins. And so your documents are more or less unitized, right across an entire collection. You can split up your documents into, you know, different notes within your distributed system. For sharting specifically in mongo d b, there's a concept of, like a sharting that you can provide and assign to each document within your collection. And mongo deb is going to take care of, you know, determining which note a specific document falls in, ok?
> Speaker 2
> Grey, asbato ask hoinow we're to look for a particular owich eve to look on. But it sounds like the sharting keys, i'm guessing ther're something lic master table. They have bin scenes of, you know, keys a through f live on the server. Sir.
> Speaker 1
> Ye. And if, you, if you 're interested in learning more about how sharding works, i would definitely point you towards, you know, the mongo d b documentation, which we can link theres you Know, specific details about, you know, what are the best practices for determining a shark key? You definitely want to make sure, you know, the star key that you define is spread out across, you know, the right set of emit allows your data to be spread out equally distributed.
> Speaker 2
> Well, sure, yet you don't no that distribution of data across servers?
> Speaker 1
> Ye, cose.


