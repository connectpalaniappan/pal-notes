---
tags:
 - people/pal
 - date/2024-03-18
---

# Agenda

![Screenshot 2022-12-26 at 7.25.54 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f9e77d1-c68b-4b23-9af7-7137a62ea587/Screenshot_2022-12-26_at_7.25.54_AM.png)

- How CDN works?
    - we’ll see how simple it is to build one but how difficult it is to scale it in production
    - we’ll realize that there are 7-8 concepts in CS around which everything is built
    - wherever it comes to B2C applications (ShareChat, FB, Instagram, Cricbuzz, etc.), CDN plays a really important role

# Instagram’s Year 1 Architecture

![Screenshot 2022-12-26 at 7.42.37 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8a1ab49-9d4e-47b4-8900-141b9b67ecb6/Screenshot_2022-12-26_at_7.42.37_AM.png)

## Why

- The field of s/w engineering is a sinusoidal wave - sine wave. Every few years, there comes a new revolutionary company that scales a lot with much fewer engineers than before. Then, everyone looks up what they did and tries to exactly replicate that.
    - e.g. 2006-08 FB started gaining a lot of transactions. From 2008 to 2012, almost all the applications that were built would use PHP as their backend, memcached as their cache, and MySQL as their DB (FB’s stack)
    - in 2011, Instagram shook the world as in just 1 yr, they had 14 million users and they were managing with just 3 engineers. People just dream of such a thing. From 2012 onwards, most companies started having the architecture as shown above. The exact tool might change but the components used remained the same.

## What

- Components
    - One monolith in Django
    - Nginx - frontend proxy (most likely, this means that request for static files is served directly by nginx and the API requests are forwarded to Django)
    - [Celery](https://www.fullstackpython.com/celery.html) - asynchronous task management
    - NoSQL DB - Cassandra
    - 1 PostgreSQL DB - for transactions
    - Memcached - normal caching
    - Redis - for advanced data structures (e.g. leaderboards, bloom filters, etc.)
    - RabbitMQ - message broker for delegation through Celery
- Everything is horizontally scalable, communication, delegation, caching, DBs - all the components of a system have been addressed
- Some parts of this were taken from FB instead of having reimagined everything from scratch

## Key takeaways

- We are due for another revolutionary company coming in with a new tech stack as it has been around 10 years since Instagram revolutionized (nothing pathbreaking has come out since)

<aside> 💡 Keep an eye out for different kinds of tech stacks, and see what you can learn from them and how they might be applicable to your own tech stack as everything is a pattern!

</aside>

# How CDN works

## Why?

- Whenever you’re building a B2C application, CDN is the way to give the user a perceived performance
    - The user should feel that the application/website is loading very quickly but behind the scene, it is all CDN
    - e.g. Hotstar, live streaming - the credit for the live streaming part should go to folks like Akamai and Cloudflare. The Hotstar team should get the credit for ensuring that the DB doesn’t crash.
- As an engineer, we should be thinking about how these things work!
- Now, most companies are cloud-native - they are hosted on either AWS, Azure, or GCP. But before 2015, a lot of companies had to build their own infra. However, today, because of the cloud providers, a lot of services are offered as managed services that we can directly leverage (and almost always should) instead of reinventing the wheel (there might be a rare use-case where you might have to build your own CDN as opposed to using a managed service offering for a CDN).
- So, there will be an emphasis on how to practically leverage these existing solutions in this class.

## What?

![Screenshot 2022-12-26 at 8.12.22 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12ce715e-af48-4931-a272-1e01718894cf/Screenshot_2022-12-26_at_8.12.22_AM.png)

- CDN is just a cache - not a magical solution that can do anything - that sits between your user and the origin (e.g. API server, S3 bucket, etc.)
- In the past, we’ve spoken about caching (how Redis is put in front of our DB, we check if the data for a query can be found in Redis, if not we fetch it from the DB and cache it in Redis, etc.). CDN does something very similar.
- CDNs represent a host of servers distributed across the world, including servers closer to your user.
    - If a user requests some data, the request first comes to the CDN.
    - If the CDN has that data, it just returns the data!
    - If it doesn’t have that data, the CDN makes a request to the origin server to fetch that data, it caches the data and returns the response.
    - The next time that another user requests that same data, it simply returns that data from its cache.
- Origin: Just an endpoint configured on CDN
- When we configure a CDN, it gives us a URL against which we have to configure a origin, which should also be a URL. This is the bare minimum configuration that we need to do on a CDN.

## Example

### Setup

![Screenshot 2022-12-26 at 9.08.18 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7baf1a93-79e4-4759-9aca-4a17035c09fb/Screenshot_2022-12-26_at_9.08.18_AM.png)

- Now, there is a mapping from the CDN URL to the origin endpoint URL
    
- When a user wants to fire an HTTP request, a Domain Name Resolution happens on the domain the user has invoked, which returns an IP address. Then, the user’s machine connects to that IP address and fires the request, etc.
    
- Suppose an image is hosted at the URL below:
    
    ![Screenshot 2022-12-26 at 9.12.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4511173c-e494-4b30-b587-d0e6eb30f78d/Screenshot_2022-12-26_at_9.12.04_AM.png)
    
- If we add this URL inside an `<img>` tag, to load the URL a request would go to `[arpitbhayani.me](<http://arpitbhayani.me>)` which is hosted on some AWS/Netlify, etc. server. as the domain name resolution would return the IP address associated with [arpitbhayani.me](http://arpitbhayani.me)!
    
- Suppose, the website is hosted in the Mumbai region. When the domain name is resolved, it would return the IP address of that Mumbai server.
    

### The problem

- If someone sitting in the US tries to load the URL, it would make a (very expensive) network request across the world, across the cross-Atlantic ocean to the Mumbai data center.

### Enter: CDN

- Can there be an intermediate server closer to the user that has cached the response from the origin of the image so that the request by the user doesn’t have to travel such a long distance?
    
- That is exactly what a CDN does.
    
- Change the domain name from the URL from that of the origin to that of the CDN!
    
    ![Screenshot 2022-12-26 at 9.35.28 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b82bda04-c467-4115-af66-03912558b387/Screenshot_2022-12-26_at_9.35.28_AM.png)
    
- If the data is not available for this request on the CDN, it would replace the CDN URL with the origin URL in the original request URL and make a request.
    
    ![Screenshot 2022-12-26 at 9.36.52 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70fb15ef-bf69-4b99-97f4-d1bb530135bc/Screenshot_2022-12-26_at_9.36.52_AM.png)
    

## The breadth of CDN

- Broadly, the CDN is just caching what the API server is sending. So, there is no reason that this functionality should be restricted to images. The CDN is just caching a stream of bytes.
    
- Thus, people usually think that one can only cache static things like JS bundles, images, etc. But that is not right.
    
    ![Screenshot 2022-12-26 at 9.46.29 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a6b22a4-110d-432d-a122-94bdbac120c3/Screenshot_2022-12-26_at_9.46.29_AM.png)
    
- We can also cache API responses on CDN
    
    - E.g. suppose we have a “Popular searches” service that returns the most popular searches that have happened in the last hour. It only gets updated after every hour.
    - In this case, why would we want the majority of the requests to even hit the backend server? Most of the requests can hit the CDN and directly get the response without even entering our infra or us having to manage all the load.
    - The user gets performance. Our infra doesn’t have to bloat or take up the load. Win-Win for both!
    - Obviously, if the response for the “Popular Searches” has changed, we have to invalidate the cache on the CDN
        1. The CDN exposes the endpoints for the invalidation
        2. Provides other ways to invalidate (e.g. TTL, path-specific TTL, etc.)

<aside> 💡 Thus, CDN actually sits in between the user and your private infra (not just the origin)

</aside>

## Notes

- How does a CDN identify the nearest server for a user? Not covered here as it dives deep into networking (look for Cloudflare blog posts). We are using CDN as a black box.

# Uploading photos at scale

## Context

- On every social media platform, people upload images
- How do we approach enabling image upload at scale?

## Requirements

- 5M photos per day

## Brainstorming

![Screenshot 2022-12-26 at 10.05.17 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74759614-f071-416b-ae17-4fe68d27c96e/Screenshot_2022-12-26_at_10.05.17_AM.png)

### Storage

- Where to store the images?
    - Any blog storage service like AWS S3
    - Why?
        - Because storing the binary data of each image in RDBs doesn’t make sense
        - We can store even very large images in blob storage services like S3
        - They are extremely cheap

### Data flow

- How to actually upload to S3?
    - How is the image sent to our Image Upload API server in the first place?
        - Just a simple HTTP POST request where the binary image data is sent in the payload
        - Then, the server can do whatever it wants with it
    - Once the server starts receiving the binary image data, it keeps storing the image data in a temporary file on the disk (inside the `/tmp` directory) until it has received the entire image data (as the image binary is sent as a multipart form-data)
    - If we want the user to have confirmation that the data has been uploaded to S3, then, the user will need to wait until we make a request to S3 to upload the temporary image file created in the last step and receive a successful response back from S3. Otherwise, we can start uploading the image to S3 in an asynchronous process and immediately send a confirmation back to the user.
- Cons:
    - We are making 2 copies of the image
        - Once on S3 (after the image upload is complete)
        - Once in disk (the temporary file created above, although it will be deleted still, for some time at least, we are maintaining 2 copies)
    - Disk limit
        - If the disk size is 1GB but the file uploaded is a 2GB video, then this approach will fail.
    - Disk I/O?
        - 1 Disk I/O + 1 Network Call to S3
        - however, since it is a local disk write, the disk I/O will be much faster than the network call
    - We are reducing the throughput of the API server + consuming double its bandwidth + high cost
        - Assume that one image is 2MB large, the flow looks like this:
            - The request is sent as packets
            - The server receives them in its RAM (the HTTP body is accessible in RAM).
            - From there, we upload it to S3
        - Thus, we are using twice the bandwidth of the server (`ingress` - incoming request in the form of packets and `egress` - outgoing request to S3)
            - Every cloud provider charges for the amount of data that we are moving - both ingress and egress
            - NOTE: if the server is on AWS and the egress request is also to an AWS service (S3 in this case), the egress cost becomes almost 0
        - Plus, we are storing the 2MB image in memory - 2MB is a huge size.
        - If the server has 4GB RAM, one machine is limited to ~2000 concurrent requests. And if we want to serve 5M image uploads per day, the number of servers required would become huge.
- Pros:
    - The client is unaware of S3
- Can we optimize it?
    - We can compress the image - it reduces the bandwidth
- What about letting the user directly upload to S3?
    - In this case, we’d be making our S3 bucket public and exposing it for anyone to upload anything they want. Then, anyone who gets access to the endpoint can use our S3 bucket as their external hard drive. Thus, security concerns creep in.
        - Suppose a user has uploaded their profile image which has gone to a specific URL. Then, if someone else gets to know the URL of the uploaded image, they can overwrite it.
        - A hacker can download all users’ information
        - Someone can upload their data to our S3 bucket such that our infra cost shoots up and they get free hard disk infinitely scalable.
    - Thus, we need some guard rails on our S3 bucket. Can there be something one-time that we can use that others can’t use so that the S3 bucket is limited in terms of who can upload to it?

<aside> 💡 Important to approach problems from the first principles, think about the next step, hit a roadblock, think about a solution for that, and hit another roadblock, and so on.

</aside>

- We can use a `pre-signed URL` that S3 provides which only gives one-time access to upload to the S3 bucket.
    - The user can make an API call to the Image Upload Service expressing an intent to upload an image
    - The API server can reserve a path on our S3 bucket and generate a signed URL (with a TTL of hardly 1-2 mins). The path is not something that S3 provides us. We specify the path on S3.
    - This pre-signed URL is returned to the client which it can use to directly upload the image to the S3 bucket using a normal HTTP POST call.
    - This way, we have reduced the bandwidth consumption of our Image Upload Service and reduced the load on our infra as the image directly gets uploaded to S3.

![Screenshot 2022-12-26 at 11.37.51 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2f844dab-7ab4-4efc-abda-22b6d3bd5acd/Screenshot_2022-12-26_at_11.37.51_AM.png)

## Demonstration (Github)

- Go to a Github issue
- Start a new comment
- Keep your network tab open and upload an image to the comment (don’t post it)

(refer to the video)

## Privacy

- For a private account on Instagram, even though the link to their post is private, if someone actually has the URL of any image for a private account, that image URL can be accessed by anyone.
- Now, for us to keep images private, we need to serve images through our image service. However, the best way to serve images is through CDN so that our image servers are not overloaded.
- So, how do companies like FB/Insta, etc. handle privacy?
    - They use short-lived certificates
    - Now, there is no authorization layer inside CDN. It does not have access to our DB. It does not know whose account is private and whose account is not. We just pass in a URL to the CDN.
    - Thus, we need a way to specify if the CDN should process a given URL.
    - Instagram (for e.g.) does it by specifying particular query params in the actual image URL that are params for the CDN that it is using which tell the CDN that it should only process the URL if it is within a given small timestamp. Otherwise, it should reject the request.
    - This is how these companies ensure that the image access is (almost) one-time.
    - But it is not truly private.

## Summary

![Screenshot 2022-12-30 at 3.27.24 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ade87da8-a146-45de-84fb-0eafa5ea48e7/Screenshot_2022-12-30_at_3.27.24_PM.png)

![Screenshot 2022-12-30 at 3.27.28 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a81c3a0-0bb7-404f-b9f6-6abf3230181a/Screenshot_2022-12-30_at_3.27.28_PM.png)

- Note, how we store on S3 but we serve it through CDN whose origin URL is the original S3 URL of the image.

![Screenshot 2022-12-30 at 3.28.44 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93c5e290-5e80-425f-bb88-5621a7c8fa09/Screenshot_2022-12-30_at_3.28.44_PM.png)

![Screenshot 2022-12-30 at 3.32.49 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eaeca6a3-84a5-42ea-bff4-5b225fdf5d9e/Screenshot_2022-12-30_at_3.32.49_PM.png)

- Here, the image service returns a pre-signed URL and user A makes a direct upload request to the S3 bucket. But when a user B wants to access the image, it does that through the CDN.

### Implementation detail

![Screenshot 2022-12-30 at 5.51.22 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc03ee62-0be4-497b-9713-d792d9cc66c1/Screenshot_2022-12-30_at_5.51.22_PM.png)

- Here, it is important that we don’t store the entire URL of the image - just the identifier for the image. An image is just one part of a post. There are other aspects to a post as well. We want to decouple the image service from the posts service.
- In our case, we are creating the image URL using the user Id and a randomly generated image ID. When we’re storing the image’s in our DB, we are already including the userId in each row for the table `posts`. Thus, we just need to additionally store only the randomly generated image Id.
- Why?
    - We don’t need to store the redundant `https://CDN_DOMAIN_NAME/` part in each row entry. Keeps things lightweight!
    - It provides us the flexibility to smoothly transition to a different CDN. We’ll just need to update the configuration once. Rather than having to update every single entry in the `posts` table.
    - It decouples the image service from the posts service.

<aside> 💡 In general, if values are derivable, rely on that instead of storing it in the DB.

</aside>

<aside> 🛺 Decouple services as much as possible, wherever possible - it is key to design a robust system!

</aside>

![Screenshot 2022-12-30 at 5.52.14 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10ebb74b-efcf-44a6-a973-9c1b9c5ce277/Screenshot_2022-12-30_at_5.52.14_PM.png)

- The user calls the Posts Service once the upload to S3 has finished, which makes an entry for a new post in the `MySQL` DB.
- Simultaneously, an event is sent by the Posts Service to Kafka which is being subscribed by other services like search, analytics, etc. which get triggered so that further processing can happen (a.k.a. `extensibility`)!
- Now, when the request for viewing the image has been made, it would include the CDN URL + userID + imageID, generated on the fly and CDN would either return its cached copy or fetch the actual image from the S3 bucket, cache it and return it.
- This is a really good example of separation of concerns, where every component is responsible for doing its own thing!
- P.S. CDC will be covered next week!

![Screenshot 2022-12-30 at 5.58.57 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/accb6cb6-9098-491f-84b7-8d0497e74429/Screenshot_2022-12-30_at_5.58.57_PM.png)

![Screenshot 2022-12-30 at 5.59.00 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2d45ec39-2f4d-4fbf-8d19-e11ad9d53278/Screenshot_2022-12-30_at_5.59.00_PM.png)

- not truly private as image URLs are publicly accessible
- approximating privacy by making URLs short-lived (typically 10 mins) through certificates

![Screenshot 2022-12-30 at 6.01.23 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f39efb29-359c-48a8-9b7d-3764edb502c4/Screenshot_2022-12-30_at_6.01.23_PM.png)

- Here, the URL returned in the JSON response includes the full image URL for each post dynamically generated by the backend.

### Image Optimizations

- Why is this needed?
    
    - Not everyone has a great internet connection. They might have limited bandwidth, etc.
    
    ![Screenshot 2022-12-30 at 6.07.51 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/117c2a2e-c7ee-47f5-83ba-660a1b2bfae1/Screenshot_2022-12-30_at_6.07.51_PM.png)
    
    - hence, for someone on a slower bandwidth network, loading the entire 1000 x 1000 image is a very bad idea. Instead, we can make do with serving a small version of the image.
    - Thus, we should be able to serve images of different resolutions based on a user’s network state.
- A lot of people feel that they have to build a separate image optimization service. However, CDN provides, usually, all the image optimization features that we need.
    
- Just like how CDN provides support for authorization through query params, similarly, it provides support for image optimizations through query params as well.
    
- e.g. here, adding `w=360` (can be added either on the backend side or the client side before requesting for the image) to the CDN will transform the image to make its width 360px while keeping the aspect ratio constant. Similarly, there are many other query params related to image optimization that we can pass to a CDN.
    

![Screenshot 2022-12-30 at 6.09.13 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/97293a86-1d7e-4eb6-9e7d-d0637e4fa7f8/Screenshot_2022-12-30_at_6.09.13_PM.png)

<aside> 📯 A lot of things have already been built and made available to us, often in an easy-to-use and cheaper manner. Leverage them instead of reinventing the wheel unless you absolutely have to.

Cheaper is, usually, always better. Need to save money for our organization!

</aside>

# Designing HashTag service

## Requirements

- This is the screen that we are building
    
    ![Screenshot 2022-12-30 at 6.18.17 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8556dc69-e60a-4319-bc2d-d2e55bcdab43/Screenshot_2022-12-30_at_6.18.17_PM.png)
    
    - We don’t care about which photos are the top 100 photos (that is the responsibility of the data science team)
    - We are focused on the user experience - we want to render this page as fast as possible
- Assumptions & scale requirement
    
    ![Screenshot 2022-12-30 at 6.19.50 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/71cbe363-3705-43e8-b8e1-bed8bed9a056/Screenshot_2022-12-30_at_6.19.50_PM.png)
    

## Brainstorm

![Screenshot 2022-12-31 at 12.48.15 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c5ed0185-4474-49a4-81ec-9d60b813770c/Screenshot_2022-12-31_at_12.48.15_AM.png)

### Storage

- Since we need to just lookup based on a key (the hashtag), we’ll use a KV store (it already gives single-digit msec response time)
- What is the structure in which we’ll store the data?
    - v1
        - hashtag: string
        - count: integer (to maintain the overall count of posts containing that hashtag)
        - posts_100: list of ids of the top 100 posts given to us by the data science team
    - Can we store something more in the `posts_100` field? What are the downsides of storing just post IDs?
        - Either on the client side, the client would have to make 100 API calls to fetch the details for each post (e.g. the link of the image associated with the post). This is not optimal because the client load will increase!
        - Or the hashtag service would have to make 100 API calls to the posts service to fetch the details of each post. This is not optimal because:
            - increases latency due to network delays
            - puts a lot of load on the posts service as many users would be simultaneously triggering the hashtag service, and each such trigger would lead to 100 API calls to the posts service.
    - What can we do? We can just store all the required information for the top 100 posts in the `posts_100` field, i.e. store the denormalized posts data (e.g. userId, random Image Id, caption, etc.). Plus, we’ll anyways be notified when the list of top 100 posts are updated. Thus, this field can be automatically updated by that.
    - What is the downside of this approach?
        - The data can be stale. Suppose the post had caption “X” when it got inserted into the `posts_100` field by the data science service. Suppose the creator of the post updated the caption now and a user is now visiting the hashtag page before the data science team sends the latest update for `posts_100`. In this case, the caption that this user would be seeing would be stale.
        - But what is the probability of the user doing that?
        - These are the tradeoffs that we need to think about which have to be informed by the product. E.g. if on the hashtag page that we are designing, we are not showing the caption at all, then, the staleness in the caption doesn’t matter at all. If we are showing the caption or some other metric that we are capturing inside the `posts_100` field, then the staleness matters _a bit_. But some amount of staleness could be allowed.
- Which DB to go for?
    - We need sharding out of the box as one DB will not be able to handle the read-and-write volume that our system is going to receive. Using a cache here will only defer the load - to the CDN, the in-memory cache, the cache in the API server, the cache in the load balancer, etc. But in the worst case, the load will still be too much for one DB to handle.
    - We can do that on SQL but we’ll have to manage the shards manually. However, NoSQL DBs support sharding out of the box (manipulating shards, moving data in/out of shards, etc.)
    - That is the main reason for choosing NoSQL. If you’re comfortable with managing shards manually, you can choose SQL DB as well.
    - Thus, we can use DynamoDB (for e.g.)

<aside> 📯 We have discussed several approaches through which we can build the system with their pros and cons. The final decision has to be informed by the product and what are the tradeoffs that we are willing to make.

Since every component of your infra at scale is a brittle component, you try to minimize the load on them!

</aside>

### Counting

- How can we update the total post count for each hashtag?
    
- Setup: we’ll have a posts service for when a new post is created which stores the new post in the `posts` DB
    
- Now, we need to update the count in the DB (we’ll call it the hashtag DB) we designed above once a new post is created.
    
- Should the posts service update the hashtag DB directly once a new post has arrived? No. There would already be a Kafka topic (e.g. post_published) listening for the event of a post being published. Let’s leverage that.
    
    - This Kafka topic would receive information about a new post once it is created. (e.g. { post ID, user ID, caption })
    - What is a good partitioning key for this Kafka topic? `user_id` (remember, the partitioning key dictates how many concurrent consumer workers can read the data from Kafka)
- Now, a pool of Hashtag consumers would be listening to this topic! Should that pool of consumers directly update the hashtag DB? Think about the implementation!
    
    ![Screenshot 2022-12-31 at 10.12.08 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b39692b-7e7c-4ef4-9f41-15fc1ce29cb9/Screenshot_2022-12-31_at_10.12.08_AM.png)
    
    - To be able to update the count of each hashtag in a given post, first, we’ll have to extract the hashtag from the new post as we just write the hashtags in the caption for each post.
    - Then, for each hashtag that has been extracted, we’ll have to update the count for that hashtag in the hashtag DB by 1.
    - What is the issue with this?
        - This will lead to the write volume blowing up for the hashtag DB.
        - On average, there are about 8 hashtags in each Instagram post.
        - Thus, the write load will be 8 times the load of creating a post on Instagram (which is already high).
- How can we do better?
    
    - Since we’ll only be displaying the top 100 posts and if a hashtag is famous, it doesn’t matter to the user if the count shown is stale by some amount, we can batch the count updates.
    - Instead of updating the hashtag DB for each post, we can update it after every minute and aggregate the updates to be made in an in-memory buffer for all the hashtags that each consumer has extracted from all the posts that it has received.
    - Think about implementation detail!
    - A good case:
        - Suppose one of the consumers received the two posts below:
            - Post 1 with hashtags: [sun, sunset]
            - Post 2 with hashtags: [sunset, icecream]
        - Now, in the batching implementation, it’ll store the updates to be made for each hashtag as:
            - sun: 1
            - sunset: 2
            - ice cream: 1
        - After a given period of time, it will update the count for each hashtag in the hashtag DB, which means n number of writes for n hashtags that it would have stored in its in-memory buffer during the batch interval!
    - A bad case:
        - Suppose two different consumers received the two posts below:
            - Post 1 with hashtags: [sun, sunset]
            - Post 2 with hashtags: [sunset, icecream]
        - Then, the batch updates to be done in each consumer looks like:
            - Consumer 1:
                - sun: 1
                - sunset: 1
            - Consumer 2:
                - sunset: 1
                - ice cream: 1
        - In this case, we’ll be doing 4 writes to the DB even though we just had 3 different hashtags. This bloats up at scale.
    - Thus, batching doesn’t work this way unless we use a centralized aggregator across the consumers and then, group by hashtag. We’ll need a shared memory buffer across consumers and then, we’ll have to scale that too. This is a huge issue as the RAM requirements would shoot up (remember 8 times the load of writing posts)
    - We also cannot change the partition key from `user_id` in the Kafka topic above as many other services depend on it (e.g. search, analytics, notifications, etc.)
- We can add another Kafka layer where the partitioning is done by the hashtag. Then, each consumer attached to this Kafka will receive all the updates for a given hashtag which it can aggregate for some time and batch-write the updates to the hashtag DB. In this case, all the updates for a given hashtag go to the same consumer, and thus, we don’t need a separate centralized aggregator for the batching to happen efficiently.
    
- This is called the high-level `Adapter` pattern and it is very commonly used.
    

<aside> 📯 We arrived at the adapter pattern by thinking about the implementation. If we hadn’t thought about the implementation, we wouldn’t uncovered the issue that required the adapter pattern.

</aside>

## Solution

- The inputs to our system
    
    ![Screenshot 2022-12-31 at 11.26.30 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/89d871c1-ce29-4bab-8929-64afcd8dd995/Screenshot_2022-12-31_at_11.26.30_AM.png)
    
    ![Screenshot 2022-12-31 at 11.27.32 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/795aa330-2a9b-4d5d-ba11-c32069449887/Screenshot_2022-12-31_at_11.27.32_AM.png)
    
    - This is a classic case of inter-service communication
        - We can do it either synchronously or asynchronously
        - If we want to do it synchronously, the hashtag service has to be up all the time. Why do that? Go for async such that Kafka acts as a glue to which multiple services can publish and we can consume what we need.

![Screenshot 2022-12-31 at 11.29.51 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27791481-2923-48c7-af46-952202b4855b/Screenshot_2022-12-31_at_11.29.51_AM.png)

- We need very fast response times as we need to provide an amazing user experience. This is what we are optimizing for. Because of that, we are sending the entire information for each of the top 100 posts in a single API request. If we were optimizing for something else or had a different risk appetite, we could have gone for a different choice (like sending only a list of post IDs instead of the entire information for each of the posts because we might be optimizing for (say) consistency)
    - having separate API calls to fetch the details of a given hashtag, the count for a given hashtag, and for fetching the list of the top 100 photos is not the right choice here because that would not lead to a great user experience as multiple API calls would hog up the client’s network.

<aside> 🚦 An important mindset to inculcate: always think from a product perspective. Ask critical questions to your Product Manager or to your manager. The product dictates engineering design!

</aside>

![Screenshot 2022-12-31 at 11.38.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ca479f5-9c8b-4f3b-a6fb-9b222a30adb2/Screenshot_2022-12-31_at_11.38.04_AM.png)

- for counting, if we make a DB call for to increment the count by 1 for each hashtag upon each new post, it would choke down the DB and the DB will die when there is a surge.

![Screenshot 2022-12-31 at 11.39.59 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7dd8d809-3363-403f-9969-ea7e982ae96c/Screenshot_2022-12-31_at_11.39.59_AM.png)

- READ path and WRITE path
    - usually both of them are different and can be clearly visualized.
        
    - READ path
        
        - how you’re reading from the system
        - READ path here:
        
        ![Screenshot 2022-12-31 at 11.40.41 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/71b07e15-5823-453c-b9e0-33bb86e4c2ea/Screenshot_2022-12-31_at_11.40.41_AM.png)
        
        - ask the question: is the READ path optimized? Because scaling reads is simple: scale DB (e.g. read replicas) + add caching layer (CDN, remote cache, centralised cache)
            
            ![Screenshot 2022-12-31 at 11.44.45 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3426493a-8829-421f-b449-8c898576cd75/Screenshot_2022-12-31_at_11.44.45_AM.png)
            
        - We want the hashtag API to do bare min work which is why we’re storing all the information in one DB (as opposed to storing just post IDs and fetching the corresponding posts from the posts service, etc.)
            
    - WRITE path
        
        - how you’re writing to the system
        - WRITE path here:
        
        ![Screenshot 2022-12-31 at 11.41.11 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/301ae1a4-a49a-4d4a-8cee-b3797e094d46/Screenshot_2022-12-31_at_11.41.11_AM.png)
        

<aside> 🤿 Separating READ and WRITE paths and optimising them separately makes us better engineers.

</aside>

![Screenshot 2022-12-31 at 11.49.17 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/904e2d16-dc12-4576-b8ef-06d09043cf93/Screenshot_2022-12-31_at_11.49.17_AM.png)

- READ path optimization
    - here, we are not adding read replicas as the DB can take the read load
    - we are simply adding a caching layer

![Screenshot 2022-12-31 at 11.50.29 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12db24ab-13d7-470e-af17-6c138080146c/Screenshot_2022-12-31_at_11.50.29_AM.png)

- WRITE path optimization
    
    - Is it doing the bare minimum that it needs to do?
        - post service sending an event to Kafka - bare minimum
        - Kafka calling hashtag service which updates the hashtag DB - bare minimum
        - So, we can’t really optimise anything here
    - Ingestion in Kafka: do you have large enough partitions to support this on Kafka or not? We need to tune it.
    - Reading from Kafka: do we have enough consumers to read efficiently from Kafka? Remember that the parallelism in Kafka is capped at the number of partitions it has. Thus, if there are 1000 partitions but only 2 consumers, that is not correct.
    - Batch writing and in-memory counting (aggregating for each hashtag) is something that we’ve already discussed
    - From our storage, we need support for partial updates as we need to be able to just increment the total count for a given hashtag or the data science team will be able to update just the `top_photos` key.
- The implementation challenge with batching and updating counts for hashtag (that we’ve discussed before
    
    ![Screenshot 2022-12-31 at 11.57.04 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9d6b0a67-b465-49ad-9f53-c8dfae30b0f7/Screenshot_2022-12-31_at_11.57.04_AM.png)
    
- ENTER: adapter pattern
    
    ![Screenshot 2022-12-31 at 11.58.10 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfac97e0-fd3c-4fbb-97c2-f92965e42acf/Screenshot_2022-12-31_at_11.58.10_AM.png)
    
    - Thus, if a new post has 3 hashtags, 3 events will be sent to Kafka with the topic `POST_HASHTAG`.
    
    ![Screenshot 2022-12-31 at 11.59.21 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93fba5f1-73ed-4e5f-b5ad-99f3419d6213/Screenshot_2022-12-31_at_11.59.21_AM.png)
    
    - now, the event for each hashtag count update will come to the same counting server which can then aggregate the updates for that hashtag in memory and make a partial update to the count for each hashtag in a batch.
    - This reduces the number of I/O that happens on our DB and is really important for our system to scale as our DB is our most brittle component.

The overall flow:

![Screenshot 2022-12-31 at 12.02.00 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba827f8e-feed-49b5-a503-08a2f247cee6/Screenshot_2022-12-31_at_12.02.00_PM.png)

- In the READ path, the CDN has been added because, for a given hashtag, since the top posts are not going to be updated for an hour (say), we don’t need to burden our infra every time for the same data corresponding to a given hashtag.
- The CDN can simply cache the JSON response. This is a classic use case for doing this!

## Key takeaways

![Screenshot 2022-12-31 at 12.05.28 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fca05dd6-f685-4f53-920d-f79ba5294fc6/Screenshot_2022-12-31_at_12.05.28_PM.png)

- Kafka acts as a glue between multiple services to talk to one another
- High-level adapter pattern where we want to partition by a different partition key - so, we consume a new post in the first Kafka, process it (hashtag extraction), and re-ingest it in another Kafka (or the same Kafka but with a different topic) where it is partitioned by a different key!
- Effective Batching and counting: to reduce the number of writes on our DB so that it doesn’t have to do a large amount of work as it is our most brittle component
- Identifying READ and WRITE paths and tackling them one at a time

[https://drive.google.com/file/d/1ZTcbOqdXlGDLzoIBD-H6iFC8HKqReUSK/preview](https://drive.google.com/file/d/1ZTcbOqdXlGDLzoIBD-H6iFC8HKqReUSK/preview)