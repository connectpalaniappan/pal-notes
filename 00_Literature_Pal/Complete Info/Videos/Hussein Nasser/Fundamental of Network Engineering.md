---
tags:
 - author/HusseinNasser
 - people/pal
 - date/2024-03-21
---
# Introduction 
## Who is this course for? 

So who is this cause for?

I specifically built this course for back end engineer like myself who are really building back in applications

that clients consume, but they don't really necessarily understand what is going on behind the scenes.

**When a segment arrives at their application, what the operating system is doing, what is the application is listening on, and why the segment goes to a certain process but not the other.**

It's effectively tries to unveil and remove the blinds from this, you know, foggy, understanding and trying to build a bridge. That gap, as I talked about previously and also remember that the fact that we're using the word back and kind of indicate that there is a frontend that consumes that back in and mostly the medium that connects the back end to the front end is networking.

So really good idea to understand what is happening behind the scenes when you're building these basic fundamentals. This course is also very good for frontend engineer who are trying to build back in application or built back in application before.

Because guess what?

Frontend engineers are those who make the calls to the back end to an API to consume it.

So it's really interesting to send a call and really follow the call all the way to the back end and make sure that it actually reaches.

So if there is a slowdown in a certain request, it doesn't mean that a back in is slow.

Could be the networking between this point, to this point has certain limitation and it's good to understand that there could be a configuration in your client side when it comes to the network and is way lower level down beneath you.

You know it doesn't it's not something you as on the application necessarily without Node.js or Python as low level is so understanding that and once you really understand is what really matters here when

you understand you know what to do.

When you don't understand, it becomes really a black box and you're just left out with more confusion.

Because also for network engineers who are interested to build back end or frontend applications and not rendering already understand these basic fundamentals.

You know, some, some of them you don't understand everything.

Nobody does, obviously.

But that gap that we talked about between the application and the networking is really huge.

And you'll be surprised that most of the networking that I met, we don't see the application.

**They treat everything above Layer seven as an application, although there are so many other layers above that, you know, it's not just, oh, why is the application doing sending a reset to the socket?**

Well, sometimes the even the back end engineer doesn't understand why is happening, not necessarily.

Right.

So there is a huge gap between the network engineer and the backend engineer and I try to bridge that

gap as much as possible.

Sometimes I fail, sometimes I succeed.

But this is the goal of this course, at least to bridge this gap.

So if you are networking Jews who want to build application and you want to even to refresh your memory

on this kind of thing, I think this course, this course might be for you.



## Course outline 

00:00.120 --> 00:02.490
So we talked about who this course is for.

00:02.760 --> 00:07.560
We talked about an overview of the course, but now what do we need to talk about the outline of the

00:07.560 --> 00:07.920
course?

00:08.190 --> 00:11.190
What are you going to get when you finish by the end of the course?

00:11.460 --> 00:12.540
What are you going to grasp?

00:13.020 --> 00:13.190
All right.

00:13.350 --> 00:14.190
How about we jump into it?

00:14.220 --> 00:21.540
So I broke up this course into six sections, but not necessarily they will remain six section when

00:21.540 --> 00:28.050
you watch this content, because I, as you might know from my other courses, I always add and make

00:28.050 --> 00:30.090
the courses and add more content to the course.

00:30.240 --> 00:35.370
It'll be more than six sections of activity, but the major six sections are.

00:35.370 --> 00:38.610
The first thing I'm going to talk about is the fundamentals of networking.

00:38.610 --> 00:46.540
And these are two sets of lectures that will help you kind of build the foundation, if you will, of

00:46.670 --> 00:51.720
of the networking aspects, like starting from scratch as if you don't know anything.

00:51.960 --> 00:55.440
What why do we need networking?

00:55.440 --> 01:01.830
Why networking was invented as a model client server, architecture, hostels, communication, things

01:01.830 --> 01:02.280
like that.

01:02.580 --> 01:08.820
To talk about just a fundamental on networking that we really need to understand before jumping into

01:08.820 --> 01:16.590
the other protocols, which the first one very critical is the Internet protocol, the IP.

01:16.860 --> 01:23.550
So we're going to demystify everything there is about the Internet protocol, the IP.

01:23.550 --> 01:26.580
And I'm going to go into details here.

01:26.820 --> 01:31.290
I'm going to talk about the routing protocol.

01:31.290 --> 01:33.900
I'm going to talk about how the IP address looks like.

01:34.140 --> 01:37.590
I'm going to talk about how the IP packets are routed.

01:38.130 --> 01:43.890
Go talk about certain protocols that are complementing the IP protocol, ARB, ICMP, stuff like that,

01:43.890 --> 01:51.990
and not just mentioning them, actually linking them with reality with what we do on a daily basis.

01:51.990 --> 01:53.520
And that's what I believe missing.

01:53.520 --> 01:56.730
And most of the courses that I interacted with at least.

01:57.860 --> 02:01.400
The link between what we do and what we study.

02:01.950 --> 02:07.960
Even mathematics, if you know it is like I used to like mathematics, but a lot of people were frustrating

02:07.970 --> 02:13.130
with mathematics because they memorize a formula and I have no idea when to use it because they are

02:13.130 --> 02:14.180
memorizing things.

02:14.420 --> 02:19.280
A lot of people memorize networking concept because they have no idea when this thing shows up.

02:19.580 --> 02:23.680
So I tried to bridge that gap by giving you examples as much as possible.

02:23.690 --> 02:28.760
So I try to give you as much as examples as possible when it comes to linking the networking aspect

02:28.760 --> 02:31.610
with real life examples, you know.

02:32.240 --> 02:38.090
I have 17 years of experience, so I try to pull in examples from personal problems that I've personally

02:38.090 --> 02:45.230
faced and from my colleagues that I ran into or from blogs article I read and I tried to reference all

02:45.230 --> 02:45.560
of these.

02:45.560 --> 02:49.250
So you'll see all the tons of references in this course as well.

02:49.250 --> 02:57.260
And it would be a good idea to download the master slide deck to It's Over, I think 170 slides, you

02:57.260 --> 02:58.820
know, there's a lot of stuff there.

02:59.750 --> 03:02.630
But yeah, it's going to be very, very interesting.

03:02.630 --> 03:06.080
The IP protocol, very, very critical concept.

03:06.110 --> 03:09.890
So another thing in the IP section, I'm going to talk about the IP packet itself.

03:09.890 --> 03:16.130
We're going to turn to the cartoon and then I'll try to understand all these headers that we have.

03:16.130 --> 03:19.430
And then what are the use cases for this head on when they will show up?

03:19.670 --> 03:21.290
And I'm not going to explain all the headers.

03:21.410 --> 03:28.760
I'm going to explain the headers that are personally I interacted with and I they kind of pinched me

03:28.760 --> 03:33.620
in a way or another, you know, some of them obviously I don't know everything, but I will talk only

03:33.620 --> 03:36.560
about the things that I believe is relatable.

03:36.560 --> 03:41.570
You know, some of that not all of the headers are I have personal experience with, so I'll explain

03:41.570 --> 03:42.380
whatever I can.

03:42.440 --> 03:48.830
So as a back an engineer, you really, to be honest, really care about what the headers are and try

03:48.830 --> 03:50.300
to understand or memorize them.

03:50.300 --> 03:51.200
Almost never.

03:51.410 --> 03:54.320
If you want to know what a header looks like, you can just google it.

03:54.560 --> 03:56.030
You know, never memorize anything.

03:56.540 --> 03:58.490
This is not what the course is for, you know?

03:58.730 --> 04:03.170
It's just understanding sometimes what each header do does.

04:03.170 --> 04:07.760
And if you want a refresher, you can always Google how it looks like, you know that's that's what

04:07.760 --> 04:08.930
it really critical here.

04:09.110 --> 04:10.520
And the next one is the UDP.

04:10.520 --> 04:16.460
I started with UDP because kind of TCP is, I would say like a superset of UDP.

04:16.460 --> 04:22.640
UDP is a simpler protocol, you know, so I'll talk about a UDP datagram that's why we call it the pros

04:22.640 --> 04:27.620
and cons of UDP, when to use it, when not use it, you know, as again personal experiences.

04:28.010 --> 04:32.990
And we'll talk about the TCP protocol and talk about the segment concept.

04:32.990 --> 04:37.250
I talk about the handshake, talk about why does TCP exist?

04:37.250 --> 04:46.690
I tried to I had a lecture which explains why do we need blah?

04:46.820 --> 04:48.110
You know, why do we need IP?

04:48.110 --> 04:49.130
Why do I need you to be?

04:49.130 --> 04:54.290
But it kind of it became a little bit a little bit cumbersome to manage.

04:54.680 --> 04:58.880
But that's what that's really what the question you you should ask all the time.

04:59.240 --> 05:01.190
It's like, why do we need IP protocol?

05:02.280 --> 05:08.070
Once you really ask the question of why it really unlocks something in your brain, you know, because

05:08.250 --> 05:11.580
you will understand why it exist.

05:12.090 --> 05:14.580
You know, because always anything exists.

05:14.580 --> 05:20.190
Because most of the time it exists because of a problem that we try to solve and we invent something

05:20.190 --> 05:20.520
to solve.

05:20.520 --> 05:26.220
This problem for nothing exists just for the sake of fashion, you know, always.

05:26.610 --> 05:34.800
And, and I find it personally when I, when I, when I understand why something exists, I, I find

05:34.800 --> 05:36.870
it I find it easier to remember.

05:37.170 --> 05:38.970
I find it, you know, more.

05:39.150 --> 05:44.190
I don't I don't I don't have, you know, fog and misconception anymore.

05:44.190 --> 05:45.330
I just find it very clear.

05:45.330 --> 05:45.600
So.

05:45.960 --> 05:49.320
TCB, We're going to ask you like why this EP exists.

05:49.320 --> 05:54.450
So that's a whole new section is it's filled with content.

05:54.480 --> 05:55.980
You talk about flow control.

05:56.400 --> 05:57.900
Why does full control exist?

05:58.450 --> 05:59.640
We're talk about congestion control.

05:59.670 --> 06:00.400
Why does it exist?

06:00.420 --> 06:06.320
When I was slow, start the super fast open handshake, closing connections connection states.

06:06.320 --> 06:12.060
I'm going to talk about so much stuff, but don't be overwhelmed because most of this is going to be

06:12.060 --> 06:12.360
fun.

06:12.750 --> 06:19.080
Because I'm going to explain because I really enjoy talking about these concepts and relate them to

06:19.080 --> 06:24.570
the to the present, to, to what we do on a daily basis that back intention into two applications that

06:24.570 --> 06:25.200
we develop.

06:25.710 --> 06:28.020
Right instead of just memorizing stuff.

06:28.020 --> 06:33.840
You know, then my favorite section, which is this is the section that kind of bridges the gap.

06:34.350 --> 06:36.480
This is the section, right?

06:36.480 --> 06:38.790
That will.

06:39.860 --> 06:45.470
Cement the first principle of networking and kind of link them to the back end performance, you know,

06:45.710 --> 06:46.400
and this section.

06:46.430 --> 06:50.720
One of my favorite networking concept that effect back in applications design.

06:51.860 --> 06:58.160
You know this this this this section specifically is the link that links that back in engineering to

06:58.160 --> 06:59.270
the network engineering.

06:59.510 --> 07:10.340
You know, you will find most of these lectures that I, I authored as a link to directly to the performance

07:10.340 --> 07:12.560
of the back end application or the front end application.

07:12.560 --> 07:17.870
Because some of this stuff is really a configuration of the client side because the client needs to

07:17.870 --> 07:21.980
make a connection at the end of the day, you know, and the concept of a connection, the concept of

07:21.980 --> 07:31.340
a performance, the concept of why when I make this handshake after a while, immediately I my data

07:31.340 --> 07:37.040
is not getting through like or why is when I started the application is so slow, but after a while

07:37.370 --> 07:41.480
it picks up why I cannot listen on on the same port twice.

07:41.690 --> 07:42.200
Why?

07:42.830 --> 07:44.480
Why cannot why cannot to do that?

07:44.570 --> 07:47.300
Why when I send I tried to send a request.

07:47.560 --> 07:50.780
It's very, very slow and I have no idea why.

07:51.080 --> 07:58.010
There is really something that this large request that I tried to send, it's really slow for some reason

07:58.010 --> 08:00.170
why it doesn't make any sense.

08:00.290 --> 08:01.190
And why does it?

08:01.190 --> 08:05.540
Sometimes when I connect to this server as fast when but when I connect to the server a slow, you know,

08:05.540 --> 08:07.070
the response comes slower.

08:07.670 --> 08:16.760
All these things, you know, while they are a little bit low level understanding them kind of bridges

08:16.760 --> 08:21.980
the gap between the back end application that we write when you actually write a line of code says,

08:21.980 --> 08:29.060
hey, I want to listen to this port on this IP address, what does what is it really that is happening

08:29.210 --> 08:30.500
when I receive data?

08:30.770 --> 08:31.100
No.

08:31.220 --> 08:35.210
And we're going to explain the concept of a request, you know, and all these stuff.

08:35.840 --> 08:37.310
It's fascinating to me.

08:37.310 --> 08:39.140
I absolutely love this thing.

08:39.500 --> 08:46.460
I talk about the maximum segments, ISE and maximum transmission unit and how do this to leg to each

08:46.460 --> 08:54.230
other and why what what determines the size of this packet or the segment specifically?

08:54.230 --> 08:59.900
And is larger packets or segments better you know all these kind of things.

09:00.650 --> 09:09.590
I how fast can I send data all the you know and how does this translate to manage GDP request get request

09:09.590 --> 09:14.450
for example all these things my thought to explain this as much as possible then as I believe it's going

09:14.450 --> 09:20.390
to be fun and unfortunately is not it won't be a networking course without actually firing up Wireshark,

09:20.420 --> 09:26.570
which is if you don't know Wireshark is this utility that allows you to sniff any packet that is going

09:26.570 --> 09:29.360
out of your machine that Wireshark is in a stolen.

09:29.570 --> 09:31.160
And we'll look through that.

09:31.250 --> 09:33.920
So we're going to warthog TCP protocol.

09:33.920 --> 09:40.810
We're going to want to CHAKA UDP how looks like we're going to wireshark ebs we go through it.

09:40.820 --> 09:44.900
We will do a trick to actually describe the Dallas handshake and look at the content.

09:44.900 --> 09:47.150
So there's going to be so much fun.

09:47.840 --> 09:54.560
Obviously, if there was an additional section, I'll add a new kind of a lecture, talk about the course

09:54.560 --> 09:58.430
update and then just like I do with my database and other courses as well.

09:59.090 --> 10:02.060
So I believe I really hope you enjoy and enjoy this course.

10:02.300 --> 10:03.770
And let's get started.



# Fundamentals of networking 

## Client server architecture 
WEBVTT

00:00.150 --> 00:04.440
So I thought we start with the [[Client]] [[server]] architecture.

00:05.190 --> 00:07.770
This is the revolution that started it all.

00:08.070 --> 00:16.350
You know, how can I put my server and my client in different location where different core pieces of

00:16.350 --> 00:17.730
code can live somewhere else?

00:17.970 --> 00:22.620
And I need to call certain piece to execute somewhere else.

00:23.220 --> 00:24.450
A revolution, indeed.

00:24.690 --> 00:27.330
Now, we don't have this big mainframe.

00:27.340 --> 00:28.550
We don't need them anymore.

00:28.560 --> 00:29.520
You know where it runs?

00:29.520 --> 00:30.090
Everything.

00:30.270 --> 00:36.450
We can just have cheap commodity hardware sitting on the client and move them.

00:36.450 --> 00:39.630
<mark style="background: #BBFABBA6;">Move their workload that are really heavy on the server.</mark>

00:39.870 --> 00:41.030
That's basically it, you know.

00:41.070 --> 00:45.150
So if you think about it, machines are expensive, applications are complex.

00:46.140 --> 00:49.280
How can I separate the application into multiple component?

00:49.290 --> 00:54.750
Doesn't necessarily just do you know, just let's break down the application that is running on a single

00:54.750 --> 00:56.070
machine into two components.

00:56.320 --> 01:02.850
If you think about it, microservices kind of inherited or borrowed from this model kind of, you know,

01:02.850 --> 01:10.200
because we have we used to have this big monoliths service and we broke it into multiple smaller microservices

01:10.200 --> 01:12.570
and let them call each other effectively.

01:12.900 --> 01:17.820
That's the same, you know, original classic concept.

01:18.450 --> 01:21.360
Let's, let's break our application into multiple components.

01:22.080 --> 01:23.160
Let them call each other.

01:23.400 --> 01:24.690
And that's the beauty here.

01:25.200 --> 01:30.810
Expensive workload can be done on the server where you can anything that is expensive.

01:30.840 --> 01:37.440
What do you say when we say expensive here.We really mean Ram takes a lot of Ram or takes a lot of CPU

01:37.440 --> 01:42.540
or takes a lot of latency, whatever that means, right?

01:42.720 --> 01:46.980
Reading to desk, you know, takes time to do all this computation.

01:47.520 --> 01:55.740
Let's move them to a a server, a machine that is a really beefy that has good resources.

01:55.980 --> 02:02.820
And then let's keep the caller in a smaller, you know, tablet or, you know, I thin out a client,

02:02.820 --> 02:03.300
if you will.

02:03.450 --> 02:04.680
Now, that's that's the beauty here.

02:05.320 --> 02:08.790
The clients call servers to perform expensive tasks.

02:09.420 --> 02:10.770
So simple, so elegant.

02:11.040 --> 02:13.380
A remote procedural call was born.

02:13.440 --> 02:16.230
This is what what what what we refer to our RBC.

02:16.710 --> 02:17.070
Right.

02:17.100 --> 02:21.050
RBC calls has been there since was sixties seventies.

02:21.060 --> 02:25.590
You know the idea of let's make a call by to a remote call.

02:25.920 --> 02:28.440
You know, previously there was no standard.

02:28.440 --> 02:30.210
You know, let's just let's whatever.

02:30.210 --> 02:34.290
Let's just send it across there, the wire.

02:34.290 --> 02:36.380
And there's absolutely no no standard.

02:36.660 --> 02:43.110
You as long as you can make it to the server, you've done it, you know, but those standards started

02:43.110 --> 02:43.640
to build up.

02:43.650 --> 02:50.010
And this is there's another important technical concept to, you know, J RBC.

02:50.490 --> 02:56.870
G RBC actually borrowed also from this concept, you know, where the Google, a remote called procedure,

02:57.060 --> 03:05.790
you know, kind of used to be to to build upon this concept but make it the universal I believe now

03:05.790 --> 03:12.570
it's a job is is there is a universal effectively communication between any two components if you are.

03:12.840 --> 03:14.910
So what are the benefits of clients over architecture?

03:15.930 --> 03:19.050
Servers have DVR, where the clients have community hardware.

03:19.050 --> 03:22.800
So you can have a lot of clients call a single server, if you will.

03:23.670 --> 03:31.260
So in this case, you kind of centralize the work and you can you kind of scale better, you know?

03:31.560 --> 03:39.000
Clients that I built, I swear, this is the same concept as microservices because this is the same,

03:39.270 --> 03:42.570
you know, advantages to microservices, like let's scale them better.

03:42.750 --> 03:48.090
Don't get me wrong, I don't necessarily in favor of microservices.

03:48.120 --> 03:50.550
I've been very critical of this technology.

03:50.550 --> 03:55.140
You know, I talked about it in my YouTube channel, but there are benefits definitely, you know.

03:55.140 --> 03:58.720
But I think we're we're a little bit overdo it with microservices.

03:59.070 --> 04:00.060
But that's another topic.

04:00.390 --> 04:05.130
So yeah, so the idea here is just really scale better clients that calls.

04:05.400 --> 04:11.010
Yeah, you can do as many clients because now they are lighter, they start faster because they're they

04:11.010 --> 04:15.300
don't they don't have all this application logic that I used to have.

04:15.300 --> 04:17.070
You know, the binaries are smaller.

04:17.460 --> 04:19.860
My God, this is so much better.

04:19.860 --> 04:22.740
You know, just move it around so clients go.

04:23.310 --> 04:24.090
But here's the thing.

04:24.930 --> 04:28.920
Clients can still perform lightweight tasks.

04:29.460 --> 04:33.510
This is the this is the trend with edge computing.

04:33.510 --> 04:40.620
If you heard about it, you know, even clients that Iot devices that are literally just censoring data

04:40.620 --> 04:46.590
and then sending requests somewhere else, they can't perform, perform compute logic.

04:46.980 --> 04:52.620
You know, unfortunately, all of these Iot devices are just mining Bitcoin at this moment.

04:52.710 --> 04:55.080
But regardless, you get the idea, right?

04:55.080 --> 04:58.230
You can you can do work in the client site as well.

04:58.500 --> 04:59.850
Now people are moving here.

04:59.880 --> 05:02.040
This is like, okay, let's do more client side logic.

05:02.040 --> 05:03.570
But that's the beauty here.

05:03.720 --> 05:05.910
Client no longer required dependencies.

05:06.060 --> 05:06.900
What does that mean?

05:07.620 --> 05:14.850
The application when you built it, when it was a monolith in one machine, it records all these dependencies,

05:14.850 --> 05:22.140
all his libraries, all these, you know, calling to desks, calling to whatever, you know, printer,

05:22.410 --> 05:29.070
all this stuff, all these dependencies or no, the server responsibility.

05:29.070 --> 05:32.730
I mean, if you want to talk to a database, you need a database driver.

05:32.910 --> 05:38.130
Now, at least Oracle, a SQL Server does, you know, for example, that means you have to install

05:38.130 --> 05:40.140
this runtime in your application.

05:40.140 --> 05:41.190
I'm just an example here.

05:41.760 --> 05:45.870
So if you move the server, you know, somewhere else.

05:46.870 --> 05:47.290
Right.

05:47.830 --> 05:53.850
The server only needs to talk to the De Beers, so it needs that dependency while the client is lightweight,

05:53.860 --> 05:54.820
it just makes the call.

05:55.680 --> 05:56.020
Yeah.

05:56.290 --> 05:59.590
And we're going to talk about what does that mean, making a call in a minute.

06:00.550 --> 06:05.020
So that's that's really powerful, if you think about it, you know, and that's where the three tier

06:05.020 --> 06:09.940
architecture, when it comes to the database and moving the server, it kind of it's got I consider

06:10.000 --> 06:13.630
the three tier architecture is going as a special case over there clients over if you will.

06:13.960 --> 06:14.530
However.

06:15.790 --> 06:16.330
However.

06:17.680 --> 06:19.590
We need a beautiful communication model.

06:19.600 --> 06:24.670
We cannot we cannot let this be the wild, wild west, my friends.

06:24.670 --> 06:25.210
We cannot.

06:25.810 --> 06:26.380
We need.

06:26.380 --> 06:27.880
And we need a standard.

06:28.120 --> 06:28.590
Okay.

06:29.230 --> 06:29.800
Got it.

06:29.830 --> 06:31.060
Client server is awesome.

06:31.480 --> 06:32.800
I need a network.

06:33.190 --> 06:38.920
You know, I need to send a call, send some data from one machine to another.

06:38.920 --> 06:43.060
But how should I connect them with a telephone wire and then send data?

06:43.090 --> 06:43.330
How.

06:43.330 --> 06:44.110
How do I do that?

06:44.290 --> 06:44.620
Well.

06:47.450 --> 06:49.490
You can do it any way you want.

06:49.940 --> 06:56.960
You know, if you figured out how to transpose, if you will, the bits into radio or electric signal,

06:56.960 --> 06:59.810
you can do it anything you want, but there is no standard.

06:59.990 --> 07:03.980
So we need a standard so we all can understand each other, you know, very critical.

07:05.120 --> 07:07.280
How about we jump into the next lecture?





  

## OSI model 
WEBVTT

00:00.030 --> 00:06.720
In this lecture, I'll talk about the Orci model, the open systems inter connection model.

00:07.530 --> 00:12.990
And I still remember 20 years ago when I was in university and.

00:14.080 --> 00:20.530
My instructor tried to explain the LCI model and I really, truly didn't understand anything.

00:21.610 --> 00:29.470
And I really didn't think it was important because because I was excited about, you know, writing

00:29.470 --> 00:32.110
C code and C++ code.

00:32.860 --> 00:34.360
I wanted to build an interface.

00:34.360 --> 00:36.430
I want to build a visual basic application.

00:36.430 --> 00:41.920
And, you know, I was I was interested in that stuff and I really didn't understand the value of what

00:41.920 --> 00:43.540
they were explaining, right?

00:44.290 --> 00:50.620
AD And so I end up memorizing everything and I was just like passing the exam, but I didn't get anything.

00:50.650 --> 00:55.060
Unfortunately, although the doctor the doctor was really good, you know, unfortunately.

00:55.180 --> 00:57.820
So I really regret that.

00:57.820 --> 01:00.400
But so what I wanted to do is just learn from that experience.

01:00.400 --> 01:07.000
Always a model is really critical to understand any engineer or any software engineer.

01:07.210 --> 01:15.460
If you ever want to interact with networking, you really need to understand those AI model, you know,

01:15.640 --> 01:17.770
and don't.

01:19.240 --> 01:26.140
Don't think like you have to understand everything in it, but just understand this seven layers effectively.

01:26.230 --> 01:31.570
And we're going to talk about also about the simplified Orci model because it does have some criticism,

01:31.570 --> 01:32.620
you know, when it comes to that.

01:32.920 --> 01:41.920
But just the Orci mind these seven layers and where does your application live that is what really matter.

01:42.280 --> 01:43.810
Where does your application live?

01:43.840 --> 01:45.220
You might say, I don't care.

01:45.430 --> 01:48.880
Why would I care where my app live?

01:49.120 --> 01:50.290
No, you should.

01:50.500 --> 01:58.270
Because if your app is a bridge between two other apps, we really need to understand.

01:58.270 --> 01:59.350
What are you looking at?

01:59.620 --> 02:00.850
What do you see?

02:01.300 --> 02:03.130
Are you looking at Mac addresses?

02:03.130 --> 02:04.910
Are you looking at IP packets already?

02:04.930 --> 02:09.040
Looking at segments, are looking at ports, are looking at the DCP options?

02:09.460 --> 02:15.220
Or are you looking at the consider of a connection, the TCB connection itself or audio decoding or

02:15.220 --> 02:26.110
encoding the audio serializing this allows in Jason or you decrypting my stuff to look at it and every

02:26.110 --> 02:31.810
single layer has a meaning and every application out there, a CD and a reverse proxy, a load balancer,

02:31.810 --> 02:36.940
a reverse proxy, an API gateway has to live in one or more of these layers.

02:37.270 --> 02:38.710
And this is what I wanted to talk about.

02:39.220 --> 02:42.220
Let's jump into the slides and nail this.

02:42.880 --> 02:44.890
I promise this is going to be fun.

02:44.950 --> 02:45.190
All right.

02:45.190 --> 02:48.460
So these slides a little bit later, so I'm going to disappear in a minute.

02:48.460 --> 02:50.260
But I used the awful day.

02:50.280 --> 02:51.160
I'll be here.

02:51.160 --> 02:51.670
I'll be here.

02:51.670 --> 02:57.820
I'm just going to explain that concepts behind the scenes and I'll show up at the end to summarize this

02:58.210 --> 02:58.720
stuff.

02:59.050 --> 02:59.320
All right.

02:59.470 --> 03:09.640
Those I model the open systems interconnection model, you know, open systems open has to be open because

03:09.880 --> 03:12.880
we really need an open communication.

03:12.880 --> 03:16.600
We really need to understand and make a standard out of this thing.

03:16.720 --> 03:19.180
So Orci model, let's get started.

03:20.710 --> 03:22.420
Why do we need a communication model?

03:22.810 --> 03:30.460
I always, as you know, I always start with a Y because to me, I don't like to understand something

03:30.460 --> 03:33.610
that I don't know why it exists personally, at least you know.

03:34.000 --> 03:37.360
So the goal here is to build agnostic application.

03:37.390 --> 03:44.260
So, you know, imagine this if you really don't have a standard, then we want to build a networking

03:44.260 --> 03:45.010
applications.

03:45.280 --> 03:50.920
Then we cannot do this because my server have no idea how to talk to your client.

03:51.160 --> 03:52.600
Like, how are you?

03:53.410 --> 03:59.110
You know, how do you how are you transposing the beds into digital to analog and analog back to digital?

03:59.110 --> 04:02.440
How, how, how am I supposed to look at this bits?

04:02.440 --> 04:04.600
You know, there must be a standard.

04:04.780 --> 04:10.540
It doesn't have to be a stunner, have to be a protocol to understand how to chop up these beds, to

04:10.540 --> 04:12.370
make sense of it as the application level.

04:12.670 --> 04:17.470
Without a standard, your application must have knowledge of the underlining network medium.

04:17.470 --> 04:18.400
That's even worse.

04:19.720 --> 04:20.620
Imagine this.

04:20.770 --> 04:27.550
Just imagine if you have to author a different version of your apps so that it works on Wi-Fi.

04:28.210 --> 04:30.160
You need a different version to work on within it.

04:30.490 --> 04:35.720
You need everybody to work on LTE and you need a different order version to work in fiber.

04:36.160 --> 04:37.510
That will be a disaster.

04:37.690 --> 04:39.850
Yes, we take it for granted today.

04:40.090 --> 04:42.010
We take it definitely for granted.

04:42.370 --> 04:43.630
Let me show up for a second.

04:43.780 --> 04:45.520
We really take this thing for granted.

04:45.970 --> 04:51.040
You are building a Node.js application today and you're sending a request or just listening.

04:51.280 --> 04:57.820
And it doesn't matter where this application runs, it runs on any CPU, you know, because someone

04:57.820 --> 04:58.870
smart built it.

04:58.870 --> 05:00.430
So it compiles on all CPUs.

05:00.820 --> 05:07.450
And when you send a request, it doesn't matter if before sending it through the satellite or sending

05:07.450 --> 05:15.850
it through radio Wi-Fi or sending it through Ethernet electric signals or sending it through the LTE

05:15.850 --> 05:18.550
radio waves, or they get it through fiber light.

05:19.240 --> 05:21.040
It doesn't matter why?

05:21.040 --> 05:29.500
Because we built a standard and that standard is used globally.

05:29.950 --> 05:31.510
Effectively, yeah.

05:34.130 --> 05:37.220
And the whole ward was the difference in my ward and global.

05:37.250 --> 05:41.720
Global is this means that the earth or just goes to space.

05:41.990 --> 05:43.400
I believe it goes the space.

05:43.400 --> 05:45.260
It's a global open system.

05:45.260 --> 05:46.820
Communication is everywhere.

05:47.180 --> 05:53.330
Just understanding of that is really powerful because imagine you have to build a different application

05:53.330 --> 05:56.900
to work on the light because it's all different mediums, right?

05:57.320 --> 06:00.500
So like, how would you expect the application to be the same?

06:01.040 --> 06:02.490
You have to have a standard.

06:02.510 --> 06:09.620
Otherwise the application was, Oh, I'm talking to this fiber, this is how I need to convert my bits

06:09.620 --> 06:11.120
to light signal.

06:11.360 --> 06:12.650
Or This is radio wave.

06:12.650 --> 06:14.310
I have to do this to do radio.

06:14.720 --> 06:18.440
But I just wanted to explain this because this is really taken for granted.

06:18.560 --> 06:22.310
But people, smart people, build this so that we don't have to worry about it.

06:22.850 --> 06:23.600
Back to this slides.

06:25.950 --> 06:27.510
Network equipment management.

06:27.870 --> 06:30.000
Without a standard model, you know?

06:31.550 --> 06:35.270
Without a standard model, upgrading network equipment becomes very difficult.

06:35.720 --> 06:36.620
You know, now.

06:37.550 --> 06:43.310
If every equipment has a different standard, then you cannot move on.

06:43.640 --> 06:48.890
You know, you you you will have different models and different things that communicate with each other.

06:49.610 --> 06:51.740
First of all, they won't be able to communicate with each other.

06:51.950 --> 06:55.010
This router won't be able to talk to this author because there is no standard.

06:55.010 --> 06:55.250
Right.

06:55.700 --> 06:57.470
And the beauty of this here is.

06:58.560 --> 07:05.130
Regardless of the underlining medium, you can upgrade the actual network because it is completely decoupled

07:05.490 --> 07:08.190
from the actual medium itself.

07:08.200 --> 07:14.280
So there is there is nothing that we can really what would you have to worry about?

07:14.430 --> 07:20.850
The underlining medium, you can just upgrade the equipment normally and whatever you bring in, we'll

07:20.850 --> 07:26.970
just support it, you know, as long as we know how to talk to it, you know, it's decoupled for innovation.

07:26.970 --> 07:28.440
You know, that's what we talked about in a minute.

07:28.440 --> 07:33.000
Innovation can be done in each layer separately without affecting the rest of the module.

07:33.480 --> 07:33.800
Yeah.

07:33.810 --> 07:36.840
And that's that's very, very critical as well.

07:37.260 --> 07:39.060
And we're going to talk about the layers in a minute.

07:39.060 --> 07:49.800
But each layer is built this way because each layer you can innovate and improve each layer alone.

07:49.920 --> 07:53.280
You know, this is a little bit vague now, but it's going to be clear in a minute.

07:53.460 --> 07:56.460
You know, you can improve the physical layer because that's the medium.

07:56.460 --> 07:57.510
You know, that's the radio.

07:58.530 --> 08:02.400
You can if someone invented something faster than fiber, I don't think you can.

08:02.670 --> 08:03.960
There's nothing faster than light.

08:03.960 --> 08:05.040
But you get my point.

08:05.040 --> 08:06.540
Yeah, it's like more efficient.

08:06.900 --> 08:11.220
Then we'll just build the interface for, then we'll go support it, you know?

08:12.120 --> 08:12.450
Right.

08:12.450 --> 08:14.250
And layer two has nothing to do with.

08:14.250 --> 08:18.450
It's just a layer two will pass into bits and the convergence will happen in the physical layer, you

08:18.450 --> 08:23.220
know, layer three, which is the I believe it cares about this stuff.

08:23.220 --> 08:30.300
If you want to add more content or more headers, it can be added of a layer layer too, you know,

08:30.840 --> 08:33.420
although this will break other stuff at the end of the day.

08:33.420 --> 08:35.310
But that's another topic.

08:35.460 --> 08:42.840
You know, just you cannot just increase the header because there is something called the protocol ossification,

08:42.840 --> 08:48.720
which is all these protocols, all these routers in the middle actually understand how to read things

08:48.720 --> 08:49.410
in a way.

08:49.590 --> 08:52.140
And if the sink change, they freak out.

08:52.470 --> 08:53.460
We'll talk about this in a bit.

08:53.460 --> 08:55.860
Actually, I'll have to remember to add a lecture.

08:55.860 --> 08:57.030
Just talk about a protocol.

08:57.030 --> 08:58.710
Ossification, a very critical concept.

08:59.670 --> 09:00.540
What is those?

09:00.540 --> 09:03.600
I model seven layers each.

09:03.600 --> 09:11.670
Describe a specific network component right layer seven the application that's what you even that can

09:11.670 --> 09:17.070
induce even they don't and they don't really interact with they are seven directly.

09:17.070 --> 09:18.960
It's usually above the application.

09:19.650 --> 09:28.170
When you look at layer seven two, a network engineer, that's just data coming in, you know, but

09:28.170 --> 09:33.180
to a back, an engineer there are they are using different libraries are listening.

09:33.180 --> 09:38.850
They're sending packages in the packets, they're using maybe a jar PC, you know, protocol or certain

09:38.850 --> 09:45.960
protocol that sits on top of FDB to which, which, which, which creates more and more packets, you

09:45.960 --> 09:46.110
know.

09:46.410 --> 09:52.830
But that's the application and that's really what, what really critical here the application is, is

09:52.830 --> 09:57.690
really huge here and everyone is looking just at that layer differently.

09:57.990 --> 10:05.160
But to us, anything above, you know, effectively the the SDP is the application, you know, or a

10:05.160 --> 10:06.300
FTP or GRB.

10:06.300 --> 10:11.940
See anything, you add this layer, this is the actual application layer six, the presentation layer

10:11.940 --> 10:13.290
encode serialization.

10:13.290 --> 10:21.630
Ever send a Jason right through fetch or Axios that's the JSON need to be serialized from this JSON

10:21.630 --> 10:22.050
object.

10:22.050 --> 10:27.870
If your JavaScript or Python, if you're if you're like a bunch of arrays or that data structure down

10:27.870 --> 10:31.260
to a string and this is happening on layer six.

10:32.160 --> 10:35.970
While you shouldn't care about this, this is already happening for you.

10:36.180 --> 10:39.240
So it's little bit a step down from will application.

10:39.240 --> 10:45.060
Your application sends a whole object, but the conversion of the encoding happens there to serialization.

10:45.360 --> 10:51.930
Oh, this is a UTF eight whatever lets encoded so that under leave layer does the job.

10:52.680 --> 10:58.050
That's why talking about this stuff is like you might say, wait a minute, say who cares, right?

10:58.560 --> 10:58.900
Right.

10:58.950 --> 11:00.300
You might say, who cares?

11:00.300 --> 11:02.850
Like about encoding and serialization.

11:02.850 --> 11:06.150
This is happening in my application and that's what people are frustrated about.

11:06.150 --> 11:13.470
The was model people is like really you really need to break this that fine of a level of a detail I

11:13.470 --> 11:19.890
don't care you know sometimes this is one of the and that presentation layer and also the session layer

11:20.070 --> 11:24.180
at some cases you know, that's why it this TCP IP model kind of simplifies this.

11:24.570 --> 11:27.690
But I still prefer the all time model just in if.

11:27.690 --> 11:28.060
Why?

11:28.350 --> 11:30.750
Because we're used to it, you know, back to the slides.

11:33.420 --> 11:33.630
So.

11:33.630 --> 11:33.960
Yeah.

11:35.170 --> 11:36.490
So that's the presentation layer.

11:37.270 --> 11:39.550
Then we have the session layer.

11:39.790 --> 11:46.180
You know, the session layer is where TLC happen, you know, where connection establishing a moment

11:46.300 --> 11:52.630
where state effectively sets place, you know, where you store a state in the client, you know, where

11:52.630 --> 11:53.560
you state, state.

11:53.560 --> 11:54.850
It's not a state in the server.

11:54.940 --> 11:58.450
That's why some protocols called stateful, you know, there's state less.

11:58.600 --> 12:02.770
DTP doesn't have a session layer because it's a it's a stateless protocol.

12:02.800 --> 12:06.100
You know, while TCP, it is a state for protocol.

12:06.280 --> 12:12.160
You store a state on the server and a state on the client and you manage a session effectively.

12:12.340 --> 12:20.470
And if this session is destroyed effectively, either you can restart that connection or invalidate.

12:20.470 --> 12:22.780
So the session layer effectively checks that.

12:22.930 --> 12:28.270
Again, a lot of people says, hey, really, really you want.

12:29.810 --> 12:31.820
It's like really session layer, really.

12:31.820 --> 12:33.920
You need a whole layer just to talk about session.

12:34.220 --> 12:35.980
Believe me, this session is actually this.

12:35.990 --> 12:37.970
This layer is actually important.

12:38.450 --> 12:46.700
A lot of proxies like Linker D, I believe, actually built logic only at the session layer, only at

12:46.700 --> 12:48.380
the connection establishment.

12:48.380 --> 12:50.120
They would do certain logic.

12:50.120 --> 12:58.190
So their application is a layer five app, you know, because they capture a connection and save it

12:58.190 --> 12:59.900
or do pooling about it, you know.

13:00.350 --> 13:02.000
So that is a layer five app.

13:02.000 --> 13:02.600
That's what it means.

13:02.600 --> 13:04.460
Like your application is layer seven.

13:04.550 --> 13:06.230
Well, this is a layer seven proxy.

13:06.260 --> 13:07.640
This is a layer for a proxy.

13:08.030 --> 13:09.110
They talk about this in a minute.

13:11.390 --> 13:11.840
All right.

13:12.680 --> 13:15.590
Transport one of the most important one.

13:16.580 --> 13:20.660
Let's be honest, layer four and layer seven has a back engineer.

13:21.260 --> 13:25.310
That is the only two things that you're going to worry about most of the time.

13:26.060 --> 13:33.020
Hey, maybe if you go and a little bit of DevOps, see, you're going to care about layer three and

13:33.020 --> 13:33.710
layer two.

13:34.190 --> 13:39.650
When you build like BRP sessions and work with Keep Alive and stuff like that, we're going to worry

13:39.650 --> 13:42.650
about this, but we live here, baby.

13:42.650 --> 13:44.420
We live in layer four and layer seven.

13:44.420 --> 13:50.150
Most of the time we build layer four, we configure doesn't necessarily be building, but we configure

13:50.150 --> 13:52.220
our application to be a layer four app.

13:52.700 --> 13:53.120
Why?

13:53.120 --> 13:53.690
What does that mean?

13:53.930 --> 13:55.580
It means we are aware of the transport.

13:55.730 --> 13:57.410
It means we're aware of the packets.

13:57.770 --> 13:58.130
Right.

13:58.670 --> 14:02.960
They're not go because they they're called segments when it's called DCP and Data Control Corner.

14:02.960 --> 14:04.040
DB All right.

14:04.190 --> 14:06.830
Let's be very specific about these naming in a minute.

14:06.830 --> 14:10.410
You're going to across the course, you're going to you're going to worry about this, understanding

14:10.430 --> 14:11.720
it very clearly.

14:11.720 --> 14:14.060
But this is what it is are effectively TCP UDP.

14:14.060 --> 14:14.330
Right.

14:15.110 --> 14:17.120
Very, very important concept.

14:17.360 --> 14:18.440
The protocols live here.

14:18.710 --> 14:23.990
These are the only two protocols, let's be honest, that are and there aren't any other protocols when

14:23.990 --> 14:24.890
it comes to transport.

14:25.220 --> 14:28.510
Well, you can call count quick as part of it.

14:28.510 --> 14:30.970
There's a very new quick protocol.

14:31.010 --> 14:32.120
The roughly new.

14:32.120 --> 14:33.680
But it's it's a transfer protocol.

14:34.640 --> 14:35.900
But that's pretty much it.

14:35.930 --> 14:39.050
You know, these are the three protocol and everything is built on top of them.

14:39.390 --> 14:47.210
To be built on top of TCP is to be to DCP is to be three quick quick is built on UDP, you know, so

14:47.210 --> 14:50.160
everything is built on either imagery on DCP or to be there.

14:51.200 --> 14:56.900
Anything else you can be fancy and build application directly on the IP, which is layer three, the

14:56.900 --> 15:01.640
IP protocol, the internet protocol here, we don't have a transport concept.

15:02.060 --> 15:06.380
You know, I don't care about the if the packet reaches or not, I'll try my best.

15:06.590 --> 15:09.800
I'll tell you if it's bad, but hey, it's up to you.

15:09.830 --> 15:12.710
It's a network protocol, you know.

15:13.490 --> 15:17.120
It's a packet that destined to an IP.

15:17.480 --> 15:22.820
Here we have visibility to ports, you know, port 80, port 80, 80.

15:22.970 --> 15:25.280
Here we don't know what ports are.

15:26.000 --> 15:29.270
We only know addresses, IP addresses, you know.

15:29.570 --> 15:34.700
So every layer has kind of a beautiful concept introduced with it, you know.

15:34.700 --> 15:41.720
So the IP have the concept of the routing and the IP addresses, which we're going to explain in the

15:41.720 --> 15:42.410
whole section.

15:42.740 --> 15:44.330
So stay tuned.

15:44.390 --> 15:45.770
Beautiful stuff coming.

15:45.890 --> 15:47.150
Beautiful stuff coming.

15:48.770 --> 15:51.950
So layer two, another important concept here.

15:52.190 --> 15:53.870
Layer two is the data link layer.

15:54.080 --> 15:56.660
And we're dealing here with the physical medium.

15:56.660 --> 16:02.000
At the end of the day, physical network addresses, you know, hey, this Wi-Fi has this Mac address.

16:02.000 --> 16:04.130
I want to send a frame to it.

16:04.520 --> 16:06.950
So we're sending a frame in layer two.

16:07.310 --> 16:11.510
And we have we know about we don't know about IP addresses at this layer, nothing.

16:11.780 --> 16:13.460
We only know about MAC addresses.

16:13.700 --> 16:14.630
We only know about.

16:15.630 --> 16:15.980
That's my.

16:16.770 --> 16:23.040
And the protocol that we use like Ethernet, Wi-Fi 802 or whatever it's called, you know, frames we

16:23.040 --> 16:24.510
send frames a layer two.

16:25.080 --> 16:31.440
I'm going to repeat this million times during the course, we send frames in layer two, we send packets

16:31.440 --> 16:39.060
in layer three and we send segment and TCP layer four and we set daylight grams when it comes to UDP,

16:39.240 --> 16:41.190
you know, also called segments.

16:41.190 --> 16:44.160
And for both, you can see with me if this is not correct.

16:45.140 --> 16:45.600
All right.

16:46.560 --> 16:48.090
But yeah, don't don't worry about it.

16:48.090 --> 16:52.410
The terminology of the physical layer, this is the bare metal.

16:52.830 --> 17:01.260
What is what is once you take the frame, how does it transport to the other medium?

17:02.830 --> 17:08.510
Electric signal when it comes to Ethernet is if fiber and light light waves, you know.

17:08.920 --> 17:12.830
Is it radiowaves, you know, wi fi or LTE?

17:13.480 --> 17:15.670
All this stuff, the physical and it is.

17:15.820 --> 17:20.320
When it comes to this is just radio waves at the end of the day or light or electricity.

17:20.710 --> 17:27.610
But eventually someone need to to convert that electric signal back to a layer two frame.

17:28.450 --> 17:36.130
Well, first, it's converted into a bunch of digital 101010 and then converts it back to frame, which

17:36.130 --> 17:41.860
then the frame convert to IP, which then the IP, we take the pieces of the data and we understand

17:41.860 --> 17:45.730
that DCP segment and then we understand that, Oh, do we have a session here?

17:45.730 --> 17:47.050
We need a state in this case.

17:47.440 --> 17:55.840
And do I need to decode, serialize and deliver to the application so you can serve your beautiful HDTV

17:56.020 --> 17:57.160
request, for example?

17:59.000 --> 18:00.530
Here's an example, actually.

18:01.430 --> 18:08.720
From from the point of view of a sender, we're sending a postal request and I specifically to the post

18:08.720 --> 18:16.160
because I need to send body and we cannot send body with get request right so we have to do a post.

18:16.640 --> 18:22.910
So sending a post request to an TPS web page here to be aware of this means that it's encrypted.

18:22.910 --> 18:31.130
So there's tools here, but we'll come to that the application post request with the JSON data to actually

18:31.160 --> 18:31.760
be a server.

18:31.790 --> 18:34.340
That's the that's what that application does.

18:34.580 --> 18:42.530
So it you use Axios or you use Fetch or you use your Python request library and we send our post request

18:42.740 --> 18:46.220
with this blob of Jason and said, Hey, send it.

18:47.250 --> 18:53.780
The presentation here takes your JSON object, which is just the object here and serialize it to flat

18:53.780 --> 18:54.500
bytes things.

18:55.130 --> 18:59.180
Right, because you're going to send an object doesn't mean anything, right?

18:59.240 --> 19:02.420
The object is meaningful in your language only.

19:02.900 --> 19:03.830
Yeah, it does.

19:03.830 --> 19:06.680
It doesn't mean anything when it comes to it's a string.

19:06.680 --> 19:08.180
You need to convert it to bytes.

19:08.630 --> 19:08.960
Right.

19:09.260 --> 19:12.590
And shove this bytes as a bunch of data here.

19:12.920 --> 19:16.460
So now we have this JSON and we have the protocol, we have other stuff as well.

19:16.460 --> 19:18.470
Information the session here.

19:19.250 --> 19:21.140
Do I need to establish a DC connection?

19:21.140 --> 19:22.460
Do I need to establish deals?

19:22.460 --> 19:23.390
Yes and yes.

19:23.390 --> 19:24.140
Yes and yes.

19:24.440 --> 19:27.170
We establish that ECB connection because we need to communicate.

19:27.170 --> 19:28.940
We're going to explain all this beautiful stuff.

19:29.150 --> 19:34.190
We're going to explain how this large DCP connection, what is DLLs really mean here in a minute.

19:34.370 --> 19:34.640
Right.

19:34.880 --> 19:40.220
So the encryption that happens, so we have this is what happened in session where you need to start

19:40.220 --> 19:45.680
a state transport, send the Syn request target port four, four, three.

19:45.680 --> 19:49.300
So that's the actual first thing that we send, right?

19:49.610 --> 19:55.880
This is a direct command from session layer because to establish a connection you need to send the send

19:56.060 --> 19:57.310
ciac ack.

19:57.320 --> 19:57.590
Right.

19:57.590 --> 19:58.340
We're going to talk about this.

19:58.340 --> 20:01.400
Don't worry if it's confusing, but but don't say that.

20:01.400 --> 20:03.620
It, it send just the send request.

20:03.740 --> 20:04.790
We're paused here.

20:04.790 --> 20:10.520
The JSON doesn't go away, doesn't go to the other party because we don't have a connection yet.

20:10.790 --> 20:16.460
So you establish a connection, you receive a connection request, then you authenticate and then you

20:16.460 --> 20:17.300
send the data here.

20:17.900 --> 20:22.550
But let's just say I'm just sending the send request for a minute here.

20:23.510 --> 20:26.000
This then is sent to port four, four, three.

20:26.000 --> 20:26.270
Why?

20:26.270 --> 20:28.490
Because the transport understand what ports are.

20:28.820 --> 20:29.120
Why?

20:29.120 --> 20:29.840
Four, four, three.

20:30.020 --> 20:32.120
Well, you said PDBs and that's the default port.

20:32.120 --> 20:37.640
Four, four, four, three, we understand four, four, three as the port for this and then network

20:38.420 --> 20:45.710
the network layer which is we we shove that send request which is the segment down to an IP packet and

20:45.710 --> 20:47.600
add the source and destination IP.

20:47.900 --> 20:52.070
So if you need the IP address, you need to do a DNS to get the IP address.

20:52.070 --> 20:54.860
And once you get the IP address, we shove it into this packet.

20:55.150 --> 20:58.970
Well, don't worry, we're going to have a beautiful diagram to explain all that stuff.

20:59.210 --> 21:05.270
But data link goes each packet goes into a single frame and as the source and destination mechanism.

21:05.270 --> 21:07.730
So we need to figure out the Mac as well.

21:08.030 --> 21:09.770
That's ARP going to go on it.

21:10.580 --> 21:15.830
Each frame becomes a string of bits and the physical layer just 10101010.

21:16.100 --> 21:24.230
These one zeros are converted into this radio signal or electricity now or light and then that's it.

21:24.800 --> 21:26.180
And take this with a grain of salt.

21:26.540 --> 21:32.030
Whatever we explain here doesn't have to be clear cut and dry, as they say.

21:32.030 --> 21:34.910
You know, some layers can inherit from each other.

21:34.910 --> 21:37.820
I'm doing stuff at the end of the human build.

21:37.820 --> 21:42.890
This, you know, nothing is just whole layer for layer five.

21:42.890 --> 21:44.660
You can argue about all any of that stuff.

21:46.100 --> 21:47.510
Receiver What does the receiver do?

21:47.900 --> 21:51.080
The receiver will receive the physical layer first, right?

21:51.170 --> 21:55.250
So we received a bunch of radio or electrical light, right?

21:55.820 --> 22:00.470
Because your server might be on fiber, but your network, you can have send that from Wi-Fi.

22:00.770 --> 22:02.060
See the beauty guys.

22:02.270 --> 22:03.530
Do you see the beauty of this?

22:03.980 --> 22:06.500
I can send your data from Wi-Fi.

22:06.860 --> 22:07.280
Right?

22:07.610 --> 22:09.350
And then you receive it through fiber.

22:10.490 --> 22:14.810
You might say, duh, but I absolutely appreciate this.

22:17.140 --> 22:23.080
So now the physical layer at the receiver side converters, the digital bits and then the data link.

22:23.080 --> 22:28.420
Okay, all the bits from layer one are assembled and the frames, the frames from layer two are simple

22:28.420 --> 22:29.350
to enable a packet.

22:29.620 --> 22:30.790
Oh now IP packet.

22:30.790 --> 22:33.580
I know that the destination IP is this for me.

22:33.850 --> 22:34.810
Yes, it is.

22:34.810 --> 22:35.230
Right.

22:35.530 --> 22:38.230
And every letter, by the way, asked the same question as well.

22:38.230 --> 22:40.960
I'm going to come to that like is this packet for me.

22:41.680 --> 22:46.330
So the transport, the IP packets from layer three on a symbol into TCP segments, you know.

22:47.260 --> 22:47.560
All right.

22:47.740 --> 22:53.050
And then this is what congestion controls, the flow control then through your transmission and it is

22:53.050 --> 22:55.360
this the the thick was this the rice packet?

22:55.360 --> 22:56.830
Is this the old packet?

22:56.830 --> 22:59.860
Is this a new and going to order all that stuff?

23:00.460 --> 23:05.590
If it's a segment that is a sin, we don't need to go any further into more layers as we are still processing

23:05.590 --> 23:06.520
the connection request.

23:06.730 --> 23:08.680
Here's the beauty, right?

23:08.890 --> 23:11.980
Since it's the connection request, we don't really go down.

23:12.220 --> 23:14.530
There's no point to go down to the session layer.

23:14.530 --> 23:18.340
Well, we have to go to the session layer here to establish that connection.

23:18.610 --> 23:23.980
And once we have the connection, we're going to have our Jason back in this next request and then we're

23:23.980 --> 23:26.680
going to go all the way to that connection here.

23:26.770 --> 23:28.660
And then we're going to go to the DC area.

23:28.660 --> 23:35.470
We're going to do the presentation layer DC rules that fly by string Jason back to the Jason object

23:35.710 --> 23:37.150
for the app to consume.

23:37.420 --> 23:43.840
And this serialization here could be completely different from the serialization that happened on the

23:44.140 --> 23:53.080
client because you can just, you can serialize from JavaScript but serialized into Python or you can

23:53.200 --> 23:59.530
serialize from C-sharp and disk realize into go, you know, it doesn't matter.

23:59.860 --> 24:01.410
And that's where your logic is.

24:01.420 --> 24:05.770
That's why a lot of people say really the presentation application layer is just the application, to

24:05.770 --> 24:10.000
be honest, like this is the application, my application is doing this logic at the end of the day,

24:10.510 --> 24:11.590
and you can argue with that.

24:11.590 --> 24:14.020
Of course, again, take it with a grain of salt.

24:14.440 --> 24:21.250
The application understand that JSON post requests and it says, hey, your express JSON or Apache request

24:21.310 --> 24:26.530
at the end of the received the event and it will trigger that event which says, Hey, someone just

24:26.530 --> 24:27.700
sent you a post request.

24:27.760 --> 24:28.750
What do you want to do with it?

24:28.750 --> 24:31.290
That function that will get called it will be triggered.

24:31.300 --> 24:32.800
Say, Hey, someone just sent your request.

24:33.130 --> 24:39.060
You can consume the request, go to the database, do something and then get back synchronously in the

24:39.310 --> 24:41.920
response back to the client.

24:42.430 --> 24:45.250
All right, finally some diagrams.

24:45.820 --> 24:47.650
So this diagram took me a while to build.

24:47.650 --> 24:48.760
Let's see if you guys like it.

24:49.600 --> 24:50.980
So the first thing client.

24:51.280 --> 24:58.360
So the client and server notice the arrow were going down or going up them is the client is the sender

24:58.360 --> 25:00.850
in this case and the server is the receiver.

25:01.270 --> 25:03.760
Does it mean that the server doesn't send data?

25:03.760 --> 25:06.010
It also can absolutely send data.

25:06.730 --> 25:09.760
So the application layer goes to the presentation.

25:09.760 --> 25:13.930
We talk about it serialization, decoding, encoding.

25:13.930 --> 25:20.380
All this shows such an layer establishing a connection, whether this deals or or the handshake itself,

25:20.380 --> 25:28.150
the TCP handshake establishes the concept of a connection, a stateful thing, then transport actually

25:28.150 --> 25:34.990
working with a TCP flow control in the ports and all that jazz, you know, the actual segments go down

25:34.990 --> 25:36.610
network, right?

25:36.970 --> 25:39.940
The IP packets itself go down data length.

25:39.940 --> 25:40.570
This is yellow.

25:40.570 --> 25:41.020
This orange.

25:41.020 --> 25:41.860
I don't know if it's clear.

25:41.860 --> 25:42.700
Hopefully it's clear.

25:43.630 --> 25:43.930
Hopefully.

25:43.930 --> 25:48.940
I don't regret the choice of these colors, you know, the physical layer, which is the actual medium.

25:49.150 --> 25:51.130
And then we send it and I chose the waves.

25:51.370 --> 25:57.130
In this case, the server receives that we received the first and from the physical medium because that's

25:57.130 --> 26:02.410
how you receive things, you know, the lowest layer your network card receives this signal and then

26:02.410 --> 26:06.430
convert it to the data link and then convert it back to the IP address.

26:06.520 --> 26:13.000
No IP packets all the way transport and then session, you know, go to the presentation and go all

26:13.000 --> 26:14.800
the replica so you just dirt.

26:15.520 --> 26:16.330
You see them all right.

26:17.920 --> 26:19.450
And then go all the way up.

26:19.840 --> 26:20.470
It's like this.

26:20.650 --> 26:21.370
It's you.

26:22.620 --> 26:22.860
Now.

26:22.860 --> 26:23.690
Let's go, dirt.

26:24.480 --> 26:29.070
The question is, do I have to always go through all these layers?

26:29.280 --> 26:30.210
Absolutely not.

26:30.630 --> 26:31.620
I'll give you an example.

26:32.370 --> 26:35.160
If you if you send a TCP.

26:36.780 --> 26:37.530
No, let's go.

26:38.340 --> 26:39.990
I'm sending initiative request.

26:39.990 --> 26:41.880
But I need to establish a new connection.

26:42.420 --> 26:44.180
Well, the application sends the request.

26:44.190 --> 26:48.840
You know, the presentation does the Jason thing, the session pauses the presentation.

26:48.840 --> 26:51.060
They say, wait a minute, session.

26:51.690 --> 26:52.940
I don't have a session here.

26:52.950 --> 26:53.790
What are you talking about?

26:53.940 --> 26:54.930
Let me create a session.

26:54.930 --> 26:55.500
Wait for me.

26:56.040 --> 26:56.640
Wait a minute.

26:56.640 --> 26:58.410
Just let me create a session real quick.

26:58.890 --> 27:02.220
So we go send the cynical two, two, two, two, two, two.

27:02.220 --> 27:05.520
To that we send that send request to create a connection.

27:05.910 --> 27:07.170
Goes all the way here.

27:07.170 --> 27:08.530
You seeing this point there?

27:08.650 --> 27:09.950
This is important to see the point.

27:09.960 --> 27:11.310
Otherwise the whole thing is pointless.

27:11.850 --> 27:14.280
You see, go out and reach the session.

27:14.280 --> 27:14.730
Okay.

27:14.730 --> 27:15.360
I agree.

27:15.510 --> 27:16.530
I'm going to create a connection.

27:17.070 --> 27:17.850
We don't go up.

27:18.210 --> 27:18.750
We don't.

27:19.350 --> 27:20.070
There's no point.

27:20.070 --> 27:21.150
There's no application yet.

27:22.070 --> 27:27.750
This is just a request to send a request to send a connection here to establish a connection.

27:28.020 --> 27:29.250
And then we establish this.

27:29.250 --> 27:29.490
Okay.

27:29.520 --> 27:33.020
Snack, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb, bomb.

27:33.060 --> 27:34.260
Go back is sent.

27:34.710 --> 27:35.040
Okay.

27:35.190 --> 27:35.490
Okay.

27:35.610 --> 27:43.890
If you were a snack and let me finally do NEC two, two, two to go back and then boom, stop here session.

27:44.100 --> 27:46.200
Now we have a full connection.

27:46.860 --> 27:53.910
Now the session will say, okay, now that we sent the EC, you may unlock and go further.

27:54.390 --> 27:55.350
All right, you have it now.

27:55.350 --> 27:56.580
A session continue.

27:56.730 --> 27:57.630
Remember the pause.

27:57.630 --> 27:59.910
JSON request is now resumed.

28:00.660 --> 28:03.390
Go to the transport layer or element, put it in a segment.

28:03.390 --> 28:09.570
This is you put your bytes strong JSON into the transport layer, shove it into an IP packet, determine

28:09.570 --> 28:15.030
the IP, address the destination shovel and do the data link, determine the MAC address.

28:15.150 --> 28:20.430
Obviously we already determined all that stuff in the handshake, but I'm just explaining here again

28:20.670 --> 28:21.600
and then send that.

28:21.600 --> 28:27.960
Then send the physical layer, draw all the data, transport, transport all the way, go to transport

28:27.960 --> 28:28.230
layer.

28:28.230 --> 28:28.920
You have a session.

28:28.920 --> 28:29.640
Yes, you do.

28:29.910 --> 28:30.690
Presentation layer.

28:30.690 --> 28:31.290
What do I do?

28:31.290 --> 28:32.640
I have the beautiful JSON.

28:32.790 --> 28:35.880
I have all this data and this could be a single.

28:36.790 --> 28:40.420
Packet or a segment, if you will, or multiples.

28:40.660 --> 28:47.770
So this will do the assemblage will assemble all the packets that necessary and then deliver one huge

28:48.220 --> 28:54.940
string to the presentation layer which will decode it or this realize it, go back to application and

28:55.330 --> 28:59.530
all of a sudden you just triggered that lesson.

28:59.890 --> 29:06.600
Uh, you know what the reason was called the post writer, if you will, if you're using express j j

29:06.700 --> 29:10.570
as here, just that now it's trigger.

29:10.570 --> 29:12.100
So look at the work.

29:13.130 --> 29:17.240
That is happening, guys, and that is the purpose of this course.

29:17.600 --> 29:20.060
Understand what is happening.

29:20.360 --> 29:23.400
And there is beauty of of understanding.

29:24.290 --> 29:26.840
I don't know what that means, but you get the point.

29:27.830 --> 29:28.130
All right.

29:28.250 --> 29:29.690
So this is a segment.

29:30.230 --> 29:30.950
This is the package.

29:31.460 --> 29:34.790
And there's a phrase I'm going to repeat that million times on daily.

29:35.030 --> 29:38.990
This is a hammered frame packet segment that is critical to understand.

29:39.380 --> 29:41.630
This is another view that I like to do.

29:41.630 --> 29:42.320
I personally do.

29:42.340 --> 29:45.060
I never seen anyone do something like this before.

29:45.590 --> 29:47.950
I just this is how I understand it.

29:48.470 --> 29:52.260
It not necessarily this hour looks like in the wire.

29:52.280 --> 29:56.540
You know, if you well or this is how I will look, I look at this.

29:56.720 --> 29:58.670
This is the Russian matryoshka.

29:58.730 --> 30:01.490
If you are aware of this, this doll's inside a doll.

30:01.700 --> 30:04.970
This is exactly what I as I'm all you application.

30:05.180 --> 30:10.610
You go to the presentation layer, go to the session layer, and the content here goes into a TCP segment.

30:10.610 --> 30:15.770
You add a destination port and a source port left and right, but not necessarily left and right.

30:15.970 --> 30:17.720
It's just literally at the end.

30:18.170 --> 30:20.810
But I like it to do it this way because I understand it better.

30:21.500 --> 30:28.340
And then this this green segment shoves into an IP packet and that IP packet.

30:28.430 --> 30:34.820
Now we have to add the destination IP address and the source IP address and then the whole IP packet

30:34.820 --> 30:39.950
gets shoved in into a frame and boy, it benefits and off frame.

30:40.130 --> 30:44.000
And we're going to talk about the frame size, of course, called an empty you maximum transmission

30:44.000 --> 30:44.230
unit.

30:44.240 --> 30:52.460
You cannot put an IP ad IP packet into multiple frames unless you fragment, which is something we're

30:52.460 --> 30:53.570
going to talk about in the future.

30:54.110 --> 30:58.070
Destination Mac and the source Mac, you pour that and then the whole thing becomes registered with

30:58.070 --> 31:01.700
thread blob of radio signals and we're going to do the same thing.

31:02.120 --> 31:02.450
Hey.

31:03.540 --> 31:06.510
Get the bets right from the physical layer.

31:07.390 --> 31:13.360
Understand where the frames start, where the frame ends, because that's what the physical layer does.

31:14.200 --> 31:15.650
And actually, they are to death.

31:15.650 --> 31:16.960
Healing does that for you.

31:17.320 --> 31:20.980
And now, hey, we have the Mac address here.

31:21.520 --> 31:22.090
We had the source.

31:22.090 --> 31:25.550
Mac, take the data portion of this frame.

31:26.230 --> 31:28.690
That becomes the IP packet.

31:28.870 --> 31:30.640
Hey, there's the destination IP.

31:30.700 --> 31:31.570
This is also IP.

31:32.140 --> 31:33.280
Here, you don't see this.

31:33.280 --> 31:37.120
This is shove the heat down into that frame, right?

31:37.360 --> 31:38.410
You have to unpack it.

31:38.740 --> 31:41.830
That unpacking takes a finite amount of time.

31:42.220 --> 31:47.860
If you nanoseconds, if you will, you know, just understand this nanosecond time that is critical.

31:48.280 --> 31:49.510
So move up.

31:49.960 --> 31:51.220
Take that IP packet.

31:51.580 --> 31:52.060
What do we do?

31:52.060 --> 31:52.660
The IP packet.

31:53.020 --> 31:54.480
Hey, destination IP is a for me.

31:54.490 --> 31:54.880
Yes.

31:55.120 --> 31:55.900
Take that segment.

31:56.560 --> 31:57.040
What do we lose?

31:57.040 --> 31:57.490
A segment?

32:00.780 --> 32:05.550
And back at there is a segment destination port surfboard, which application this is destined to.

32:06.030 --> 32:07.710
There are thousands of port here.

32:08.130 --> 32:09.600
Oh, you want this port?

32:09.630 --> 32:09.960
Okay.

32:10.590 --> 32:16.770
Let me deliver that segment to that application, to that process.

32:17.730 --> 32:20.570
Because based on the port, you going to deliver this way, right.

32:20.940 --> 32:22.860
And this is something we're also going to explain.

32:22.950 --> 32:26.130
Now, each port is technically one process is one port.

32:26.580 --> 32:30.300
This can change, obviously, but this is just a general rule of thumb.

32:31.650 --> 32:33.840
And then we understand, do I have a connection?

32:33.870 --> 32:34.500
Yes, we do.

32:35.190 --> 32:36.000
Do I need to do anything?

32:36.000 --> 32:36.960
The presentation layer?

32:36.990 --> 32:37.380
Nope.

32:37.650 --> 32:38.520
Do I have to do anything?

32:38.520 --> 32:41.970
I application here and we deliver the app effectively.

32:42.540 --> 32:44.850
Here's another slide that is very important to understand.

32:45.990 --> 32:49.290
You want to say that the client is not directly connected to the server, right?

32:49.560 --> 32:50.160
This is the client.

32:50.190 --> 32:50.880
This is over.

32:51.190 --> 32:52.650
There are switches in the middle.

32:52.900 --> 32:53.970
Those are outers.

32:54.120 --> 32:55.320
They're not proxies.

32:55.320 --> 32:56.540
The A ends.

32:56.790 --> 32:58.080
That is reverse proxies.

32:58.410 --> 32:59.820
You know those load balancers?

33:00.450 --> 33:03.360
What are those suckers doing in the middle?

33:03.960 --> 33:08.370
They look they peek the content.

33:09.270 --> 33:13.920
And when they peek at the content, they take a finite amount of time because they make decisions based

33:13.920 --> 33:14.490
on this.

33:15.330 --> 33:15.900
Of the data.

33:16.500 --> 33:16.770
All right.

33:16.770 --> 33:22.230
So let's go through an example where a client want to talk to a server, but it goes to a square generator.

33:22.410 --> 33:22.680
Right.

33:23.370 --> 33:25.510
So the client will send information as usual.

33:25.530 --> 33:30.150
You know, the client was in information as usual to go through the application presentation session,

33:30.150 --> 33:32.580
transport network data and their physical.

33:32.610 --> 33:33.710
And then we'll send.

33:33.750 --> 33:34.050
Right.

33:34.350 --> 33:40.110
The first thing you might hit in your organization, maybe switch the switch connects different substance

33:40.110 --> 33:40.650
together.

33:40.650 --> 33:42.810
You know, hey, this is the network.

33:42.810 --> 33:45.420
This is a subnet where this is happening the way I want to connect them together.

33:45.720 --> 33:52.210
And I don't want data to be sent unnecessarily to a different network.

33:52.290 --> 33:54.270
You know, that's the power of the switch.

33:54.270 --> 34:01.230
You know, it understands where to send the data based on the frame itself, based on the Mac address.

34:01.260 --> 34:01.770
That's the trick.

34:01.770 --> 34:05.280
It does like, oh, this computer's connected to this port, you know.

34:05.550 --> 34:08.000
So the Mac address of that is this.

34:08.000 --> 34:13.620
So it goes to this board, you know, so it doesn't necessarily unlike a hub, for example, where just

34:13.800 --> 34:21.300
literally the hub broadcasts that the data to every single port, which is a lot that is a lot of bandwidth

34:21.300 --> 34:21.980
wastage there.

34:21.990 --> 34:24.600
But the switch to do its job.

34:24.930 --> 34:30.060
It needs to look at the Mac addresses because that's how it does its lookup.

34:30.960 --> 34:34.050
So it only be to take the physical layer.

34:34.440 --> 34:35.910
Convert that to data link.

34:36.000 --> 34:37.080
Look at the frames.

34:37.980 --> 34:40.650
Look at the destination Mac address.

34:41.040 --> 34:42.450
And then that's it.

34:43.110 --> 34:46.320
It doesn't need the IP addresses mod, so it's more to most.

34:46.320 --> 34:47.490
The switches don't.

34:47.760 --> 34:48.900
But some do.

34:49.680 --> 34:50.880
But most switches.

34:51.060 --> 34:52.140
Just look at layer two.

34:52.440 --> 34:53.280
That's it.

34:53.520 --> 34:55.830
And then once it does, it is like, Oh, I'm done.

34:56.800 --> 34:59.980
And then sends that data to their next sports.

34:59.980 --> 35:00.280
Right.

35:00.310 --> 35:05.650
So it does it does re transmit the data, if you think about it here.

35:06.160 --> 35:08.490
Well, now let's go through our router.

35:08.680 --> 35:10.180
The router will do the same thing.

35:10.480 --> 35:12.040
The router will need the physical layer.

35:12.040 --> 35:13.960
Obviously, we'll go to the data link.

35:13.960 --> 35:18.040
It will sometimes act like a switch if you're sending to the same subnet.

35:18.580 --> 35:27.280
But the most important thing, routers need to run out and routers need the IP addresses and order out.

35:27.760 --> 35:30.370
So it needs to go up to layer three.

35:31.440 --> 35:32.330
To root.

35:32.610 --> 35:33.480
That's why it's out.

35:33.480 --> 35:39.420
There is a layer three device while the switch is a layer two device.

35:39.840 --> 35:42.480
Very critical concept to understand.

35:42.690 --> 35:48.210
So you go up two and then go down and then rather goes all the way to layer three and then go down.

35:48.720 --> 35:53.340
And then until you reach the application, you might go to multiple routers and we go up to layer three

35:53.340 --> 35:58.860
and go down up to the area and go down underneath the application where we go all the way to application

35:58.860 --> 35:59.640
if necessary.

35:59.640 --> 36:04.050
Again, because sometimes you're establishing your connection or you want only to go to the layer session,

36:04.470 --> 36:10.020
the session layer, or sometimes the, the packet is invalid and we'll it will fail right here today.

36:10.020 --> 36:10.920
You don't have a connection.

36:10.920 --> 36:12.810
Why you me sending me data with a connection?

36:13.140 --> 36:16.020
You know, that's the TCP idea effectively.

36:16.060 --> 36:21.480
So that's why UDP doesn't really have a concept of a session layer if you think about it might be wrong

36:21.480 --> 36:24.660
there, but if you think about it, there's no state and UDP.

36:24.660 --> 36:25.770
UDP is stateless.

36:25.890 --> 36:27.720
You just send data and there's that.

36:28.350 --> 36:29.280
There is no state.

36:29.970 --> 36:32.850
But that's that's a very critical concept as well.

36:34.350 --> 36:37.560
My favorite let's add a firewall.

36:37.590 --> 36:39.240
Let's add a layer for proxy.

36:39.390 --> 36:42.420
Let's add a seed in content manager content delivery network.

36:42.750 --> 36:45.510
So a firewall, guys, what does a firewall do?

36:47.260 --> 36:56.770
FARA blocks certain applications from sending data or blocks and blocks 13 unwanted packets to come

36:56.770 --> 36:58.210
through your network.

36:59.360 --> 37:02.060
And in order to do that, it needs to look at the IP address.

37:04.080 --> 37:05.850
It needs to look at the ports.

37:06.660 --> 37:14.310
That's why the at least the ports, some firewalls are are they go all the way and look at the application.

37:14.850 --> 37:17.280
These are the firewalls that look up the here.

37:18.090 --> 37:19.950
They're effectively called transparent firewall.

37:20.430 --> 37:25.710
Transparent by all the transparent proxies really are transparent like your ISP.

37:26.460 --> 37:29.460
Everything up to here is available to everyone.

37:29.460 --> 37:31.470
Everyone can read your ports.

37:31.890 --> 37:34.440
Everyone can read your IP addresses.

37:35.070 --> 37:35.910
That is why.

37:36.950 --> 37:37.910
It's public.

37:38.060 --> 37:38.630
It's not.

37:38.660 --> 37:39.950
It's never encrypted.

37:39.980 --> 37:40.640
Never.

37:40.760 --> 37:41.990
The network openness.

37:41.990 --> 37:42.380
You need.

37:42.650 --> 37:46.770
You need the IP address in order to travel data and the ports.

37:46.790 --> 37:48.170
You need them public as well.

37:48.500 --> 37:48.710
All right.

37:48.710 --> 37:49.820
So these are public.

37:50.150 --> 37:52.700
That's why anyone looking at this, they are called transparent.

37:52.730 --> 37:54.770
Transparent firewall, transparent proxies.

37:54.770 --> 37:58.430
If you ever heard about this, these are proxies that doesn't really change anything.

37:58.440 --> 37:59.510
It's almost like a transplant.

37:59.510 --> 38:00.200
They go through it.

38:00.950 --> 38:05.670
And that's why your ISP can technically block you from going to any website they want.

38:05.690 --> 38:06.830
They don't want you to go there.

38:07.190 --> 38:11.840
A lot of our government uses transparent proxies.

38:12.110 --> 38:16.010
You know, they don't go all the way to the application because if you go to the application, you need

38:16.010 --> 38:16.730
to decrypt.

38:16.970 --> 38:18.830
You need to stop the session and decrypt it.

38:19.370 --> 38:19.670
Right.

38:19.910 --> 38:24.440
And to do that, you need to serve the certificate of the server, which you don't have.

38:24.530 --> 38:24.800
Right.

38:25.010 --> 38:31.550
Unless you're Kazakhstan, which literally forces a certificate into every computer and they're citizens,

38:31.550 --> 38:35.510
you know, to the certificate authority for trusting it.

38:35.960 --> 38:41.450
But most of the world, they're not like that, you know, so they are always in transparent.

38:41.460 --> 38:45.710
The only thing you can do is just block the IP address that you're going to.

38:45.720 --> 38:46.640
You can do that.

38:47.330 --> 38:48.890
All you have to do is just stop.

38:48.890 --> 38:52.610
Don't send the data right, because it goes through you.

38:52.610 --> 38:54.530
And if something goes through, you can stop it.

38:55.010 --> 39:00.290
So the firewall stops that layer for proxy if you want to do the load balancing based on a port.

39:00.710 --> 39:07.340
Hey, if you're going to a port at 80, I want you to rewrite the packet and send it to to this address

39:07.340 --> 39:09.690
instead or send it to this address instead.

39:09.710 --> 39:09.980
Right.

39:10.130 --> 39:15.260
So you can rewrite the packet right here, change it effectively, and then send it somewhere else.

39:16.100 --> 39:19.230
Actually, if you think about it, your ISP can do that too.

39:19.550 --> 39:19.880
Right.

39:19.920 --> 39:22.790
Can't get to can send you somewhere else if you want.

39:22.820 --> 39:30.530
If they want to know anyone, I say your ISP because your ISP is where your first packets go to.

39:31.110 --> 39:31.310
Right.

39:31.310 --> 39:32.930
That's why a lot of people use VPNs.

39:33.620 --> 39:37.100
VPNs effectively.

39:37.130 --> 39:40.770
I didn't add it here, but VPN is actually a layer three protocol if you think about it.

39:41.330 --> 39:45.590
It takes the IP packets and put them in another IP packets.

39:45.620 --> 39:50.480
That's that's a simpler, simpler solution for the IP for the VPNs.

39:50.480 --> 39:55.100
Most Vivian's not doesn't do this, but one solution is to put an IP in an IP.

39:55.370 --> 40:01.220
So I don't care what the content of this IP packet is, it could be an issue request could be a geographic

40:01.250 --> 40:02.510
database because I don't care.

40:02.510 --> 40:03.290
It's an IP.

40:04.010 --> 40:08.330
And that's why AWS, I, I'm one of the really critical, you know, take that and just shove it there

40:08.330 --> 40:09.440
and then send it, you know.

40:10.130 --> 40:14.060
So the VPN is actually a layer three protocol, if you think about it.

40:14.210 --> 40:17.900
Some people actually live in the layer two as well.

40:18.170 --> 40:18.470
No.

40:20.120 --> 40:20.290
So.

40:20.300 --> 40:20.450
Yeah.

40:22.530 --> 40:26.430
Go all the way here as a firewall or a proxy.

40:27.030 --> 40:32.190
But then if you have a load balancer, like a layer seven load balancer, you know.

40:33.260 --> 40:35.330
A few built one as a back injury.

40:35.330 --> 40:42.640
And, you know, like in generics where you want to cache data or you want to balance based on certain

40:43.030 --> 40:50.140
paths, like if I go to slash whatever, slash pictures, right?

40:51.290 --> 40:55.470
Go to this server if you go to slash images.

40:55.490 --> 40:56.510
Pictures are the same thing.

40:56.810 --> 40:58.820
Images, slash, whatever.

40:58.820 --> 40:59.280
Blob.

40:59.300 --> 41:02.030
Go to this set of servers if you want to do that.

41:02.600 --> 41:07.880
The slash, that path is actually an application concept which is encrypted most of the time.

41:08.210 --> 41:09.860
To look at it, you have to decrypt it.

41:10.100 --> 41:17.300
So the Layer seven proxies or content delivery networks or Layer seven, they play at this layer.

41:17.600 --> 41:25.130
That means they decrypt everything you send, look at it, cache it, and then send it.

41:25.130 --> 41:26.630
So they go all the way there.

41:26.990 --> 41:31.010
So they are way slower than the routing or file wise.

41:31.010 --> 41:31.430
Lower.

41:31.760 --> 41:37.400
You go and go all the way up and then re transmit everything back down.

41:37.670 --> 41:44.600
So you effectively know you need a completely different session between this, those two copies, right?

41:44.600 --> 41:49.180
Because this session, this is one session and this is one session.

41:49.190 --> 41:53.960
This is the final endpoint to you as a client.

41:54.020 --> 41:55.550
You're connecting to this.

41:55.550 --> 41:57.800
You know, that's why this is called also a reverse proxy.

41:57.800 --> 42:03.920
You know, where this is your final destination, but your true final destination is actually this back

42:03.920 --> 42:06.110
in server, which you don't know anything about.

42:06.410 --> 42:08.870
That's how Google work and any other application.

42:09.200 --> 42:13.340
When you go to Google, you really don't touch the front end server.

42:13.340 --> 42:14.690
You're just going there.

42:14.960 --> 42:20.870
But the Google server might turn around and send requests to another server on the back end that you

42:20.870 --> 42:24.170
have no idea of, as I call a reverse proxy.

42:24.440 --> 42:30.440
While a proxy goes through, you know, you're sending a request, but you know, the final destination,

42:30.440 --> 42:38.180
you know, you know this is your final destination, but the proxy makes that request on your behalf,

42:38.450 --> 42:38.660
right?

42:38.660 --> 42:39.320
Does that make sense?

42:40.900 --> 42:41.140
All right.

42:41.140 --> 42:43.840
So what are the shortcomings of this Orci model?

42:44.290 --> 42:47.850
What is and what has too many layers which can be hard to comprehend?

42:47.860 --> 42:55.150
And definitely that was my belief and opinions back maybe three years ago.

42:55.600 --> 43:01.830
And I changed my mind ever since then, you know, I really thought I really session and presentation.

43:01.900 --> 43:04.120
I think this this shouldn't really treat as one.

43:04.390 --> 43:10.060
But now the more I understand, the more I build back in application, the more I start to read and

43:10.060 --> 43:10.870
understand.

43:11.320 --> 43:18.410
We really need that low level, you know, breaking down sometimes, you know, not all the time, but

43:18.430 --> 43:20.130
is really hard to argue about which they are.

43:20.140 --> 43:20.860
That's what it's like.

43:21.130 --> 43:25.420
People still argues like all presentation or should only really describes or presentation layer should

43:25.450 --> 43:26.230
really decode.

43:27.160 --> 43:27.910
Okay.

43:28.120 --> 43:28.990
And then do they.

43:30.270 --> 43:33.190
It's all people, you know, speculating of anything.

43:33.330 --> 43:34.890
So it's it's really not funny.

43:35.190 --> 43:38.370
You know, just everybody has an opinion.

43:38.370 --> 43:40.120
It becomes an opinion at the end of the day.

43:40.160 --> 43:40.390
Right.

43:40.590 --> 43:44.310
Because there is no if you look at the computer, there is no they are fi.

43:44.340 --> 43:49.020
You know, it just is not something you will read as something we talk about or our.

43:49.170 --> 43:53.370
So us engineers can talk through things, you know, so similar.

43:53.370 --> 43:55.050
It is definitely simpler to deal with.

43:55.050 --> 43:58.140
They are five, six and seven as just one level, which is the application.

43:58.140 --> 44:01.350
And that's what the the Cppib model does exactly that.

44:02.010 --> 44:03.360
It's much simpler.

44:03.660 --> 44:05.100
It's just the application layer.

44:05.100 --> 44:07.590
Hey, five, six, seven is the application.

44:07.590 --> 44:13.890
I don't care don't, don't complicate things which I, I have mixed feeling about this.

44:13.890 --> 44:14.730
It's up to you.

44:14.730 --> 44:15.000
Really.

44:15.000 --> 44:15.720
What do you think?

44:15.750 --> 44:16.070
But.

44:17.250 --> 44:18.870
Applications on application, right?

44:19.110 --> 44:25.590
Some people say, hey, don't done don't do that now just hey, one layer application.

44:25.590 --> 44:26.190
I don't care.

44:26.490 --> 44:33.480
But yeah, avoid numbering the CPI B layer, it's not layer five you know, or layer four, layer three

44:33.720 --> 44:38.520
you can with therefore layer three, it's the same language, you know, because they are four nearly

44:38.520 --> 44:41.820
identical to the OSA model.

44:41.910 --> 44:47.610
But layer five is if you say they are five, you have to specify or this is the TCP IP, all that means

44:47.610 --> 44:52.260
this is the application while layer five and and also is actually the session layer you know so the

44:52.260 --> 44:58.470
can become real cumbersome to talk through layer two same thing data link and physical layer is really

44:58.650 --> 45:01.230
something never talked about as far as I know.

45:01.830 --> 45:02.190
Right.

45:02.580 --> 45:06.990
So I don't even see this layer in the TCP IP model.

45:07.260 --> 45:14.310
So it's literally the TCP IP, which is DCP and IP and the data link, right, which is the MAC addresses

45:14.310 --> 45:15.090
and all that jazz.

45:15.690 --> 45:16.050
All right.

45:16.200 --> 45:19.320
How about we summarize this beautiful all say model?

45:19.320 --> 45:25.800
I believe one of the most important thing specifically when you write an applications, you know, it's

45:25.800 --> 45:31.260
really good to understand where your application sits, if it is if it's a network based application,

45:31.260 --> 45:38.130
if it if you if if data passes through your application, it's good to know where your application is

45:38.520 --> 45:40.170
so that you can talk through a SU.

45:40.170 --> 45:47.280
You can know what you can optimize, what do you have access to and what can you improve?

45:47.310 --> 45:47.670
Right.

45:47.670 --> 45:48.420
It's very critical.

45:48.420 --> 45:48.610
Right.

45:48.810 --> 45:50.370
So we talked about the OCI model.

45:50.370 --> 45:55.320
We talked about the we we showed examples, many examples where firewalls, we added proxies.

45:55.320 --> 46:00.600
We had a reverse proxy read the content delivery network CDOs like fastly stuff like that.

46:00.750 --> 46:05.490
They all every ETN is a layer seven reverse proxy.

46:06.000 --> 46:13.440
That's what they are just you know, that's a glorified naming see content delivery network because

46:14.040 --> 46:21.780
it stores the content by definition it has to access it has it need access to your content, right.

46:22.620 --> 46:22.920
Right.

46:23.220 --> 46:25.950
So again, take it with a grain of salt.

46:25.950 --> 46:30.420
You know, each device doesn't have to map to all the seven layers.

46:30.420 --> 46:32.250
You know, it's really blurred.

46:32.250 --> 46:33.900
The line is blurred sometimes.

46:33.900 --> 46:37.290
You know, the TCP IP is definitely a simpler model.

46:37.290 --> 46:42.870
My personally, I prefer the the finer grain quality of things, the breaking things down.

46:42.930 --> 46:50.400
Now while we don't talk about session five as layer six is the really the layer that I almost never

46:50.550 --> 46:52.710
hear anything anyone talk about, right?

46:52.920 --> 46:59.160
But layer five I've seen use cases where someone, hey, I'm actually a layer five.

46:59.370 --> 47:01.080
We're playing a layer five here.

47:01.080 --> 47:03.230
Linker This is a clear example.

47:03.930 --> 47:05.890
One envoy, I believe another one, right.

47:06.000 --> 47:07.380
Hey, we managed sessions.

47:07.380 --> 47:09.450
We managed connections ourselves, you know.

47:09.450 --> 47:14.910
So you're playing it, you're playing a session layer, you're playing at the connection, you're playing

47:14.910 --> 47:17.990
at that just that you don't you don't really care about anything else.

47:18.140 --> 47:20.550
You're building a proxy at the end of the day, link up.

47:20.550 --> 47:22.500
There's a proxy, by the way, if you didn't know that.

47:23.040 --> 47:23.610
But yeah, guys.

47:24.710 --> 47:26.300
Hope you enjoy this lecture.

47:26.750 --> 47:28.430
How we jump into the next one.

## Host to host communication 
WEBVTT

00:00.360 --> 00:02.880
Coast to coast communication.

00:02.880 --> 00:04.710
How messages are sent between hosts.

00:06.740 --> 00:12.110
I struggled with naming in this lecture, but I found it very critical to add just because we knew we

00:12.110 --> 00:16.850
need to talk about just how to host are talking to each other at the lowest level.

00:17.150 --> 00:22.580
You know, and this is what really you need to to understand that we're going to talk about not open

00:22.580 --> 00:23.870
windows than what else is.

00:24.440 --> 00:27.260
This is layer two concepts.

00:27.590 --> 00:32.210
Most of this stuff really and layer three, sometimes we need to send a message from host to host.

00:32.210 --> 00:33.290
B What do we really need?

00:33.500 --> 00:35.720
Usually this is a request to do something on Hornsby.

00:35.720 --> 00:37.280
Hey, I'm sending an RBC call.

00:37.730 --> 00:41.240
Hey, B, do my work for me, please.

00:41.730 --> 00:41.980
Right.

00:42.590 --> 00:49.050
Each host has a network card with a unique media access control or called a mac address.

00:49.050 --> 00:52.340
So if you ever heard about this, you can check your MAC address right now.

00:52.580 --> 00:53.900
Go to your network properties.

00:54.320 --> 00:56.960
You must have a network address.

00:57.020 --> 01:02.030
You know, if you have a VM, a virtual Mac address is created for you, you can create that.

01:02.030 --> 01:05.180
But those this is this is how it looks like effectively.

01:05.180 --> 01:06.620
This is a mac address.

01:06.800 --> 01:07.820
This is one Mac address.

01:07.830 --> 01:09.110
This is another Mac address.

01:09.110 --> 01:09.380
Right.

01:09.650 --> 01:14.870
And they are what, the lowest level of communication.

01:16.090 --> 01:22.750
Of discussion, you know, of these these are the lowest level of communication that it needs to happen

01:23.020 --> 01:31.120
regularly, you know, so if are able to send a message to be so B, C, D is the MAC addresses, I

01:31.120 --> 01:33.360
just simplify them here for simplicity.

01:33.370 --> 01:35.910
Just wanted to make sure that it clean and clean.

01:35.920 --> 01:40.420
You know, I don't want to add the whole, you know, whatever number of bytes here, but l want to

01:40.420 --> 01:43.780
send a message to B and this is the, the, this is the network we have.

01:44.170 --> 01:49.030
Literally everyone is connected to each other, the mesh network, as they call it.

01:49.480 --> 01:55.570
So everyone on the network will get the message, but only B will actually accept that message.

01:56.260 --> 01:56.490
Why?

01:56.590 --> 02:02.290
Because, you see, when I send, I have no idea where to send the data here.

02:02.290 --> 02:05.230
This is this is a analytical homework, almost like a broadcast.

02:05.230 --> 02:06.280
Hey, the send message.

02:07.000 --> 02:10.690
Whoever have this Mac address, please get my message.

02:11.620 --> 02:18.280
But is the thing we have to go up to layer two here to look at the Mac address and compare it to mine.

02:18.310 --> 02:28.360
So everyone, hey, b c DNA will get this frame of data name and then we'll look at it says okay is

02:29.260 --> 02:35.980
this is destined to be I am c drop this is destined to be I am d drop.

02:36.340 --> 02:43.300
No, this is destined to be I am b take it and send that frame to the higher levels the layer.

02:43.300 --> 02:47.440
So layer three, layer four eventually going to get it, all of it if necessary, you know.

02:48.340 --> 02:54.260
So that's very critical if you are in this configuration, which is a very wastage, if you think about

02:54.260 --> 02:54.310
it.

02:54.880 --> 02:59.620
And not only wasting is actually security wise is dangerous.

02:59.620 --> 02:59.860
Right.

03:00.070 --> 03:05.680
That's how what happened in Wi-Fi public Wi-Fi connection when you send packets, right.

03:05.710 --> 03:12.580
Everyone in the Wi-Fi because Wi-Fi is a mesh like everyone is connected device is not so like it's

03:12.580 --> 03:18.520
a wired right knows like I'm connected to this machine and this machine connected to this you know I

03:18.520 --> 03:25.990
only connected to this no Wi-Fi as everyone everyone will get the Mac address as that's how people and

03:25.990 --> 03:28.840
public Wi-Fi sniff passwords back in the day.

03:28.960 --> 03:30.100
It doesn't happen anymore.

03:30.100 --> 03:38.620
But if you have a sniffer that just gets the Mac address but doesn't really drop it because hey, I

03:39.040 --> 03:43.540
yeah, this is not for me, but I wanted I want this beautiful frame.

03:43.900 --> 03:45.190
Give it to me.

03:45.580 --> 03:46.630
Give me that frame.

03:46.630 --> 03:47.350
I need it.

03:48.280 --> 03:50.950
So that's how sniffing networks, nothing is happening.

03:51.580 --> 03:53.200
As long as the data passes through you.

03:54.460 --> 03:56.140
So imagine millions of machines.

03:56.140 --> 03:57.250
Can you get in with each other?

03:57.250 --> 03:57.760
How?

03:57.760 --> 04:00.070
How do we effectively scale?

04:00.220 --> 04:02.300
We cannot just send the data to everyone.

04:02.300 --> 04:08.050
No, we need we need to eliminate the need to send the data to everyone.

04:08.710 --> 04:10.060
The address need to get better.

04:10.330 --> 04:12.070
These mechanisms are just random.

04:12.430 --> 04:16.990
You know, they don't have information that tells me.

04:18.630 --> 04:23.310
Information that tells me where to send it and we're not to send it.

04:24.270 --> 04:26.430
We need relatability.

04:26.440 --> 04:28.950
I don't know if that a word I, I just used it.

04:28.950 --> 04:35.310
So I'm sorry if it's not a word, but we need to out meet the IP address.

04:37.100 --> 04:38.960
That's why we invent things, guys.

04:39.230 --> 04:43.430
We only invent things when we absolutely need it.

04:44.210 --> 04:44.630
Right?

04:44.870 --> 04:47.470
I even spoke in a British accent just to understand it.

04:47.480 --> 04:47.780
Right.

04:48.320 --> 04:50.810
We absolutely need it.

04:51.110 --> 04:56.480
We need this IP address because there is a problem with MAC addresses.

04:56.670 --> 05:00.620
You know, a lot of people say, hey, Mac, aliases are supposed to be global.

05:00.770 --> 05:02.870
Why do we need IP addresses?

05:03.200 --> 05:11.030
My Mac, my iPhone, my fridge has a unique global Mac address.

05:11.360 --> 05:14.060
They will no two machines will have the same device.

05:14.270 --> 05:15.770
Why do we need another address?

05:16.100 --> 05:17.720
Why complicate our life?

05:18.200 --> 05:18.780
We do.

05:19.460 --> 05:21.110
Because of this Barbie relatability.

05:21.110 --> 05:21.920
We cannot rout.

05:22.760 --> 05:26.660
Hey, let's say, okay, if you will give me your Mac address and I'm going to send you a message.

05:26.660 --> 05:28.420
You to close the globe there.

05:28.430 --> 05:33.180
Absolutely no way you're going to get it, because how do I know you get it?

05:33.200 --> 05:35.780
You would need to scan the entire network to find it.

05:35.990 --> 05:40.010
It's literally the same thing I talk about in my database cause, you know, it's just like a scanning

05:40.010 --> 05:40.130
it.

05:40.130 --> 05:46.970
Whole entire table is slower than using an index, you know, to narrow that path.

05:47.570 --> 05:48.440
And that's what we need to do.

05:48.440 --> 05:52.790
We need to slash the number of machines that we need to scan.

05:55.450 --> 05:57.500
And that's why we have an IP address.

05:57.520 --> 05:58.630
The host to host communication.

05:58.630 --> 06:04.060
I built this lecture just because I want to explain the concept of mach an IP address and why we need

06:04.060 --> 06:04.210
to.

06:04.210 --> 06:04.840
Because of IP.

06:04.990 --> 06:09.730
Because I'm not going to explain this again or this is very critical to understand and I want to take

06:09.730 --> 06:10.930
it for it.

06:10.990 --> 06:13.900
Just grab the concept and then run with it.

06:14.290 --> 06:15.820
The IP address has two parts.

06:16.570 --> 06:20.710
The first part is and divide the network and then the second one to define the host.

06:20.950 --> 06:27.100
So it's really while this it's this much bytes, I believe it's four bytes.

06:27.520 --> 06:28.270
It's four bytes.

06:28.270 --> 06:29.350
Yeah, four bytes.

06:29.980 --> 06:37.080
But it describes the entire, you know, sets of 4 billion devices.

06:37.540 --> 06:38.500
But how does it do it?

06:38.500 --> 06:45.730
You know, we don't really scatter 4 billion devices when we send an IP packet, we use the network

06:45.730 --> 06:48.040
portion to eliminate many, many network.

06:48.370 --> 06:53.980
So I only send this packet to the network that is destined.

06:53.980 --> 06:58.990
And then that network we we effectively only have this many hosts.

06:59.140 --> 07:04.600
I'm going to explain that the host path is used to find the host and still we still need the MAC addresses.

07:04.600 --> 07:11.530
There is no escape there because at that low level in that private network, we need MAC addresses to

07:12.070 --> 07:13.570
just deliver that frame it.

07:13.870 --> 07:15.880
Now that we're local, send it.

07:17.320 --> 07:19.180
So here's an example.

07:19.540 --> 07:27.820
We have ABC here and I use the same name here just to confuse you for more host on network n and then

07:27.970 --> 07:31.060
wants to talk to host B on network in two.

07:31.060 --> 07:34.030
So this is not work in two and this is in one.

07:34.270 --> 07:36.100
I used this abstraction.

07:36.100 --> 07:38.110
We're going to become a little bit clearer now.

07:38.410 --> 07:40.060
But this is a network, right?

07:40.180 --> 07:45.550
And there is a router that allows them to network together.

07:45.970 --> 07:46.270
Right.

07:46.420 --> 07:47.830
Raster is a layer three protocol.

07:47.830 --> 07:53.290
So it needs to see the IP packet to look at the addresses in order to allow.

07:54.610 --> 07:58.330
So A-one, two told me this is how it's done, right?

07:58.570 --> 08:03.670
Those two A's and the browser and then the router will send them back it to be.

08:03.860 --> 08:04.120
Right.

08:05.110 --> 08:09.220
So here is the IP address, the IP addresses for.

08:10.550 --> 08:11.180
Four bites?

08:11.210 --> 08:16.970
No, a part of it is the network, and part of it is actually the.

08:18.880 --> 08:19.410
The host.

08:19.420 --> 08:19.710
Right.

08:19.860 --> 08:25.290
I'm going to explain how is this actually effectively as is specified in a minute.

08:25.680 --> 08:29.010
But for example, 192168123.

08:29.190 --> 08:31.470
This is 192168812.

08:31.740 --> 08:35.010
And this is 19268121.

08:35.760 --> 08:37.940
And these are different network.

08:37.950 --> 08:39.740
192.168.2.

08:40.110 --> 08:40.650
See that?

08:40.920 --> 08:44.220
192.16.1 is the shared between this network.

08:44.460 --> 08:45.540
This is the network section.

08:45.900 --> 08:46.440
Why?

08:46.800 --> 08:47.870
Why did you look, Jose?

08:47.880 --> 08:49.280
And why did you look at the first three by?

08:49.280 --> 08:50.370
Why not the first two?

08:50.670 --> 08:55.620
Well, because we told you that this is the network.

08:56.040 --> 08:59.190
The first 24 bit is the network slash 24.

08:59.220 --> 09:02.400
You know, there are other stuff like class AA, class B.

09:03.030 --> 09:04.710
Personally, I don't.

09:05.250 --> 09:07.530
I never seen them used.

09:07.800 --> 09:08.130
Right.

09:08.280 --> 09:12.030
The class eight, class B, class C, you know, this is the future.

09:12.030 --> 09:13.470
No, the classless thing.

09:13.500 --> 09:15.360
That's why I don't want to explain things that.

09:16.310 --> 09:21.290
You're not going to mention in reality, it's as theoretical at the end of the day.

09:21.560 --> 09:25.160
Previously this was Class A, this was class B, class C.

09:25.310 --> 09:32.000
Then they noticed that they made a mistake because, oh, it's really a waste of, you know bytes IP

09:32.390 --> 09:39.200
to use class and Cosby class C so they move to this classless thing, which is basically let me know

09:39.200 --> 09:45.650
how many bits is your network because you can use one bit for your network or up to 31, you know,

09:45.830 --> 09:46.660
because we have a.

09:47.720 --> 09:49.270
For 8 minutes.

09:49.280 --> 09:49.520
Right.

09:50.330 --> 09:52.870
So now we have the network and this is the network.

09:52.910 --> 09:53.870
So that's 94, right?

09:54.200 --> 09:56.720
So this is the shared part.

09:57.290 --> 09:58.700
If this part is different.

09:59.960 --> 10:02.060
That means you are on a different network, Poppy.

10:03.290 --> 10:08.960
So now 192168123 wants to talk to 192.168.222.

10:09.470 --> 10:10.730
These are different networks.

10:11.270 --> 10:12.560
How do you know this from network?

10:12.770 --> 10:13.310
Simple.

10:13.730 --> 10:15.470
There's something called the subnet mask.

10:15.480 --> 10:18.920
You apply that, which is basically this slash 24.

10:19.220 --> 10:22.820
And if you get a different number, that means you are not in the same network.

10:23.030 --> 10:26.210
If you get the same number, if you get the same network, you're on the same network.

10:26.510 --> 10:27.260
If you are not.

10:27.860 --> 10:29.430
Then you say all bets are off.

10:29.450 --> 10:35.360
Send it to the net to the router, which is your gateway, and that gateway will take care of routing

10:35.360 --> 10:36.260
it to somewhere else.

10:36.470 --> 10:39.980
So it changes things in the process.

10:40.420 --> 10:42.050
There's a reason I do think about.

10:42.860 --> 10:44.300
So, yeah, so that's how it's done.

10:44.810 --> 10:46.970
You're out from one network to another network.

10:47.330 --> 10:48.410
This is a pause.

10:49.340 --> 10:53.330
If you don't have this logic, then you have to send it here as it is here.

10:53.450 --> 10:55.580
And then to here and then to here as it is here.

10:55.600 --> 11:00.080
So you have to scan six machines just to find that.

11:00.080 --> 11:00.270
No.

11:00.350 --> 11:05.000
But here you immediately know, because this writer knows exactly where this machine is.

11:05.180 --> 11:06.710
It will send it immediately to it.

11:08.930 --> 11:12.080
But my host have many apps.

11:14.530 --> 11:16.510
It's not enough just to address the host.

11:16.600 --> 11:16.780
Right.

11:16.820 --> 11:17.290
Because now.

11:17.290 --> 11:20.170
Yeah, you send me a a packet.

11:20.290 --> 11:21.460
What do I do with that?

11:22.150 --> 11:24.850
Don't I have many applications?

11:25.390 --> 11:25.750
My.

11:25.900 --> 11:28.300
My machine's not really running one thing.

11:28.410 --> 11:30.220
No, it has all sorts of things.

11:30.610 --> 11:36.010
So we need another fine grained level control beside the IP address.

11:38.290 --> 11:46.590
You can send a request on Port 82 right on the same machine and the DNS request on Port 53 and says

11:46.640 --> 11:50.050
this request on Port 22, all running on the same server.

11:50.920 --> 11:52.750
How does this happen?

11:53.260 --> 11:55.210
Ports is what?

11:56.470 --> 11:56.830
What?

11:57.940 --> 11:58.870
What do we use here?

11:59.260 --> 12:02.990
We use ports in addition to the IP address to know.

12:03.010 --> 12:03.280
Okay.

12:03.280 --> 12:03.580
Yeah.

12:04.860 --> 12:09.870
The Rather did a job deliver the packet to me as a host.

12:09.870 --> 12:11.070
But I.

12:12.460 --> 12:16.540
Need to know where do you want to go, which process?

12:16.540 --> 12:23.590
I have thousands of processes and that the port, the destination port and the source port is also important

12:23.890 --> 12:26.740
to understand where exactly you need to go.

12:26.950 --> 12:29.110
So host the host communication summary.

12:29.110 --> 12:33.400
I really out of this lecture to talk about the IP address, why do we need it?

12:33.730 --> 12:39.130
Talk about Mac addresses and then the problem with Mac addresses and why would we introduced IP addresses

12:39.370 --> 12:41.350
and then talk about the needing of the ports.

12:41.530 --> 12:47.230
And I talk about really we added a flavor of adding that, talking about the concept of networks which

12:47.230 --> 12:52.390
we will explain in detail in the future, but talking about different networking, you know, how what

12:52.390 --> 12:55.030
does it mean to send one packet to another network?

12:55.210 --> 12:57.670
What does it mean to send a packet to the same network?

12:57.970 --> 13:01.110
All of that that will be will be demystified.

13:01.120 --> 13:07.810
But I just wanted to kind of tease up our guys to introduce this concept, just to have an overview,

13:07.810 --> 13:12.820
because this is kind of a fundamental really and understanding as in my opinion.

13:13.120 --> 13:15.490
And finally, we really need the idea of ports.

13:15.920 --> 13:19.720
I am you noticed that everything in this guide, I say, why do we need something?

13:19.720 --> 13:26.620
And I just why, you know, and this is the only reason I'm doing this and it maybe a little bit annoying.

13:26.620 --> 13:31.870
I'm sorry, but the reason I'm doing is because I personally ran into these questions before, you know,

13:31.870 --> 13:32.860
I was frustrated.

13:32.860 --> 13:35.950
Okay, why do any ports why do you need IP addresses?

13:36.160 --> 13:37.690
Why do we need a network?

13:38.320 --> 13:39.400
All of these questions.

13:39.790 --> 13:49.780
I try to frame them in a way so that I have an answer that will reveal and demystify things like let

13:49.780 --> 13:51.310
me know if this is this helps or not.

13:51.310 --> 13:54.070
But yeah, four ports are also another concept.

13:54.070 --> 13:59.020
So host to host communication really critical to understand these basic.

13:59.890 --> 14:01.000
Building blocks, you know.

14:01.600 --> 14:06.520
IP address, MAC address, network host and port.

14:06.820 --> 14:08.350
You know, simple things.

14:08.590 --> 14:10.360
You deal with them on a daily basis.

14:10.360 --> 14:15.430
Viewer back in engineering network engine you know even the front end user you send port request or

14:15.430 --> 14:19.650
request to port all the time but and you specify the IP address as well.

14:19.660 --> 14:19.930
Right?

14:20.320 --> 14:25.480
I wish I added another slide to talk about localhost, but it's kind of clear I localizes the IP address

14:25.480 --> 14:27.010
that is loopback.

14:27.160 --> 14:28.750
You know, never leaves the machine.

14:28.780 --> 14:31.660
You're talking to the same IP address.

14:31.660 --> 14:33.130
127001.

14:33.130 --> 14:37.510
No, that's the IPV four and call in one k so IPV six.

14:37.510 --> 14:45.190
But we're talking about the same machine that we, when we listen on a server DB server locally and

14:45.190 --> 14:49.830
send a request, nobody else can talk to this machine because we listened on local horse ram.

14:49.840 --> 14:53.230
That's another constant ad and in addition, in the summary.

14:53.830 --> 14:54.100
All right.

14:54.100 --> 14:54.970
Thank you so much.

14:55.270 --> 14:56.590
Let's jump to the next lecture.








# Internet protocol 
## IP Building blocks 

WEBVTT

00:00.060 --> 00:00.520
All right.

00:00.540 --> 00:08.790
How about we start this section, the IP protocol with the first lecture, the IP building blocks.

00:09.810 --> 00:17.250
And I named it this way because I think these are the basic, you know, building blocks that we need

00:17.250 --> 00:19.890
to understand in order to understand the IP protocol.

00:19.920 --> 00:24.360
You know, we're going to talk about things that I mentioned in the previous lectures like Subnet Mask

00:24.360 --> 00:28.740
and Network and the whole host and, you know, class lists and stuff like that.

00:28.830 --> 00:30.000
We're going to talk about all that stuff.

00:30.040 --> 00:33.210
You know, I'm just trying to demystify this as much as possible.

00:33.360 --> 00:35.610
What happened when you actually wrote the packet?

00:35.910 --> 00:37.560
What happened when I sending a packet?

00:37.560 --> 00:40.020
No, I'm mentioning the word packet to guide.

00:40.440 --> 00:45.930
And I want you in your brains to think about what a packet is, is the layer three.

00:45.930 --> 00:53.250
Now, when I say packet as layer three, that means it's a bunch of data with destination IP address,

00:53.250 --> 00:56.550
with source IP address that's set with other headers.

00:56.550 --> 00:57.480
But we don't care now.

00:58.140 --> 00:58.320
Right.

00:58.320 --> 00:58.860
But that's it.

00:59.310 --> 00:59.910
Ports.

01:00.630 --> 01:01.650
I don't care for the.

01:01.650 --> 01:07.800
Yeah, that is ports inside of there is the trace and the data, all of this stuff inside this IP back

01:07.860 --> 01:13.590
but to the rafters it's just an IP packet and that's the beauty of this whole all is I think, you know,

01:13.590 --> 01:15.870
if you think about it, let's jump into it.

01:16.140 --> 01:19.440
IP address is a layer three property.

01:19.560 --> 01:20.370
We talked about this.

01:20.820 --> 01:24.780
It can be set automatically or stateless, statically, statically.

01:24.780 --> 01:25.110
Right.

01:25.590 --> 01:27.270
And this is the DHCP thing.

01:27.480 --> 01:30.840
I'm going to talk about it, but the idea is the IP address can be assigned.

01:31.050 --> 01:37.200
You know, this is a way or a network engineering course, actual course detail ID will be valuable.

01:37.200 --> 01:43.110
You know, talking about okay, how is the CPU oracle is assigning this is a network level thing, you

01:43.110 --> 01:47.400
know, networking, network engineering kind of a thing.

01:47.400 --> 01:48.870
You know, it's a little bit more detail.

01:48.870 --> 01:54.570
So I won't gone to that level of detail because hey, I as long as I have an IP address, I'm good.

01:54.570 --> 01:56.860
I'm not troubleshooting my network.

01:56.860 --> 02:03.870
So there are the network engineers who are, you know, well versed and adept in that particular thing,

02:03.870 --> 02:07.590
you know, troubleshooting and oh, IP, the IP.

02:07.590 --> 02:09.510
And how does it work to protocol?

02:09.630 --> 02:10.350
It's all right.

02:10.980 --> 02:14.130
Maybe I will change my mind and add a lecture for it in the future.

02:14.190 --> 02:14.550
Who knows?

02:16.110 --> 02:19.740
But yeah, the IP address can be assigned automatically.

02:19.950 --> 02:24.120
Or you can statically fix it on your machine.

02:24.180 --> 02:25.410
No, and it has.

02:25.410 --> 02:26.290
I will talk about this.

02:26.290 --> 02:29.190
It has a network port and a host portion.

02:29.640 --> 02:34.330
The IP address is a four by two and it's going to be V four and it's more than that.

02:34.740 --> 02:35.430
IPV six.

02:35.520 --> 02:37.350
I'm going to talk about IPV six in this course.

02:37.740 --> 02:39.150
Maybe in the future I'm going to add more.

02:39.510 --> 02:41.100
Yeah, let's keep it law.

02:41.310 --> 02:46.110
But there's so much content as it will add more stuff in the future.

02:46.590 --> 02:48.390
But yeah, there is do a bit right.

02:49.380 --> 02:50.520
And there's two.

02:51.410 --> 02:55.910
Portion the A, B, C, D or the a, b CD.

02:56.390 --> 03:00.800
Is this is the first by a second by third by four by and the slash x.

03:00.800 --> 03:03.470
And I want you to understand this slash x, right?

03:03.740 --> 03:08.210
The X here is the network bits and what remains are the host.

03:08.240 --> 03:09.200
And here's an example.

03:09.230 --> 03:09.500
Yeah.

03:09.740 --> 03:14.660
If you say 12192168.254.0 slash 24.

03:14.960 --> 03:18.680
That is the first 24 bit which is 888.

03:18.680 --> 03:19.670
That's 24.

03:20.000 --> 03:27.740
These puppies are the network portion and this left by alone.

03:27.740 --> 03:31.220
The fourth byte in this case is the host.

03:31.220 --> 03:40.100
That means I can have up to 25d5 horse, right while I can have up to whatever two to the ball 24 networks.

03:40.220 --> 03:45.980
Now the first 24 bit three byte are network host the rest are eight for the host just talked about this

03:46.340 --> 03:49.160
this means we can have up to two the power 24.

03:49.340 --> 03:50.900
Look at how many networks do you on?

03:51.230 --> 03:53.060
Do we really need this much networks?

03:53.240 --> 03:57.650
Ask yourself again if you're a network administrator, that's that's one part of your job.

03:57.650 --> 04:01.250
And this is not something we usually do as a back in and do we build applications.

04:01.250 --> 04:03.560
We need to understand how that packets are delivered.

04:03.920 --> 04:10.070
But configuring the network is something really is better left to the network engineer who this is their

04:10.070 --> 04:11.300
bread and butter, as they say.

04:11.300 --> 04:11.510
Right?

04:11.690 --> 04:12.980
Like how many network do I need?

04:12.980 --> 04:14.900
Oh, do I need slash 24.

04:15.220 --> 04:15.950
A little bit too much.

04:16.010 --> 04:17.540
Let me let me reduce that.

04:17.570 --> 04:21.650
I am more host than networks, actually, and you can play with that.

04:21.980 --> 04:23.990
This is a ward by itself.

04:23.990 --> 04:30.950
That's why I really mentioned that the discourse is not really for a depth network engineer want want,

04:30.960 --> 04:35.810
teach you all these low level stuff, you know, CCNA and passing all these exams.

04:35.810 --> 04:41.780
No, this is actually decided, designed for our software engineers who want to understand the network.

04:41.780 --> 04:42.980
It's a bridge now.

04:43.160 --> 04:47.810
After that, if you're really interested in networking, you might take an actual networking course

04:47.810 --> 04:53.690
and you might have a actually a better, you know, better luck with it if you want if you think about

04:53.690 --> 04:55.730
it, because now you get to understand the high level stuff.

04:58.780 --> 05:03.460
And each of these network will have 2 to 55 hosts.

05:04.120 --> 05:05.650
And this is also called a subnet.

05:05.740 --> 05:11.410
If you ever heard about this subnet because of a subnet subnet mask, very critical concept.

05:11.710 --> 05:16.090
So if I do 19216822 54.0 slash 24.

05:16.420 --> 05:20.850
This is also called a subnet and the subnet must have a subnets mask.

05:20.920 --> 05:27.340
So if the subject mass is used, if you're sending an IP packet, you know, and you have an IP address

05:27.340 --> 05:36.490
and you want to know that is this IP address that I'm about to send to belong to my subnet or not to

05:36.490 --> 05:41.290
answer that particular question because that question will.

05:42.350 --> 05:48.710
Will be forced into to, you know, logics, like if it's in my subnet to do this, if it's not of my

05:48.710 --> 05:49.580
summit, do that.

05:50.060 --> 05:50.360
Right.

05:50.540 --> 05:56.060
If it's in my subnet, you can use the Mac address to send it directly back to the host to host communication.

05:56.330 --> 06:01.220
Just use the mac address to send it directly because it's literally in the same network as you.

06:01.340 --> 06:01.660
Yeah.

06:01.970 --> 06:04.160
While if it's not in your subnet, all bets are off.

06:05.300 --> 06:11.060
You need to talk to someone who knows how to rout this and use it.

06:11.390 --> 06:13.790
This is usually called a router or a gateway.

06:14.150 --> 06:16.010
That's why you have a gateway IP address.

06:16.010 --> 06:19.430
In every network you assign, there's a gateway IP address.

06:20.060 --> 06:22.130
That's when things are unclear.

06:22.160 --> 06:24.560
Hey, what do I know that I don't know.

06:24.680 --> 06:25.700
Send it to the gateway.

06:26.510 --> 06:30.320
Subnet mask is used to determine whether an IP is in the same subnet or not.

06:31.400 --> 06:32.060
Default gateway.

06:32.060 --> 06:33.020
We just talk about this, right?

06:33.470 --> 06:34.310
Default Gateway.

06:34.340 --> 06:38.390
Most networks consist of host and a default gateway.

06:38.510 --> 06:45.260
So you have a network and you have a bunch of hosts right in that network up to whatever the host bets

06:45.260 --> 06:51.590
you are allowed to have that network and there must be one of those host must be a gateway.

06:51.890 --> 06:52.180
Why?

06:52.220 --> 06:56.540
Because those host they want to talk to somewhere outside of their subnet.

06:57.260 --> 06:58.830
They need to talk to the gateway.

06:59.090 --> 07:03.590
The gateway is just another device that happened to have two network interfaces.

07:03.800 --> 07:09.110
One network that is assigned to belong to this network, and another network that belongs to another

07:09.110 --> 07:12.320
network, or maybe three or four or five or six.

07:12.800 --> 07:16.340
These border routers have hundreds of networks.

07:16.340 --> 07:18.170
You know, they can talk to many other networks.

07:18.440 --> 07:23.300
So host a can actually talk to host B directly if they are both in the same network, you know, same

07:23.300 --> 07:24.230
subnet effectively.

07:24.470 --> 07:26.440
And they use the Mac address for that.

07:26.450 --> 07:26.780
Right.

07:27.890 --> 07:34.970
Otherwise, if A doesn't know how to talk to be if it's B is in not in a subnet and it can find out

07:34.970 --> 07:35.990
by using the subnet mask.

07:35.990 --> 07:37.430
We're going to give an example, guys only.

07:37.460 --> 07:38.000
Now, wait a minute.

07:38.450 --> 07:42.080
Otherwise assigns it to someone who might know that gateway.

07:42.380 --> 07:44.240
That Gateway might not know, by the way.

07:44.750 --> 07:45.050
Right.

07:45.470 --> 07:50.690
Because the gateway eventually might talk to another gateway that might know, you know, you get the

07:50.690 --> 07:51.140
point, right?

07:51.350 --> 07:52.550
It's an elegant design.

07:53.030 --> 07:54.020
I absolutely of it.

07:54.770 --> 08:00.440
The Gateway has an IP address on each and each host should know its gateway.

08:00.470 --> 08:00.770
Right.

08:00.980 --> 08:05.600
And it also have multiple IP addresses depending on how many networks are.

08:05.630 --> 08:06.020
Dr. Doctor.

08:06.440 --> 08:09.800
Hey, find an example and I'm going to disappear here so you can see the whole picture.

08:09.830 --> 08:10.250
All right.

08:10.880 --> 08:14.570
So, host 192168.1.3.

08:14.570 --> 08:20.260
Wants to talk to 19216812, two, two, talk.

08:20.270 --> 08:21.590
I use the word talk here.

08:21.590 --> 08:29.600
I really literally mean sending data, sending packets which to translate it to application client front

08:29.600 --> 08:30.980
end back end speak.

08:31.160 --> 08:35.010
We're sending in DTP request, for example, right now that's talking, right?

08:35.240 --> 08:42.140
Assuming 1.1.2 is actually a server and 1 to 3 is actually a client in this case.

08:42.140 --> 08:45.920
Or you want to send a curl request or you do a server.

08:46.130 --> 08:47.600
That's what talks are really mean.

08:47.840 --> 08:56.540
And then to they as I search or not as DTP DNS, all of these fits into a nicely tucked in IP packet

08:56.780 --> 08:59.660
which has a destination IP and the source IP.

08:59.870 --> 09:00.950
And that's the beauty of this.

09:01.110 --> 09:03.080
Browsers don't care about the protocol.

09:03.090 --> 09:05.240
Some routers, unfortunately, do.

09:05.240 --> 09:06.380
They look at the content.

09:06.380 --> 09:09.920
They block certain protocols, but most don't.

09:10.100 --> 09:11.810
No, but let's let's take a look.

09:12.140 --> 09:15.310
192168.12312.21.2.

09:16.730 --> 09:18.260
First of a question, try to answer.

09:18.590 --> 09:20.000
Are you in my subnet?

09:21.170 --> 09:27.440
It applies a subnet mask to itself and the destination IP address would subnet mask it's own subnet

09:27.440 --> 09:27.860
mask.

09:28.190 --> 09:30.560
Right, because that's the only thing it has.

09:30.560 --> 09:32.210
It doesn't have the subject matter of the other machine.

09:32.210 --> 09:33.260
It doesn't need it actually.

09:33.470 --> 09:36.200
It needs the subnet mask of you, which you have.

09:36.410 --> 09:36.650
Right.

09:36.650 --> 09:37.940
You can go to your network.

09:37.940 --> 09:42.950
You're going to have three things the your IP address, your subnet mask and your gateway.

09:43.490 --> 09:46.520
Without these, you are you cannot do anything.

09:46.610 --> 09:48.650
You're basically dead in the water.

09:48.650 --> 09:50.000
You cannot connect with anyone.

09:50.120 --> 09:50.350
Right.

09:50.600 --> 09:51.710
You need these three pieces.

09:52.190 --> 09:57.710
So you take this guy, do that to five, five, two, five, 5255.0.

09:57.890 --> 09:59.360
Apply that right.

09:59.360 --> 10:05.560
If you do the normal and operator, you know this is ones all of these are ones you'll find five via

10:05.570 --> 10:06.050
this one.

10:06.410 --> 10:13.070
Right and this is zero ones and anything one, if you add anything with a one, it becomes the same

10:13.070 --> 10:13.490
value.

10:13.670 --> 10:19.490
So when you add these bits, right, this is simple byte operations.

10:19.880 --> 10:22.820
Anything that you end with a one becomes the same value, right?

10:23.060 --> 10:30.570
So 192 becomes Raymond 992168 with 255 becomes one nine.

10:30.590 --> 10:32.570
Because at the end of these, these are one one.

10:32.600 --> 10:36.050
I wish I, I built a bitmap for you guys, but you get it right.

10:36.320 --> 10:37.640
One, one, one, one, one, one.

10:37.640 --> 10:40.530
And these are actual bits, like one zero, whatever.

10:40.970 --> 10:41.780
So anything you.

10:41.860 --> 10:43.480
And he's going to become the same value.

10:43.690 --> 10:43.890
Right.

10:44.140 --> 10:46.030
Two, five, five, and one becomes one.

10:46.240 --> 10:48.100
And there's the most important thing.

10:48.100 --> 10:48.670
Zero.

10:48.670 --> 10:49.930
And anything is zero.

10:50.740 --> 10:53.220
If you add anything with zero, just nulls it out.

10:53.230 --> 10:53.560
Right.

10:53.890 --> 10:56.110
So zero and three is zero.

10:56.800 --> 10:57.100
All right.

10:57.280 --> 11:01.960
Let's apply to the second IP address two and Z two and zero is zero.

11:02.410 --> 11:03.970
And this is the output from this.

11:04.090 --> 11:10.690
The second IP address, this is out of 19.168.101926.11.120.

11:11.080 --> 11:13.000
These are the same subnet.

11:14.230 --> 11:19.660
And that question leads to the first branch that we talked about which nobody took out.

11:20.410 --> 11:21.820
I don't need to rout it.

11:22.090 --> 11:23.530
I don't need you, guy.

11:24.220 --> 11:25.210
I don't need this guy.

11:25.510 --> 11:28.120
I actually do because it's a switch in this case.

11:28.120 --> 11:29.270
It's playing as a switch.

11:29.290 --> 11:30.430
We're going to talk about it in a minute.

11:30.910 --> 11:36.270
So I am sending this data to my writer, but the writer is just going up to layer two.

11:36.280 --> 11:38.260
In this case, it doesn't need the IP address.

11:38.260 --> 11:38.550
But why?

11:38.560 --> 11:41.560
Because it is in the same subnet, right?

11:42.250 --> 11:46.140
I believe maybe the router will go to that layer and looks at the as.

11:46.150 --> 11:47.650
But it is the same IP address.

11:47.650 --> 11:47.920
Right.

11:48.400 --> 11:51.100
So in this case, it will just say, look at the Mac address.

11:51.370 --> 11:52.120
This is all right.

11:52.750 --> 11:54.520
This Mac address is actually on this board.

11:54.910 --> 11:55.330
Boom.

11:55.600 --> 11:56.470
Let's send it right here.

11:56.740 --> 11:59.320
So the router will act as a switch in this case.

11:59.620 --> 12:03.640
So it will look all it really need just there to this particular case.

12:03.910 --> 12:06.100
And this, by the way, the second one, we're going to come to that.

12:07.200 --> 12:09.060
All right, let's spice things up a little bit.

12:09.330 --> 12:12.630
192.168.1.3.

12:12.630 --> 12:16.170
Wants to talk to 192.168.222.

12:16.620 --> 12:17.490
This guy.

12:18.030 --> 12:19.650
This guy wants to talk to this guy.

12:20.070 --> 12:21.810
Well, it's a different network, right?

12:22.050 --> 12:22.860
How did I know?

12:22.980 --> 12:24.300
Well, apply them, ask.

12:24.510 --> 12:31.290
And all of a sudden, you know that this is 19216120i, I been one, two or three.

12:31.290 --> 12:32.250
Am I right?

12:33.290 --> 12:35.250
Uh, this is my network.

12:35.550 --> 12:39.780
The guy I want to talk to is 2.0 different subnet.

12:39.960 --> 12:41.760
I don't know what to do.

12:42.150 --> 12:43.370
This is different subnet.

12:43.740 --> 12:46.200
I need to routing to someone who does.

12:46.500 --> 12:48.750
The packet is sent to the default gateway.

12:48.990 --> 12:51.810
My default gateways 192168.1.1.

12:53.730 --> 12:56.760
Now you need to send the packet to the router.

12:56.760 --> 12:59.130
I can guess what you need.

12:59.460 --> 13:04.170
This is now loops back to the first scenario.

13:05.170 --> 13:07.510
What are you sending a horse to horse directly.

13:07.990 --> 13:14.230
Now you're as if sending that packet itself destined to this guy.

13:14.680 --> 13:19.240
But the Mac address, right, is the router.

13:19.690 --> 13:23.950
And here's where every attack possible happens.

13:24.550 --> 13:25.900
This is called are poisoning.

13:26.350 --> 13:32.260
If someone here to pretend to be the router, then all the packets can go through it.

13:32.440 --> 13:36.280
And that's how our poisoning happen as another topic for another day, right?

13:37.000 --> 13:42.880
Because the MAC addresses is I need to know what is the Mac address of my router because now I need

13:42.880 --> 13:45.760
to send them back it to my router.

13:45.760 --> 13:46.060
Right.

13:46.300 --> 13:49.390
And my author is in myself the same subnet as I am.

13:50.100 --> 13:50.190
Right?

13:50.250 --> 13:54.850
I sent this to Rather and the router turns around and understand that.

13:54.850 --> 13:56.710
Hey, okay, where is this guy?

13:56.710 --> 13:57.150
One night?

13:57.670 --> 14:01.330
So the router has actually another IP address on the other end.

14:01.330 --> 14:03.620
19.68.22 201.

14:03.910 --> 14:06.820
So router lives, double lives.

14:06.820 --> 14:08.890
You know, it lives two lives.

14:08.890 --> 14:11.590
You know, that's that's what it does, you know.

14:11.860 --> 14:13.780
So it's living two lives effectively.

14:13.780 --> 14:16.600
It's a it's an it's an address here and it's an address here.

14:16.600 --> 14:20.500
So it's living it's a literally you have two representations.

14:20.800 --> 14:27.160
So this can talk to this and this kind of is and that's how this how basically it is done.

14:27.970 --> 14:28.390
All right.

14:28.390 --> 14:33.040
Let's summarize so talked about what an IP address as talked about what is the difference between a

14:33.040 --> 14:34.690
network portion and the host portion.

14:34.960 --> 14:41.920
And you can know what is your network today if you want and you can know how many host can it possibly

14:41.920 --> 14:45.820
happen and you can configure your router to assign more or less.

14:45.820 --> 14:46.570
Host Right.

14:46.720 --> 14:52.210
Based on that and we're talking about the subnet, we are told about the subnet mask, very, very critical

14:52.210 --> 14:53.290
concept to understand.

14:53.680 --> 15:01.120
And we're going to talk about more why this is a critical and in the final section actually where if

15:01.120 --> 15:06.760
your database is actually in a different subnet, then you're back in application.

15:07.120 --> 15:15.220
Then IP packets that are in form of TCP connection request, you know, from your back in application

15:15.220 --> 15:18.670
to that database is going through the router.

15:19.390 --> 15:23.560
And if this routing is congested, then you're going to see delays.

15:24.630 --> 15:29.280
So this is a little bit of a tease and spoiler alert, you know, to that section.

15:29.280 --> 15:32.610
But that's one of the thing that just makes sense.

15:32.970 --> 15:35.370
Do not put your database in a different subnet.

15:35.460 --> 15:40.680
You know, sometimes it's not that that to be honest, it it's okay to put it in a different subnet.

15:40.980 --> 15:48.120
But what happen if this rather is so congested, if it's if it's talking to thousands of the networks,

15:48.330 --> 15:48.560
right.

15:49.140 --> 15:56.280
Or so many networks and so many host it's routing packets, then there might be chances where the router

15:56.280 --> 15:58.050
will buffer will fill down.

15:58.320 --> 16:05.760
And your beautiful sequel statement request, which will transmit to multiple segments, will be posed

16:06.420 --> 16:11.100
in the router and it will never reach the database until a few millisecond later.

16:11.340 --> 16:12.810
And you will see those delays.

16:12.960 --> 16:14.220
You will knows why.

16:14.220 --> 16:16.410
I do have delays in my back in application.

16:17.100 --> 16:23.940
That's just tiny, something tiny and is immediately you understand it because now they understand what

16:23.940 --> 16:24.900
is actually happening.

16:25.110 --> 16:26.940
Now go check your back in configuration.

16:26.940 --> 16:33.360
Do you have your database different than your your application pull in the subnet because it costs you

16:33.360 --> 16:33.720
nothing.

16:34.080 --> 16:34.310
Right.

16:34.470 --> 16:36.060
In this case, put a switch.

16:36.570 --> 16:37.610
Put an actual switch.

16:37.660 --> 16:40.140
This is where network configuration comes into the picture, actually, right?

16:40.320 --> 16:47.370
Where you get to put an actual network switch and you talk a high performing network switch and you

16:47.370 --> 16:54.000
put the database and the application took it to the switch that the application has no business talking

16:54.000 --> 16:55.100
to the router, right?

16:55.200 --> 17:00.420
Don't use the router to run out application packets to your as a switch.

17:00.420 --> 17:03.510
You know that's just a cheap switch at this and right.

17:03.810 --> 17:09.720
Routers is not they are not designed to be switches that's why those high performance switches are cost

17:09.720 --> 17:11.350
a lot of money and they're price switches.

17:11.350 --> 17:18.840
And now again, I'm not very versed in this, but if you really want to go to that level, that's a

17:18.840 --> 17:22.110
network engineering, bread and butter.

17:22.110 --> 17:23.310
You know, that's where.

17:24.250 --> 17:25.570
And that's what I want.

17:25.600 --> 17:26.830
I want to bridge that gap.

17:26.860 --> 17:28.060
That's what I'm talking about, guys.

17:28.840 --> 17:29.710
Back in Engineer.

17:30.580 --> 17:37.240
The moment you understand this, you will ask the network engineer to do this configuration photo because

17:37.290 --> 17:39.960
you don't have no idea what you want.

17:39.970 --> 17:40.170
Right?

17:40.180 --> 17:43.510
Because they know everything, but they don't know what you want.

17:43.900 --> 17:44.200
Right?

17:44.380 --> 17:46.270
So if you are a network engine, you're talking.

17:46.270 --> 17:46.630
Of course.

17:46.630 --> 17:47.050
Thank you.

17:47.260 --> 17:51.640
But you now understand the requirements, right?

17:52.420 --> 17:54.640
But now we're bridging this gap.

17:54.640 --> 17:57.250
We're closing the wound, as they say.

17:57.730 --> 17:58.210
But yeah.

17:58.570 --> 18:03.970
And the default gateway, the concept of the default gateway also has been explained in this lecture.

18:04.360 --> 18:11.320
How about we jump into it and move to the next lecture or the first lecture of the IP packet RFP thing?

18:11.620 --> 18:14.620
You know, there there's so much, so much to discuss here.

18:15.730 --> 18:16.540
Let's jump into it.

## IP Packet 
WEBVTT

00:00.060 --> 00:06.720
Now that we have discussed the building blocks of the Internet protocol itself, I'd like to go and

00:06.720 --> 00:08.700
take a moment to.

00:10.010 --> 00:16.400
Take the lid off of this and dive into the IP packet itself.

00:16.850 --> 00:21.080
This is the anatomy of the IP packet as jump into it.

00:21.320 --> 00:27.320
I'll write the IP packet, the anatomy of the IP packet itself.

00:27.620 --> 00:30.380
You know, we're now we're going a little bit deeper.

00:30.590 --> 00:37.580
We've always as back end engineers and funded engineers, we always look at the IP packet as just a

00:37.580 --> 00:44.570
bunch of data with a targeted IP address and a source IP address, as at least I always visualize it

00:44.570 --> 00:48.680
this way, but it's critical to understand certain pieces.

00:48.680 --> 00:49.880
Not all, really.

00:50.180 --> 00:55.160
What I believe there are certain important information about the IP back itself, and this is what this

00:55.160 --> 00:55.790
lecture is about.

00:56.360 --> 00:58.370
So what does IP but IP recognize?

00:58.370 --> 01:00.800
Headers and data sections.

01:01.220 --> 01:02.840
Two sections, the data and the header.

01:03.170 --> 01:05.050
Most of the time we really care about the data.

01:05.060 --> 01:06.410
We don't really care about the headers.

01:06.800 --> 01:16.490
But if you want to debug certain problems or understand certain situations, you need to dive into this

01:16.490 --> 01:16.790
thing.

01:17.720 --> 01:23.300
One more important thing to understand is the size of the packet and headers come into the picture.

01:23.330 --> 01:26.660
If you add a 20 extra byte, that's the IP here, by the way.

01:27.110 --> 01:30.890
20 byte extra to your data.

01:30.920 --> 01:34.340
That is a 20 by that you that's not really your data.

01:34.340 --> 01:37.850
It's it's the cost of doing business effectively.

01:38.390 --> 01:38.960
And guess what?

01:39.380 --> 01:43.820
This can go up to 60 bytes if there are certain options are enabled.

01:43.820 --> 01:47.030
So I believe those options are not always in.

01:47.160 --> 01:52.820
But if they are, you can go up to 60 bar it's forces to back it.

01:52.820 --> 02:00.920
So it is really important for these certain algorithms to kick in to save on sending like a single bite

02:01.220 --> 02:05.030
of packet, you know, with 20 header, 20 bytes header.

02:05.030 --> 02:10.490
It's just a waste of time, you know, it's just a waste of resources to send a single wide and then

02:10.490 --> 02:13.460
attach a 20 byte header to it.

02:13.460 --> 02:15.980
So that's what algorithm like.

02:15.980 --> 02:21.920
Nigel Algorithm and delayed acknowledgement try to solve effectively, you know, try not to send your

02:21.920 --> 02:26.300
else command through search as a single back is just a waste, you know.

02:26.570 --> 02:29.150
But sometimes you can escape that, you know.

02:29.480 --> 02:38.660
That's why we have the data section can go up to 65, 536, you know, and that's because the length

02:38.660 --> 02:40.820
of the data itself is as 16 bit.

02:40.880 --> 02:47.150
So you can only address up to 16 bit worth of content that's equal to the equivalent to 65,000.

02:47.150 --> 02:55.040
And to be honest, I never seen an IP packet that large at all because if you think about it right,

02:55.040 --> 03:01.040
and we're going to talk about this in later sections, there is something called the empty you name,

03:01.520 --> 03:03.290
which is the maximum transmission unit.

03:04.070 --> 03:07.040
So next transmission within the Internet is 1500.

03:07.460 --> 03:16.250
So what packet and avoid all the ideas or fragmentations you can't really shove more than 1500 words

03:16.250 --> 03:18.320
around IP packet without a fragmentation.

03:18.320 --> 03:24.920
So seeing that maybe in a cloud and Amazon where is that custom made hardware with empty you is I don't

03:24.920 --> 03:33.080
know a gigabyte gigabit empty use that I don't know if that's even possible but that will reach that

03:33.080 --> 03:42.080
but to me you will never reach that in single IP packets is almost the average is 1500 bytes, maybe

03:42.080 --> 03:45.410
9000 certain situation, but that's sort of in jumble friends.

03:45.410 --> 03:46.610
Well, that's a bit premature.

03:47.030 --> 03:51.200
So yeah, I always like to add this IP packet to a back end engineer.

03:51.950 --> 03:54.380
It's a bunch of data destination IP address.

03:54.560 --> 04:01.010
So as IP areas, I for the longest time I always look at the IP back in like this now and effectively

04:01.010 --> 04:05.780
like this the right hand side has the destination and the left hand side is the source IP address.

04:06.110 --> 04:08.360
It doesn't look like this on.

04:09.330 --> 04:10.230
On paper.

04:10.510 --> 04:10.770
Right.

04:10.780 --> 04:17.440
But I personally like to do it this way because it fits like I met through a Scud doll, if you will.

04:17.460 --> 04:23.110
You know, I packets, vitamins, our frame, the segment fits into the data and so on.

04:23.110 --> 04:23.310
Right.

04:23.580 --> 04:24.210
I just like it.

04:24.210 --> 04:24.930
Do it this way.

04:25.170 --> 04:29.670
But here is how the actual IP packet looked like.

04:30.120 --> 04:31.440
Scary, isn't it?

04:31.770 --> 04:36.900
So this is how it actually looks like, you know, the IP packet itself and these are the references

04:36.900 --> 04:42.290
you can use that at this DA of C of the IP protocol, you know, that are broken.

04:42.300 --> 04:47.250
This is the Wikipedia that explains, you know, have a summary of all that stuff.

04:47.880 --> 04:49.140
What are we looking at here?

04:50.310 --> 04:59.100
This is, you know, horizontally from 0 to 31 is that is is four bytes, you know, so this is a bits

04:59.100 --> 05:01.110
a bits, Airbus air bits.

05:01.560 --> 05:03.690
You know, this is how it's organized.

05:03.810 --> 05:10.530
So four bytes and the first all four bytes and the second row for Biden, the third row for Biden in

05:10.540 --> 05:13.920
the fifth row and for Biden on the final one.

05:13.920 --> 05:21.480
So if you multiply by four by five rows, that gives you 20 bytes that we talked about.

05:21.600 --> 05:24.840
So this is the options and this is determined by the Internet headline.

05:24.850 --> 05:26.040
We're going to talk about it in a minute.

05:26.520 --> 05:31.410
By default, this is five which which explains these five bytes, you know, by four rows.

05:31.650 --> 05:36.270
And if it goes more than that, then that will define the length of the options effectively.

05:36.390 --> 05:38.370
And this goes up to 60 now.

05:38.370 --> 05:42.030
We'll get to talk about it so we can add stuff to these options.

05:42.030 --> 05:43.200
You know, and this is good.

05:43.950 --> 05:50.760
Those guys, whoever it to find the IP protocol, they defined it in a way to make it extensible.

05:51.150 --> 05:57.390
Unfortunately, from what I read is some writers effectively block the options for some reason, you

05:57.390 --> 05:59.790
know, because it's dangerous or whatever.

06:00.090 --> 06:02.280
So this is sometimes getting blocked.

06:02.280 --> 06:05.160
You know, that's the sad thing about the Internet.

06:05.190 --> 06:10.020
Not everybody follows the rules and as a result, you don't get predictable.

06:10.020 --> 06:16.950
So otherwise I go back in and I would have definitely use the IP packet to, to sneak in data, my own

06:16.950 --> 06:18.390
data in the packet itself.

06:19.020 --> 06:20.640
Imagine that how cool this is.

06:20.940 --> 06:27.830
You know, we always build on top of, you know, protocols on top of TCB, on top of DB to we build

06:27.840 --> 06:32.760
protocols on top of protocols and we forget how that this is available for us.

06:32.970 --> 06:38.670
You know, as programmers we can write a packet and we can send options, right?

06:39.160 --> 06:39.930
Unfortunately.

06:40.240 --> 06:43.560
What do you guarantee that these options are arrived safely?

06:44.280 --> 06:44.790
I don't know.

06:44.790 --> 06:46.040
Apparently not.

06:46.050 --> 06:48.930
You know, because these options sometimes are dropped.

06:49.110 --> 06:52.380
But it's pretty cool if you think about it.

06:53.040 --> 06:58.320
I don't know if these are user said or not, but regardless, this is the data portion we talked about.

06:58.320 --> 07:03.300
This goes up to 65 kilobytes, you know, 64 kilobytes to be specific.

07:03.930 --> 07:06.450
Know and let's go through this version.

07:07.260 --> 07:09.960
What's the version of this is either four or six?

07:09.960 --> 07:12.300
We don't have are versions of the IP protocol, right.

07:12.750 --> 07:15.150
So this is either for a specific bed.

07:15.150 --> 07:21.720
So we have zero one, two, three, you have four bits to describe that little bit of an overkill if

07:21.720 --> 07:22.410
you think about it.

07:22.410 --> 07:22.650
Right.

07:22.830 --> 07:23.340
Four bits.

07:23.480 --> 07:26.010
How much is that is that's 16 numbers.

07:26.250 --> 07:26.580
Right.

07:27.000 --> 07:27.630
Because to the bar.

07:27.630 --> 07:28.050
Eight.

07:28.290 --> 07:29.430
Exactly, 15.

07:29.890 --> 07:30.240
Right.

07:31.200 --> 07:31.980
That's a lot.

07:32.610 --> 07:37.530
So they embedded like hey, we will go up to version 15 of the IP protocol.

07:37.890 --> 07:45.060
But sadly these bits are never used, you know, because we only use for our six and now so we never

07:45.290 --> 07:46.260
lose the other bits.

07:46.260 --> 07:48.690
So it's a waste, but that's what we have today.

07:50.400 --> 07:51.450
Internet header length.

07:51.450 --> 07:52.230
We talked about this.

07:52.230 --> 07:57.150
This defines how long is the options and by default IDL is five I believe.

07:57.300 --> 07:57.630
Right.

07:57.930 --> 08:01.830
And you can add more say okay, I need 20 bytes.

08:01.840 --> 08:02.190
Right.

08:02.430 --> 08:07.830
Of options and that will in there will allow the router to read the options or not.

08:07.830 --> 08:15.600
If this is five, it will read one, two, three, four, five will read this five rows if you will.

08:15.600 --> 08:16.620
And the total length.

08:17.190 --> 08:17.490
Right.

08:17.760 --> 08:21.060
This describes the total long of the whole thing.

08:21.060 --> 08:23.130
You know, this includes the data and the header.

08:23.550 --> 08:27.210
So and this is extreme, but as we talked about, so eight plus eight.

08:27.780 --> 08:37.530
So you can go up to two to the power, uh, 16, which gives you the 65,000 bytes and that describes

08:37.530 --> 08:40.920
not just the data just above the whole header which is could be 20.

08:41.370 --> 08:46.620
You know, I do the, do the math 22 up to 60 based on the options if you have options there.

08:46.980 --> 08:53.700
But yeah, fragmentation, this is really a powerful concept.

08:54.390 --> 08:58.200
Sadly, this is very hard to get right.

08:58.560 --> 09:07.500
And from what I know, most implementations actually uh uh, are frowned upon.

09:07.500 --> 09:08.750
Fragmentation quick.

09:08.870 --> 09:16.940
Give us a good example at a quick every packet and quick the protocol, you know, disables IP fragmentation

09:16.940 --> 09:22.620
because it causes so all sorts of things, you know, because now if the packet is so large, what is

09:22.620 --> 09:22.660
the.

09:22.670 --> 09:24.410
Well, let's talk about the fragmentation really.

09:25.010 --> 09:26.120
We talked about empty.

09:26.120 --> 09:28.460
You write the the maximum transmission unit.

09:28.550 --> 09:28.850
Yeah.

09:29.510 --> 09:32.020
And you don't really need this.

09:32.020 --> 09:33.290
So again, talk about it right here.

09:33.890 --> 09:38.330
So we talk about them to you write the maximum transmission unit, which is the frame size.

09:38.990 --> 09:42.200
And we talked about the IP packet by default.

09:42.200 --> 09:46.550
The IP affected IP package should fit nicely into a single frame.

09:48.150 --> 09:54.750
And if it doesn't fit, that means if the IP packet is large for some reason, let's say the empty was

09:54.750 --> 09:58.560
1500 and the IP Beckett is 2000.

09:59.580 --> 10:01.440
Then that is called.

10:02.830 --> 10:03.810
You have two options here.

10:04.590 --> 10:06.510
The IP package won't fit in the frame.

10:06.630 --> 10:07.350
You have two options.

10:08.070 --> 10:10.890
You can either tell the client whoever sent this Beckett.

10:11.250 --> 10:13.530
Hey, MTU you two too small.

10:13.530 --> 10:16.440
I can fit this large packet that you sent in.

10:16.440 --> 10:19.050
In that empty you fail.

10:19.320 --> 10:20.610
It will send a message.

10:21.030 --> 10:22.140
How does it send a message?

10:22.170 --> 10:23.880
We talked about the ICMP protocol.

10:23.880 --> 10:29.340
That Internet controller message protocol messages are sent through this protocol ping trace allowed

10:29.340 --> 10:35.370
things like that through the IP vehicle will say, Hey, I can throw this back at a still large write.

10:36.300 --> 10:39.570
That is only if you said that don't fragment bit but.

10:40.720 --> 10:41.770
The other option is.

10:44.460 --> 10:44.970
Fragment.

10:44.970 --> 10:45.360
This thing.

10:45.780 --> 10:46.600
The IP packet.

10:47.160 --> 10:47.850
2000.

10:47.970 --> 10:52.470
All right, let's put 101 frame and the 500 goes to another frame.

10:52.470 --> 10:57.870
So you have one IP packet that had been fragmented into two frames.

10:58.320 --> 11:01.200
So those frames will be sent as two frames.

11:01.290 --> 11:05.130
So one packet two frames, the two frames will arrive.

11:05.250 --> 11:05.730
Guess what?

11:05.760 --> 11:06.090
None.

11:06.180 --> 11:07.380
Not necessarily in order.

11:07.590 --> 11:13.500
So the host has to understand that this frame belongs to a something that was fragmented and tried to

11:13.500 --> 11:14.070
assemble.

11:14.070 --> 11:17.490
So there is assemblage that needs to require assembly.

11:17.490 --> 11:19.800
The fragment is one of the most dangerous things.

11:20.280 --> 11:20.640
Right.

11:20.640 --> 11:21.600
Security wise.

11:22.380 --> 11:29.790
And just because people can fake fragmentation, you know, and then I won't go into details on this,

11:29.790 --> 11:33.630
but plus it's its cost that is on the whole site.

11:33.990 --> 11:36.780
So you can fragment if you want.

11:37.140 --> 11:37.380
Right.

11:37.380 --> 11:38.370
And this is how you do it.

11:38.370 --> 11:39.240
We're going to talk about it.

11:39.480 --> 11:46.050
But if you do understand the consequences, one frame might fail.

11:46.050 --> 11:47.220
You have to rescind it.

11:47.220 --> 11:49.680
And how do you send just part of the fragment?

11:50.460 --> 11:51.630
It's very complicated.

11:51.650 --> 11:54.360
And that's why the protection you know what?

11:55.140 --> 11:56.460
Let's not let's not fragment.

11:56.460 --> 11:56.910
Let's not.

11:57.600 --> 12:01.800
Hey, if you don't fit into our frame, just fail.

12:01.950 --> 12:09.000
So that's the responsibility of the client to send back it, that they know this should fit and all

12:09.000 --> 12:11.770
the empty use that the network will pass through.

12:12.510 --> 12:13.290
Back to the slides.

12:15.950 --> 12:17.330
Well, actually, I kind of like this, huh?

12:17.510 --> 12:19.820
Yeah, because there's nothing here, so.

12:19.820 --> 12:21.800
Yeah, well, the ID.

12:22.190 --> 12:24.050
This is the idea of the fragment.

12:24.050 --> 12:26.680
So if you have one packet that a fragment into four.

12:26.780 --> 12:33.410
So this is one, two, three, four, effectively write the ID of the frame flags like, hey, should

12:33.410 --> 12:35.930
I fragment or should I not fragment?

12:36.350 --> 12:42.470
So this is a flag that literally tells the client whether they're out there or not.

12:43.310 --> 12:49.970
Am I supposed to break this big packet if the empty is too small or not?

12:50.330 --> 12:56.270
So if there is a def, I believe here a flag will say, okay, you can, you can, you can fragment.

12:56.270 --> 13:04.460
The fragmented offset is that 0123 and this is ID, which is the unique identifier of the fragment itself

13:04.580 --> 13:04.880
now.

13:05.600 --> 13:11.390
So the all of these are just usually for a for far off fragmentation jumbo packages.

13:11.720 --> 13:13.470
You can get into this as well, right?

13:13.640 --> 13:17.390
If you have that large IP back, it's effectively time to live.

13:17.390 --> 13:18.830
We're going to talk about this as well.

13:18.860 --> 13:19.130
Right.

13:19.820 --> 13:28.340
Every IP packet has a bit actually eight bits, you know, a single byte that represent a counter.

13:30.540 --> 13:32.040
And this is very interesting.

13:32.340 --> 13:38.670
Before we talk about time to live, we're going to talk about a problem because what do we do in this

13:38.670 --> 13:38.930
course?

13:38.930 --> 13:41.490
We we always ask the question of why?

13:41.520 --> 13:42.900
Why does something exist?

13:43.470 --> 13:46.260
Why do we need to fragment back, as do a lot?

13:46.290 --> 13:47.610
Why do we have time to live?

13:48.720 --> 13:52.230
Because of the idea of routing that we talked about in a while.

13:53.340 --> 13:56.730
The packet can go into different routes.

13:56.760 --> 13:57.060
Right.

13:57.480 --> 14:01.470
And they can end up into a situation where they will go into an infinite loop.

14:01.710 --> 14:04.830
We go to this road, this road, and the cities are out there and there's road.

14:04.830 --> 14:06.090
And then back to the same rather.

14:06.720 --> 14:09.570
And the packet can go infinitely.

14:10.110 --> 14:14.880
And you have no idea if you visit this because the routers are not stateful, you know, they don't

14:14.880 --> 14:16.050
save the state.

14:16.050 --> 14:22.200
IP protocol is stateless, you know, they don't save the state of that protocol.

14:22.380 --> 14:28.980
Like, Oh, this package was visited before, unlike the layer layer for where we have states, we have

14:28.980 --> 14:30.240
session, we have all that stuff.

14:30.240 --> 14:34.560
IP is just stateless, no IP packets just passing through, so we don't know.

14:34.560 --> 14:40.830
State So how do I prevent packets from roaming around the internet forever?

14:41.550 --> 14:50.190
Me Time to live TTL You When you send a packet you say, okay, I estimate that this package will live

14:50.190 --> 14:51.960
for 100 routes.

14:52.440 --> 14:54.030
All right, so we put 100 year.

14:55.730 --> 14:56.900
As they go.

14:58.430 --> 15:02.780
This packet goes from you, it reaches the host.

15:02.990 --> 15:06.620
You know that gateway, of course, if you're sending it to the Internet, will go to your gateway,

15:06.620 --> 15:07.370
which is your router.

15:08.180 --> 15:10.580
The router will do minus one to the packet.

15:10.580 --> 15:18.110
So well that the IP packet arrival, the physical layer will be converted to a data link or be converted

15:18.110 --> 15:21.710
to frame the frames right will be converted to them.

15:21.710 --> 15:25.820
IP packets, you know one frame, let's assume simplicity.

15:25.820 --> 15:29.010
One frame goes into a single IP packet, that's biscuits.

15:29.030 --> 15:29.450
In audio.

15:29.810 --> 15:32.330
We have the IP packet and the router takes that.

15:32.330 --> 15:36.530
I'll be back and take the time to live decrement by one and send it again.

15:36.710 --> 15:43.640
So it goes back to the RSA model and goes off to the internet and every one of the writers and hosts

15:43.640 --> 15:48.530
that sees this packet decrements it, that's the responsibility, that's the whole contract.

15:48.890 --> 15:55.850
This way we kind of add the state right to the packet, you know, if have your program before the,

15:55.850 --> 16:01.280
you know, the cons of stateless versus def or stateless, we have to send that information with that

16:02.300 --> 16:04.600
with the request right there.

16:04.610 --> 16:05.990
Of course, in this case the IP packet.

16:05.990 --> 16:07.430
Right, send it with it.

16:07.430 --> 16:12.440
So the state always follows the data itself now and instead of saving it in the host.

16:12.440 --> 16:12.740
Right.

16:13.400 --> 16:22.100
So now if this time to have reached zero, whoever they come into the to zero must stop, you know,

16:23.210 --> 16:29.540
must drop the packet and must send back and ICM P message ICMP shows again.

16:29.570 --> 16:31.640
That's why I explained it very critical.

16:31.910 --> 16:38.720
The ICMP protocol shows up again so they a packet timeout, whatever.

16:38.960 --> 16:44.150
No, I don't remember that exact message and we'll say it, we'll send it back to whomever.

16:45.380 --> 16:47.480
Was that the source IP address.

16:47.990 --> 16:50.300
And that is exactly how traceroute works.

16:50.870 --> 16:52.970
Throw out works or router route.

16:53.600 --> 16:54.080
Same thing.

16:54.920 --> 17:00.620
Trace it out or traceroute you know I believe the the British call the router.

17:00.860 --> 17:01.220
Yeah.

17:01.220 --> 17:05.390
So routers you know the routers right.

17:05.600 --> 17:07.460
Will decrement that until it reaches zero.

17:07.460 --> 17:10.970
And there's a message to the sources said hey there's done.

17:11.150 --> 17:13.310
So the trace road actually does it this way.

17:13.340 --> 17:17.090
It will set a very small time to live and it will incremented.

17:17.450 --> 17:22.250
And every time we pass a hop, we reach the next hop.

17:22.760 --> 17:26.870
That router will tell us about its source IP address.

17:27.050 --> 17:30.170
So we know effectively we trace the entire road.

17:30.590 --> 17:35.120
Obviously some routers disable ICMP altogether, some firewalls disable ICMP.

17:35.540 --> 17:39.590
And if that is the case, that's where you get the dot, dot, dot, dot and trace it out.

17:39.860 --> 17:43.100
You cannot to basically trace it in that particular case.

17:43.730 --> 17:46.460
So that's down to that very, very important concept.

17:46.670 --> 17:49.010
How many hops can this packet survive?

17:49.310 --> 17:52.310
And this is usually 128 number or whatever.

17:52.550 --> 17:58.640
You set it as a large number, not too large, because eventually the packet will live for a long time.

17:58.640 --> 18:02.240
No, I believe that whatever the default number is enough.

18:02.390 --> 18:10.760
If you see your packet takes more, maybe longer path and they are dying, maybe the client will increase

18:10.760 --> 18:16.070
that number protocol and we they of saying what we we know we are in the IP address.

18:17.330 --> 18:22.100
No this is the protocol of what is the content that is inside this data.

18:22.220 --> 18:28.970
Now I always find this when I first saw this is like why that's kind of moot.

18:29.990 --> 18:33.380
I have to define the protocol and you have to know my protocol.

18:33.770 --> 18:35.300
I want to send the strand of data.

18:35.300 --> 18:36.740
Doesn't have to be a protocol.

18:36.950 --> 18:38.310
I want to invent my own protocol.

18:38.310 --> 18:41.210
Are you going to block me then?

18:41.660 --> 18:43.820
I thought about this, right?

18:44.150 --> 18:47.750
I say, Hey, just read the data and figure out the protocol.

18:47.930 --> 18:49.340
That's why that's what.

18:49.520 --> 18:51.500
That's the first thought that came to my mind.

18:51.710 --> 18:56.510
Why do you need an extra eight bits waste, you know?

18:57.140 --> 18:58.270
And then I thought about this.

18:58.880 --> 18:59.510
You know what?

19:00.740 --> 19:01.880
It's actually a good idea.

19:02.360 --> 19:05.990
This way the Raptors don't have to pass the entire data.

19:06.260 --> 19:13.190
They can just read that 20 bytes header and immediately figure out what is inside this and whether they

19:13.190 --> 19:15.350
should pull the data or not.

19:15.650 --> 19:18.140
You know, that's ingenious effectively.

19:18.290 --> 19:19.640
We always do this.

19:19.730 --> 19:27.890
You know, this method takes animated data to save performance and obviously it's probably decided to

19:27.890 --> 19:30.250
block or want to do anything else.

19:30.260 --> 19:31.460
You can just read this protocol.

19:31.820 --> 19:38.330
So our protocol could be ICMP is part of a would that it does this DCP or other UDP whatever the content

19:38.330 --> 19:40.700
of the IP, the IP data itself.

19:41.120 --> 19:42.290
That's the protocol here.

19:42.320 --> 19:44.810
There's a list and and Wikipedia.

19:44.840 --> 19:51.130
But if I can share it as well, showing you over a single protocol that for example, unspecified,

19:51.380 --> 19:54.560
I think that is like miscellaneous or something like that.

19:54.560 --> 19:56.090
You can put all that stuff here.

19:56.210 --> 19:58.520
There's there's obviously a big eight bit.

19:58.520 --> 19:59.420
So how many do we have?

19:59.750 --> 20:04.190
You can have up to 255 protocols, but that's it.

20:05.870 --> 20:07.280
Source on destination IP.

20:07.670 --> 20:12.140
By far the most important pieces of metadata here to the header.

20:12.590 --> 20:15.290
Where are you going and where are you coming from?

20:15.560 --> 20:17.600
Very important piece of information.

20:18.020 --> 20:22.310
Everybody can fake source IP errors, you know, you can try.

20:22.340 --> 20:26.510
That's why it's like, okay, all my IP address has been spoofed.

20:27.050 --> 20:32.050
You know, I hear a lot of people, it's like it's like, oh, this is not this.

20:32.750 --> 20:35.000
We've seen your IP address on our forums.

20:36.410 --> 20:38.220
No, that was not me.

20:38.240 --> 20:40.160
My IP address was spoofed.

20:40.850 --> 20:41.570
I was like, Yeah.

20:41.600 --> 20:44.090
Like, spoofing is something easy to do, huh?

20:45.200 --> 20:47.860
Spoofing is the idea of changing the source.

20:47.900 --> 20:54.530
Every packet that you send right from your machine, you effectively change the source IP address to

20:54.530 --> 20:55.280
be something else.

20:55.640 --> 20:56.860
You can do that, right?

20:57.290 --> 20:58.280
But guess what?

20:58.700 --> 21:02.510
Your ISP, the packet, the IP will go through the browser.

21:02.510 --> 21:05.060
Then the first router, it hits the major router.

21:05.060 --> 21:06.710
What is what's what's the first major?

21:06.710 --> 21:13.790
Rather it's your ISP because that's your link to the internet and it will say say hey, my source IP

21:13.790 --> 21:19.560
address actually whatever that guy, you know, you can put any number you want, you can you can write

21:19.560 --> 21:20.990
that simple code that do that.

21:20.990 --> 21:23.980
Does that rewrite every single IP packet?

21:24.680 --> 21:25.000
Right.

21:25.220 --> 21:30.740
The source IP would be something else, but your ISP, ISP will call you out like, wait a minute,

21:30.800 --> 21:32.300
that's not your source IP address.

21:32.330 --> 21:34.310
I know your IP address.

21:34.340 --> 21:35.630
I assigned it to you.

21:35.990 --> 21:37.760
So your ISP actually blocks it?

21:38.300 --> 21:40.960
No, you cannot do that unless.

21:41.310 --> 21:45.470
Unless every single Internet provider will have this block.

21:45.470 --> 21:47.060
You know, you cannot spoof anymore.

21:47.060 --> 21:53.000
You know, it's not easy to spoof IP addresses, you know, unless you build your own ISP, which is

21:53.000 --> 21:54.320
I don't think it's impossible.

21:54.320 --> 21:55.040
You can do it.

21:55.160 --> 22:00.470
And then you run your own Espoo, pay money to link yourself to the internet.

22:00.470 --> 22:02.120
Yeah, you can spoof all you want that.

22:02.540 --> 22:06.800
But even if you spoof, then how, how would you get responses back?

22:06.800 --> 22:10.280
Because that's what is used to the responses, you know.

22:11.390 --> 22:17.240
So yeah this the nation IP is where are you going source is where you're coming from very critical and

22:17.240 --> 22:24.500
these are, as we talked about four bytes because this is what this is the IPV four write explicit congestion

22:24.500 --> 22:25.040
notification.

22:25.040 --> 22:28.700
We're going to talk a bit about this more on the TCP IP section.

22:29.270 --> 22:35.990
But this bit is effectively is is from an A, so from a lower layer upon layer from an upper layer.

22:36.230 --> 22:45.440
This bit is set by that outer and this is what it means, explicit congestion notification before we

22:45.440 --> 22:47.930
talk about acceptable congestion notification.

22:49.840 --> 22:53.960
And again, we're talking about this in details and the future, but it doesn't hurt to talk about it.

22:54.130 --> 23:01.170
Now, congestion is when packets start to drop you.

23:02.080 --> 23:05.530
I.B. packets will be arrived at routers like floods.

23:05.530 --> 23:07.610
You know, everybody sending data.

23:07.630 --> 23:10.180
Everybody I am as I speak, I'm sending data.

23:10.420 --> 23:11.200
This is not Life City.

23:11.210 --> 23:12.130
But you get the point.

23:12.220 --> 23:18.700
And if you playing this, packets are coming through routers, you know, at the end of the day routers

23:18.850 --> 23:23.650
to process this because they need to send thin amount of memory called the buffer to put the packets

23:23.650 --> 23:26.620
in this memory fills up.

23:27.130 --> 23:33.010
If that fills up, if you have too many packets or your router is slower like it does a lot of stuff

23:33.010 --> 23:33.760
to pass.

23:34.510 --> 23:36.790
More work means more time.

23:36.790 --> 23:43.240
More time means queue will go longer and the buffer will fill and the buffer fills.

23:43.810 --> 23:45.550
That means you cannot accept more packets.

23:45.830 --> 23:48.190
That means you have to drop incoming packets.

23:48.190 --> 23:52.210
Any packet that comes the controller of the browser will drop the packet.

23:52.510 --> 23:55.840
And when that happens, that indicates something called congestion.

23:55.840 --> 24:02.320
That means, hey, the network is congested or these characters are having a having a hard time processing

24:02.320 --> 24:03.700
packets stop.

24:04.150 --> 24:10.360
So there is a whole solution to congestion control, control the traffic in the Internet, and that's

24:10.360 --> 24:11.380
called congestion control.

24:12.280 --> 24:16.960
For the longest time, routers always drop the packets, they drop the packet.

24:16.960 --> 24:17.650
I don't care.

24:17.830 --> 24:20.950
That's it doesn't even send any message or anything like that.

24:20.950 --> 24:22.570
Just drop it and leave it alone.

24:23.410 --> 24:26.230
You know, it doesn't even send an ICMP message.

24:26.230 --> 24:27.760
I don't think so.

24:27.760 --> 24:29.320
The client have to guess what the.

24:29.320 --> 24:30.040
Okay.

24:30.040 --> 24:31.900
My packet had timed out.

24:31.930 --> 24:33.760
I don't see an acknowledgment.

24:33.790 --> 24:37.240
I'm going to assume it's going as dropped and I'm going to assume congestion.

24:37.240 --> 24:38.050
That's what happens.

24:38.440 --> 24:43.570
It's a waste because that timeout is so long and we're wait.

24:43.810 --> 24:45.580
We need better communication.

24:45.910 --> 24:54.490
Meet explicit congestion notification the router when their buffer fills up because they are IP packets,

24:54.490 --> 24:56.290
they don't deal with layer three packets.

24:56.500 --> 24:57.960
They will take this packet and says.

24:58.930 --> 25:00.310
I'm about to drop this on my bucket.

25:00.310 --> 25:01.020
It's fall.

25:01.030 --> 25:01.840
But wait a minute.

25:01.960 --> 25:05.110
I'm going to actually I'm going to actually not drop it.

25:06.160 --> 25:08.320
My puffer is about to fill.

25:08.800 --> 25:11.380
I know I'm going to fill is in.

25:11.380 --> 25:12.670
Said the bit to one.

25:13.000 --> 25:13.270
Right.

25:13.270 --> 25:13.720
Whatever.

25:13.730 --> 25:16.360
Said it to true boom notification.

25:16.930 --> 25:19.510
I'm about to get filled and then it will actually process.

25:19.900 --> 25:26.830
So the receiver will see that bit that oh oh someone actually some of the routers experience congestion.

25:27.190 --> 25:31.690
I better tell the, uh, I better tell the receiver.

25:31.740 --> 25:36.580
And so the TCP layer takes control as we experience congestion.

25:37.030 --> 25:42.940
And then the client will start communicating at the higher levels of the TCP transport layer as again,

25:42.970 --> 25:43.970
we experience congestion.

25:44.080 --> 25:51.130
So the beauty here is with this small change, we manage to notify the both the client and the server.

25:51.670 --> 25:52.000
Right?

25:53.170 --> 25:55.720
The server will reply back to the lines with the same bit.

25:55.720 --> 26:02.650
So everybody will know eventually and and they just manage to know that there is congestion without

26:02.650 --> 26:03.730
any packets getting up.

26:04.090 --> 26:05.110
Beautiful design.

26:05.770 --> 26:10.840
I absolutely love how elegant such small to bits can do.

26:11.020 --> 26:11.130
Right.

26:11.200 --> 26:13.340
And and to be honest, I don't know why do we have to go bits right?

26:13.450 --> 26:16.120
We can go into more details, but this is the gist of it.

26:16.810 --> 26:17.470
Beautiful.

26:17.470 --> 26:19.480
I absolutely love this stuff.

26:19.840 --> 26:27.010
You know, we can learn so much as back in India from these elegant designs, you know, because we

26:27.010 --> 26:36.220
waste so much when we build applications, do we build all sort of you know, we allocate arrays like

26:36.580 --> 26:43.480
thousands and thousands of by Jason bloated Jason we duplicate keys all around.

26:43.720 --> 26:46.930
We took duplicate responses from the database.

26:46.930 --> 26:48.670
We put it everywhere.

26:48.670 --> 26:50.650
We send information we don't need.

26:50.920 --> 26:59.410
So all of this stuff really hurts me when I see a response from an API that that we just got back up,

26:59.410 --> 27:02.860
you know, we send the same value over and over again.

27:03.520 --> 27:05.230
These kind of things makes me crazy.

27:05.230 --> 27:13.780
You know, back in the old days, they had a limit to work with and they appreciate this limit today.

27:14.590 --> 27:18.220
Engineers, we don't have a limit from what?

27:18.220 --> 27:19.750
Islam I don't care.

27:19.750 --> 27:22.900
I have 700 gigabyte ram.

27:23.230 --> 27:24.430
I don't care.

27:24.430 --> 27:30.730
Let me I look at everything I want and unfortunately we lost that, you know, source of scarcity.

27:31.660 --> 27:37.270
This is just me ranting and that's pretty much this is the most important thing that I like to explain

27:37.300 --> 27:40.150
and when it comes to the header that I've ever had.

27:40.360 --> 27:40.720
All right.

27:41.020 --> 27:43.210
How about we summarize this IP packet?

27:43.210 --> 27:51.940
The IP packet is one of more elegant, you know, uh, anatomy that is, you know, the packet has headers,

27:51.940 --> 27:56.380
it's 20 bytes can go up to 60 if you have options and it is enabled.

27:56.650 --> 27:59.830
Data Section Guide Go to a 65,000 bytes.

28:00.370 --> 28:06.880
I never seen such such IP back of that lot because there is no empty you that fits it.

28:06.880 --> 28:12.370
First of all, you know, you can argue that hey, 16 bit is actually too much, but you never know.

28:12.730 --> 28:19.570
Maybe an Amazon cloned a cloud, Amazon Cloud or Microsoft Azure or Google.

28:19.750 --> 28:25.960
They build their own network and really with a large MTU that can effectively be 65,000.

28:25.960 --> 28:26.530
Who knows?

28:26.680 --> 28:28.450
They don't share this information with us.

28:28.690 --> 28:36.700
So if you have that such a large frame, you can send one IP, large IP backwards and then it fits it

28:36.700 --> 28:37.630
in a single frame.

28:37.630 --> 28:39.910
Now, I don't know the limitations of that.

28:40.120 --> 28:42.330
What can what can go wrong with that?

28:42.330 --> 28:46.180
It probably people will try to, but definitely will decrease the latency.

28:46.630 --> 28:46.930
Right.

28:47.410 --> 28:53.710
If you have your own network that all of these devices live tightly high bandwidth network I'm not going

28:53.710 --> 29:00.520
to the Internet is just between me it's on my own back in the database connect to the to the back in

29:00.520 --> 29:10.630
application all they are I don't know a hundred gigabit Ethernet and I'm to use 65 K to use and I'm

29:10.630 --> 29:11.410
going to use that.

29:12.160 --> 29:14.140
Sure you're not going to the Internet.

29:14.140 --> 29:18.370
So this is tightly local area network.

29:18.370 --> 29:21.640
So you're optimizing the heck out of everything.

29:22.000 --> 29:23.710
So I'd like to see this one day.

29:24.010 --> 29:29.260
So if someone ever, if there is an article, some wild love to read, someone actually taking advantage

29:29.260 --> 29:31.990
or if there is any limitation comes to empty use sizes.

29:34.270 --> 29:39.610
We talked about packets need to be good fragmented if it doesn't fit a frame unless you set the bed

29:39.610 --> 29:44.590
that says Hey, don't fragment the fly that we talked about, hey, don't fragment.

29:44.590 --> 29:50.410
And if you don't fragment, then if the package is too large for them to you, we fail, we drop the

29:50.410 --> 29:55.270
packet and we tell the client that, Hey, we couldn't fragment your stuff because you told us, don't

29:55.270 --> 29:55.750
fragment.

29:55.770 --> 29:55.980
Right?

29:56.530 --> 29:57.900
And that's where ICM.

29:58.640 --> 30:02.800
Uh, actually, this is where a black hole connection can happen.

30:02.810 --> 30:04.430
We're going to talk about this as well in the future.

30:05.120 --> 30:08.090
Black hole, TCP connection, Google that, right.

30:08.180 --> 30:09.230
That was the IP packet.

30:09.350 --> 30:09.560
How?

30:09.560 --> 30:11.290
I'm moving to the next lecture.





## ICMP, PING, TraceRoute 

## ARP 

## Capturing IP, ARP and ICMP. Packets with TCPDUMP 

## Routing Example 

## Private IP address (Alaska airline WiFi Example)

# User datagram protocol (UDP)

## What is UDP? 

## User datagram structure 

## UDP Pros & Cons 

## UDP server with Javascript using NodeJS 

## UDP server with C 

## Capturing UDP traffic with TCPDump 

# Transmission Control protocol (TCP)

## What is TCP ?

## TCP Segment 

## Flow Control 

## Congestion Control 

## Slow start vs Congestion Control 

## NAT 

## TCP connection states 

## TCP Pros and Cons 

## TCP Server with Javascript using NodeJS 

## TCP Server with C 

## Capturing TCP Segments with TCPDUMP 

# Overview of popular Networking protocols 

## Networking protocol Introduction 

## DNS 

## TLS 

# Networking concepts that affect the backend performance 

## What is this section?

## MSS vs MTU vs PMTUD 

## Nagle's algorithm Effect on performance 

## Delayed acknowledgement effect on performance 

## Cost of connection establishment 

## TCP Fast open 

## Listening Server 

## TCP Head of line blocking 

## The importance of proxy and reverse proxies 

## Load Balancing at layer 4 vs Layer 7 

## Network Access Control to Database Servers 

## Networking with Docker 

# Analyzing protocols with Wireshark 

## Wiresharking UDP 

## Wiresharking TCP/HTTP 

## Wiresharking HTTP/2 (Decrypting TLS)

## Wiresharking MongoDB 

## Wiresharking Server send events 

# Answering your questions 

## Should Layer 4 proxies buffer segments ?

## How does the Kernel manage TCP connections?

# Course summary 

# Extras 

## Exposing local servers publicly 

## The networking behind clicking a link 

## What is SNI (Server Name Indication TLS Extension)?

## Replacing TCP for Data centers (Part 1)

## Replacing TCP for Data centers (Part 2)
	
## Replacing TCP for Data centers (Part 3)
