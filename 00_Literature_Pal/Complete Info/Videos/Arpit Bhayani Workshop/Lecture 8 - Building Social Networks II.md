---
tags:
 - people/pal
 - date/2024-03-18
---

# Agenda

![Screenshot 2022-12-31 at 12.11.55 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2ea8b99-4974-4a37-a40e-b4c77984e087/Screenshot_2022-12-31_at_12.11.55_PM.png)

<aside> 💈 An engineer has to wear three hats: engineer for implementation, product manager and architect

</aside>

For tagging photos, we’ll wear the hat of a PM and think from all perspectives, think about how it affects other systems, how other systems would depend on it, etc.

<aside> 🛫 Seeing the blast radius of your implementation is really crucial!

</aside>

# Foundation: How images are served

- Why?
    
    - Based on this knowledge, a lot of fancy stuff is built
    - E.g. in social media apps that allow us to share stuff (e.g. year in review), we typically see an image that is personalized to each user. Now, the platform doesn’t store an image for every user. Instead, they are created dynamically.
- Example: image path
    
    ![Screenshot 2023-01-03 at 3.21.56 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4bca640b-4289-41ac-99ac-3a604bd61277/Screenshot_2023-01-03_at_3.21.56_PM.png)
    
    - We usually put it in `<img src=`
- But what happens behind the scenes in a browser when the image above is loaded?
    
    - Browsers are very simple
    - When they see a `<img>` tag, they search for an `src` attribute
    - If that attribute is set, it assumes that whatever value is given to `src` is a URL and it makes an HTTP GET call to that URL. It doesn’t matter whether the value is actually a URL. Which is why `<img>` tags are susceptible to security issues.
    - Finally, whatever response it receives, it interprets it as an image and tries to render it.
- The most generic way of serving an image
    
    ![Screenshot 2023-01-03 at 3.30.59 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f0f869b-cabd-4d89-868d-a4687c827d6f/Screenshot_2023-01-03_at_3.30.59_PM.png)
    
    - use a `static` folder
    - Essentially, we map the route `/static` on the API server to a path (e.g. `/site/static`) on the disk attached to that server.
    - The value following `/static` in the image path refers to the relative path of the image on the disk inside the folder mapped to the `/static` route.
    - Once an API server receives a request for an image URL, it first notices that the path starts with `/static` and so, it knows that it has to read an image file from the local static folder at the path specified by the value following `/static`.
    - It does a literal file read (opening the file and reading the bytes) and returns the bytes as the response.
    - We can usually configure this on our web server.
- Modifying this to use S3
    
    ![Screenshot 2023-01-03 at 3.36.36 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ae58e37-7f29-4c2e-9e53-bd18375ea772/Screenshot_2023-01-03_at_3.36.36_PM.png)
    
    - Instead of reading from the local disk of our API server, we can change the handler for the URL to read from S3 instead.
    - S3 is also a file system. So, instead of reading from our local file system, we are reading from S3.
    - `raw_b`: the raw bytes
    - Here, we built a proxy that serves everything that is there on S3 through the API handler.
    - The example above is a normal API server that we’ve run (running on port 5000, for e.g., on my local machine)
- The example above on using a proxy using our API handler to serve images through S3 gives us the ability to serve dynamic images.
    
    - A very practical e.g. Github. A few years back, upon sharing the URL of our repository, it would simply show our profile photo which looked horrible.
        
    - But now, upon sharing the URL of our repository, it generates a really nice image with information about the repository which dynamically updates.
        
        ![Screenshot 2023-01-03 at 3.58.29 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61543131-6bc8-48fa-93cc-b6cdbb248e4d/Screenshot_2023-01-03_at_3.58.29_PM.png)
        
    - How? When the URL of a repository is added to a social media platform, the thumbnail image for that URL is generated through the `og:image` meta tag specified in the <head> tag of the source code for the website.
        
    - In the case of a Github repository, the value of that tag is something like this:
        
        ![Screenshot 2023-01-03 at 4.00.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/642ff3ac-2753-4f4c-9f84-8dea26f8caf3/Screenshot_2023-01-03_at_4.00.38_PM.png)
        
    - In this case, the URL does not end with `.png` or `.jpg`. It makes an API call that dynamically generates an image (for e.g. if the server is written using Flask, it could use a library like PIL to generate it) on the fly and returns the image as the response.
        
    - Now, if all the requests for loading this image were coming to the API server, it would bloat up. Which is why a CDN is used. The CDN cache could be cleared once a day (for e.g.) so that when a new request comes in, it can fetch a new image from the server and keep serving that same image for all the requests for that image made that day.
        
- This also opens up more use cases. Example: DocuSign
    
    - Here, we still want to serve documents but these documents are extremely private and security is a very important factor. If we serve it through a CDN, anyone with the link will have access to it.
    - DocuSign is not meant for serving an image at scale because usually, the document signing happens between a few handfuls of people. Privacy is what matters. Thus, we can compromise on speed.
    - So, in this case, we serve the images/documents through an API server that controls who has access to the file.

<aside> ☁️ Thus, don’t live in a binary world where CDN is always used to serve images. It depends on your use case. Learn to live in the grey area.

</aside>

# Designing Gravatar

## What is Gravatar?

![Screenshot 2023-01-03 at 4.10.55 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e94eb87d-353a-4bc5-8f07-fbd72280573d/Screenshot_2023-01-03_at_4.10.55_PM.png)

- We specify our email ID and based on the hash of our email ID, an image URL is generated.
- Since the hash function always returns the same value for the same email, the URL is constant.
- When we add our Gravatar URL to a `<img>` tag, it renders our “active” profile picture.

## Requirements

![Screenshot 2023-01-03 at 4.11.55 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bbba27dd-9e0b-483b-8c33-860772d5f529/Screenshot_2023-01-03_at_4.11.55_PM.png)

- As a user can upload multiple photos on Gravatar (a private platform) and choose which profile photo is active.
- The URL always remains constant because it doesn’t point to a specific image. It points to a profile.
- The image is dynamically updated depending on whatever the user has chosen as their active profile picture.

## Brainstorm

### Storage

- best to use a simple RDB with 2 tables
    
- `users` table
    
    - `id`: autoincrement
    - `email`: unique identifier
- `photos` table
    
    - `id`: autoincrement
    - `user_id`: foreign key
    - `s3_key`: we can generate the whole image URL from the S3 key
    - `is_active`: boolean (index)
- SQL query: (given an input `hash`)
    
    ```sql
    SELECT * from photos 
    INNER JOIN users
    	ON photos.user_id = users.id
    WHERE
    	photos.is_active = true
    	AND 
    	?? = hash
    ```
    
    - Since we’ll receive only the user hash as input (remember the URL consists of the hash of the user’s email)
        
    - For `??` there are two options:
        
        - compute the hash on the fly and check
        - precompute and store the hash for each user and just compare the stored hash value
        
        (assumption: the hashing algorithm is never going to change)
        
    - The problem with option 1 is for every request, it will do a complete table scan and compute the hash for each row and then, do the comparison. This is extremely expensive. Thus, we’ll go with precomputing and storing the hash value for each user.
        
- Thus, our `users` table now looks like this:
    
    - `id`: autoincrement
    - `email`: a unique identifier (unique index)
    - `hash`: string hash of the email (unique Index)

<aside> 🔉 Most DBs have a feature like `EXPLAIN` to which you can pass an SQL query which will show how the query will be executed. Make use of that!

</aside>

### API Handler

- What is the API handler supposed to do? Assume the route we need to handle is this:
    
    ![Screenshot 2023-01-05 at 10.45.42 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9aa866d8-2058-429d-948d-c333e6d1e926/Screenshot_2023-01-05_at_10.45.42_AM.png)
    
- For the route, we add a handler method. In that handler method:
    
    - We first extract the hash
    - Next, we fire the SQL query to get the S3 key
    - Next, we actually read the S3 file
    - Finally, we send the raw image bytes.
- Here, we don’t return the image path because the API route that we are handling would be added inside an `<img>` tag, which expects an image to be returned from the URL. We can’t change how `<img>` tag works. Thus, we don’t return the image path here, but the entire image itself. This a basic mistake that a lot of people.
    
- However, this will put a lot of load on our API server, which is where we make use of CDN!
    

## The flow

### Uploading Photo on our Gravatar

- It uses the same image upload service that we designed in Class 7!

![Screenshot 2023-01-05 at 10.49.09 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fe51841-bc6a-4ed0-94be-603df438930d/Screenshot_2023-01-05_at_10.49.09_AM.png)

### Saving the image on our DB

- Once the upload is successful, we make a POST request to store the image ID for the corresponding user ID in our DB
    
    ![Screenshot 2023-01-05 at 10.50.35 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8cbf747d-3562-44e4-b652-82e605336792/Screenshot_2023-01-05_at_10.50.35_AM.png)
    
- Here, we can directly use the image ID for the `id` column in the photos table instead of having another auto-increment ID!
    
    ![Screenshot 2023-01-05 at 10.51.21 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/58269630-9f29-4e1d-a457-34614be646f6/Screenshot_2023-01-05_at_10.51.21_AM.png)
    
    - again, storing hash is important event though it is a derivable value from the email because that would require doing a complete table scan each time we have to fire an SQL query!
    - Thus, we store the hash and create a unique index on top of it!

### Rendering the active photo for a given user

![Screenshot 2023-01-05 at 10.53.44 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f239e854-e8c2-4722-8cec-920d5b81a7fe/Screenshot_2023-01-05_at_10.53.44_AM.png)

### Marking a given photo as active

![Screenshot 2023-01-05 at 10.57.53 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5c47796-1d79-4794-b5b1-b142963701b6/Screenshot_2023-01-05_at_10.57.53_AM.png)

- Let’s say a user has uploaded multiple photos and now, wants to change the active photo
- There are multiple ways of doing it. One way is the good-old transactions. Here, we need to ensure that `is_active` for the currently active photo is set as False and `is_active` for some other photo (that the user has specified) is set as True. Both of these steps should happen. If any of the step fails, it would be an error (either none of the images being marked as active or multiple images marked as active). That is why, we need to do it in a transaction

### Handling load and making it easy to use for the end-user

- We want to use `gravatar.com/<hash>` instead of `api.gravatar.com/user/<hash>`
- Enter CDN

![Screenshot 2023-01-05 at 11.00.47 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4e7c258-8323-466b-8ae2-812dbbfbf4a8/Screenshot_2023-01-05_at_11.00.47_AM.png)

- Thus, here, we put CDN in front of an API server!

### Overall architecture

![Screenshot 2023-01-05 at 11.03.12 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d0c3fa1-2aa7-46b7-abde-da0c530b7e18/Screenshot_2023-01-05_at_11.03.12_AM.png)

- Image Upload: User uploads the image to S3 and makes a POST request to our API server to store the image ID in our DB.
- Reading Image: When a user wants to use the gravatar image, they put the URL in an <img> tag (say), which makes a GET request to our CDN. If the image is not cached on the CDN, it makes a request to our API server, which gets the image ID using the user hash from our DB, fetches the image from S3 and sends the image back. The CDN then caches the image and returns the response. Next time, for the same URL, the CDN will serve from its cache.
- Updating active image: Now, we are not going to update our profile photo often. When we do update it, we want the changes to be reflected everywhere. In this case, when the active photo is updated, it sends an event to Kafka which triggers the CDN invalidation workers which simply makes an API call to the CDN to invalidate the cache for that particular user. CDN provides an API to invalidate the cache in such a manner for a certain path.

### Optimizations

![Screenshot 2023-01-05 at 11.18.49 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/81df868f-9e44-4f4b-96c1-9c051d7d2e3d/Screenshot_2023-01-05_at_11.18.49_AM.png)

- Instead of store `is_active` on the photos table, we can store the `active_photo_id` in the users table itself. Multiple benefits:
    - The API handler for fetching the Gravatar image won’t have to do a join between the users and photos table to find the active photo ID.
    - When we want to update the active photo, we don’t need to use transactions to ensure a safe update of 2 rows (the previous active photo and the new active photo). We just need to update the `active_photo_id` column in one row in the `users` table.

### Security

- Unauthorized updates: It is possible that someone might send the image ID of an image that belongs to some other user. To avoid that, while making the update, we need to check both image ID and the fact that the image ID belongs to the user.
    
    ```sql
    UPDATE photos SET is_active = true WHERE image_id = ?? AND user_id = ??
    ```
    
- PII: here, even though our Gravatar has the user email, that email ID is never exposed. Only the hash of that email ID is exposed, from which the email cannot be recovered. Thus, anyone else using our gravatar service, will not have access to user’s PII unless the user explicitly granted access to its PII to them. Important to keep this in mind!
    

<aside> 🎯 Even though it was a simple looking system, there were a lot of considerations to be made. So, we should strive to develop this holistic thinking.

</aside>

# On-demand Image Optimization

- In Lecture 7, we used a CDN’s native image optimization feature. Today, we’ll build our own.

## Requirements

![Screenshot 2023-01-05 at 12.12.31 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f4e5806-db41-4d9d-85c7-52f164c60ac6/Screenshot_2023-01-05_at_12.12.31_PM.png)

- We should be able to specify the on-demand optimization that we want to do on the image in the image URL itself as transformative parameters (which is what CDNs let us do)
- In the example, above, although the original image is 1024 x 1024, specifying w = 32 should return a 32 x 32 image instead.
- There are many such parameters that we should be able to send - like grayscale, colorise, decolorise, face detection, remove background etc.

<aside> 🪐 When you’re using a CDN, go through the image optimisation parameters that it supports

</aside>

## Approach

- Broadly, it looks like this
    
    ![Screenshot 2023-01-05 at 3.54.38 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56e640c8-5b3c-4871-adc4-a79aed525141/Screenshot_2023-01-05_at_3.54.38_PM.png)
    
    - If we receive a param for whom we don’t have the image, we save it to the local cache as well as to S3 so that the next time we don’t have to generate the image. Once the cache expires, we can fetch the image from S3 instead of generating it. These are two ways of optimising this process.
- Given that this is on-demand image optimisation, we can’t do it asynchronously as there is no time to do it async. The user wants the response then and there. This is why, on-demand image optimisation tends to be costlier as it is very CPU intensive. Thus, we need large servers with large number of cores (in front of a load balancer) that do the on-demand transformation as users are expecting really fast response times.
    

### Transformation

- How to actually do the transformation? You are not going to manually write the code for the manipulation for the bits and pixels of the given image. Instead, go for using libraries.
- Almost every single company uses `imagemagik` - a very optimised (most performant till date) utility written in C++ with its bindings in Java, Python, etc. It uses multiple cores on our machine to do image transformation. (even, python’s library PIL comes with this binding)
- We have to use `imagemagik` if we want to build an on-demand optimisation service or do image transformation on the fly.
- Every single param that `imagemagik` supports can be supported as a param for image optimisation where we just have to extract the parameter value from the URL, pass it to `imagemagik` and it will give us the transformed image.

## Optimisations

- If we know that there are certain image dimensions that are going to be requested, we can create those versions asynchronously and store them on S3 (saves money as less requests for our API servers)

# Tagging Photos

## Goal

- To become comfortable with ambiguity. E.g. we have been given a one-liner for the feature that we need to build, nothing else. As a senior engineer, we’ll have to think through all the systems that it would depend on, the systems that would be affected by it, what if it goes down, etc. Usually, all the possible scenarios are not thought through.

## Requirements

- Need to support tagging in photos

## Questions

- Whom can we tag? People, locations?
    
    - Implications:
        - Different teams might have to work together as each might be responsible for each type of entity that we are allowing to be tagged
        - How we are storing the data and what we are storing: we need to collate the data for the tagged objects across the different types of entities in one place (just like how we faced the choice of either storing the reference to post IDs or the entire data of the posts themselves in the tagging service that we designed in Lecture 7)
        - The UI rendering might be different. If someone is hovering on the tagged entity, we might want to show the details of that entity (e.g. place details for a tagged location or profile for a tagged person). Depending on the decision that we made on how to store the data, this would impact the corresponding service (s). If we store only the reference to the objects, upon hovering, we’ll have to make an API call to fetch the details of that entity. This will increase the load on the services corresponding to each entity that we are allowing to be tagged
    
    <aside> 🪐 Probe in different directions
    
    </aside>
    
- Do we want to notify people who have been tagged?
    
    - Implications:
        - To send the notification, we’ll probably send an event to Kafka which will trigger a consumer that will call our notification service. Thus, we need to integrate with the existing notification system in place.
        - This might, hence, increase the load on the notification service
        - We might have to work with the notification team to add support for a new type of notification - i.e. notification for when one is tagged.
        - Do we notify about all tags in the same manner? Suppose if a famous person tagged a user, we might want to send the user an email vs if their friend tagged, we might be okay with just sending a regular notification in the app.
    
    <aside> 🎖️ We have to think about all the different configurations because we are the ones owning it.
    
    </aside>
    
- are we allowed to tag? - authorization
    
    - E.g. if we tag someone in an obscene photo, they might not like it as their image would be at stake.
    - Implications:
        - Thus, we can enable a review of all the photos where one has been tagged. This would require building a review and approval system.
        - Or we can give them options to specify if they want all people to tag them or no one or some people, etc.
        - If an existing authorization system exists, we might have to leverage it. If it doesn’t, we might have to build it.
- Show in the feed of my friends the photos that I’ve been tagged in (fan-out)
    
    - Implications:
        - Similar to the notification team, I would have to work with the feed team to enable a new type of feed post - one where the photos in which one is tagged is shown.
        - It might lead to more likes/reactions and the service handling that might receive a surge too.,
- Ability to search by tagged people/places?
    
    - Implications:
        - Are we ingesting the tag information in the search service or not (assuming a search service is already in place)?
        - Thus, we’ll have to ensure that our tagged entities are also a part of the search index.
        - Going into more details, if we’re doing elastic search, what kinds of information are we allowing to search on: in the case of a tagged user, is it their first name, last name, their bio, city, etc. If the person has gone to a certain school and we search for that school, should a photo in which that person has been tagged show up?
        - Depending on the degree of depth that we want to go to, the search index has to be that much complex and the search team would have to do that work (all the things that need to be done to power an IR system).
        - This will surge the Search traffic so, at minimum, the search service would have to be scaled up.
- Adding tag suggestions on an image?
    
    - When a user uploads an image, we give them suggestions for whom they can tag.
    - Implications?
        - It would involve a lot more of image processing in the API servers, need to do face recognition (we’ll need a service that is training an ML model on face images)
        - When we’re tagging, in terms of UX, we give them the suggestion usually when they hover on top of the face of a person. Thus, along with detecting the presence of different faces in an image, our ML model has to also return the coordinates of where each face is present in each image.
- Search: The service that is impacted the most
    
    - How are we tagging them?
        - We’ll search for the name of the person/place, etc. for every key press.
        - Millions of people would be doing this
        - On average, each photo has 2-3 people.
    - Implications:
        - This would lead to a massive surge in the search traffic (along with the additional surge we discussed above from searching by tagged people/photos)
        - Search would have to be configured in a very fast, simple, efficient way.
        - It would have to be integrated with the suggestion service as well to re-rank the search results that we are showing (e.g. if we detected 3 faces, then, the names for those users should be shown at the top of the search results)
        - Because of the huge traffic surge, we cannot use deep learning based search here. Even Instagram/FB tagging used to be very dumb before where we had to write the exact full name or the handle of a user to tag them (typeahead search)

<aside> 🎖️ Thus, a small feature statement from the PM or CEO has so many implications. It might seem simple to them but it is up to us as senior engineers to think through all these possibilities holistically and envision what all could happen and be future-ready.

</aside>

## Implementation

- How would you store the tag information?
    - corresponding to the photo, we have a key `tagged` which has list of all tagged people.
        
        ![Screenshot 2023-01-05 at 5.38.34 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e7eadb13-68e9-4c5c-8f22-df0775fe6279/Screenshot_2023-01-05_at_5.38.34_PM.png)
        
        - We’ll normalize the coordinate values so that they are between 0 and 1 so that for every image resolution (hence, to handle on-demand image transformation), we can use the coordinates correctly. (e.g. if image is 1000x1000 and center of bounding box for a tag is at 300, 300, then, we’ll store x = 300/1000 and y = 300/1000)
        - However, for a bounding box we need 4 values (either x,y,w,h or top-left point and right-bottom point)
        - In the most accurate case, the bounding box cannot be fix width as different people’s faces may occupy very different sizes in the image.
        - Depending on how easy or complicated we want it to be, we can either:
            - Use a service that does simple image processing to get the coordinates of the faces; or
            - Ask the user to draw the bounding box for each person’s face; or
            - Just use a fixed width bounding box (day 0)

![Screenshot 2023-01-05 at 5.39.15 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75f304ad-da8e-45c8-892d-830832527a74/Screenshot_2023-01-05_at_5.39.15_PM.png)

- Again, Kafka as a glue
    
    ![Screenshot 2023-01-05 at 5.39.35 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b3f7933d-6bb0-494a-9237-ec51d9af85c1/Screenshot_2023-01-05_at_5.39.35_PM.png)
    
    - When someone is tagged/untagged from a photo, an event is sent to Kafka and different services can be triggered accordingly.

# Designing Newly Unread Message Indicator

## Goal

- To introduce a new high-level design pattern that is very prevalent in the industry but very few people talk about (in companies that are in a high-growth phase)

## Requirements

- here, it is not the number of unread messages. It refers to the number of new messages that we aren’t even aware of that we’ve received.
- E.g. we might be shown, like in the image below, that we have messages from 3 unique people. We could click on the icon, and see that we have new messages from 3 different people. Without actually reading those messages, we could leave the app. Even though those messages are still unread, the count for new messages going forward will now begin with 0. Thus, this is not the total number of unread messages. It is the number of new messages that we haven’t even glanced over or acknowledged the presence of or the number of newly unread messages.

![Screenshot 2023-02-01 at 8.54.09 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d434adea-52d7-4d08-bf58-4c0bc449cbf9/Screenshot_2023-02-01_at_8.54.09_PM.png)

The count for our example, not true universally, refers to the number of `unique people` from whom we have received newly unread messages.

![Screenshot 2023-02-01 at 8.57.51 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6bee267d-7f16-4c49-9739-6c84f578af53/Screenshot_2023-02-01_at_8.57.51_PM.png)

## System Design

Assumption: messaging service and messaging DB already exist. We only care here about the implementation of the counter mentioned above, which exists in parallel to the messaging service.

### v1

Write path:

- Have a Kafka that is triggered upon receiving a message, there will be consumers attached to that Kafka and each consumer will write to an Indicator DB where we’ll store the list of unique senders for each receiver. Since we want to store unique users, we can simply use sets for storing the unique senders with the key being the receiver.
    
    ![Screenshot 2023-02-01 at 10.03.43 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4c35f05-57f1-4846-bfee-a8f8f62e76e6/Screenshot_2023-02-01_at_10.03.43_PM.png)
    
- When do we trigger the Kafka? For all messages?
    
    - No. We don’t need to do the step above for users who are already online.
    - So, we’ll only trigger Kafka for users who are not online.
    - How to know if a user is offline?
        - We are likely using a WebSocket for sending messages from one user to another. So, if the WebSocket connection with the receiver is not present, we can consider the receiver offline (`ON_MSG_UNSENT` event)
        - Alternatively, we might have an offline/online indicator service that we can query to check if the user is online (`OFFLINE` event)
    
    ![Screenshot 2023-02-01 at 9.43.27 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba3e8a47-0ac1-43a9-aa63-24dcedb82afe/Screenshot_2023-02-01_at_9.43.27_PM.png)
    
- Here, since we are using Kafka, we can now do a bunch of things. For example, for offline users, we can send them email notifications mentioning that they have unread messages.
    

Read path:

- We just want to read the count of the newly unread messages here. So, we can make a simple GET request to fetch the count from the indicator DB. There are other complicated ways to do this by implementing a WebSocket, etc. This is a simpler implementation.
    
    ![Screenshot 2023-02-01 at 9.46.01 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a79c9cbb-ac2c-4b3e-a977-ccf023a67bc1/Screenshot_2023-02-01_at_9.46.01_PM.png)
    

### v2

How can we optimize both the read and write path?

Read Path:

- Which DB to use? We can simply use Redis. Any DB that gives us set-like functionality would do the job.
- Will one node for the DB be enough? The system is going to be read-heavy as we might make periodic calls from the frontend or the user might open the app and make a GET call. We could either partition the DB or use Read Replicas. Since it is a key-value DB, partitioning is easy to do. Thus, need a DB with distributed functionalities.

Write path:

- Which is the most brittle component of the write path? (ignore messaging service)
    - Kafka is not as it is distributed, gives fault tolerance, and replicates our events. This is safe.
    - The consumers are stateless. Safe.
    - The DB is still the point of concern even though it is distributed since the number of writes and reads happening on the DB is huge.
- Suppose a user is online and they received 1000 new messages from 10 unique users. In that case, we would be making 1000 writes and 990 of those writes won’t be changing the state of the Indicator DB. These are 990 useless writes that we are making to our most brittle component.
- How can we avoid useless writing?
    - We can store another DB that stores the set of senders instead of the Indicator DB. When Kafka receives an event, the consumer first checks this new auxiliary DB. If the user doesn’t already exist, only then it updates the Indicator DB, which now just stores the count of newly unread messages instead of the set of new senders.
    - This includes a tradeoff as this new DB will increase the infra cost and will increase the latency by a very small amount.
    - What kind of DB can we use? We can simply use Redis!

<aside> 💡 This is a new pattern - auxiliary DB!

This is done in a system that is both read and write-heavy (so, the DB becomes the most brittle component) and most of the writes are redundant (they have no impact on the statefulness of the system). We should be protecting the DB as much as possible. This is a very common pattern. Today, Load Balancers and Auto Scaling Services have solved most of the problems, DB still remains one. The auxiliary DB prevents the main DB from having to do unnecessary operations.

</aside>

- Finally, when we click on the app icon, the counter is reset. So, in that case, we’ll make another API call from the receiver to Delete the key corresponding to that receiver in both the Indicator DB and the auxiliary DB. This is another tradeoff as we have to make updates to both the DBs.

![Screenshot 2023-02-01 at 10.02.17 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4075a0e6-08d2-4129-9741-c33650242a7f/Screenshot_2023-02-01_at_10.02.17_PM.png)

![Screenshot 2023-02-01 at 10.04.22 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb209c41-6ebb-45cb-8e32-9b75cc2e777a/Screenshot_2023-02-01_at_10.04.22_PM.png)

- One might want to avoid read replicas as well as we are trying to protect the DB and read replicas increase the load on the master DB.

# Recommended Reads

- [Building a Notification Service](https://www.youtube.com/watch?v=kIP8L-CSl2Y&t=1080s)

[https://drive.google.com/file/d/1qzqxifcZzGY1veYhjoYTyZam9ogXjYSB/preview](https://drive.google.com/file/d/1qzqxifcZzGY1veYhjoYTyZam9ogXjYSB/preview)