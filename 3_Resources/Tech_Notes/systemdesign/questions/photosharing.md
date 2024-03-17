
Facebook, Instagram

𝗛𝗼𝘄 𝘁𝗼 𝗗𝗲𝘀𝗶𝗴𝗻 𝗜𝗻𝘀𝘁𝗮𝗴𝗿𝗮𝗺?
Let's discuss the design of a photo-sharing service like Instagram.

𝟭. 𝗥𝗲𝗾𝘂𝗶𝗿𝗲𝗺𝗲𝗻𝘁𝘀:
Functional requirements:
-Users should be able to upload/view photos.
-Users can follow/unfollow other users.
-The system should generate Newsfeed for users.

Non-functional Requirements:
-Highly available and reliable service.
-Consistency can take a hit in favor of availability.


𝟮. 𝗗𝗮𝘁𝗮𝗯𝗮𝘀𝗲 𝗦𝗰𝗵𝗲𝗺𝗮
We need to store data about users, their uploaded photos, and the people they follow.

-User (ID, name, email)
-Photo (ID, userID, title, photoPath, location, creationDate)
-UserFollow (followerID, followeeID)


𝟯. 𝗛𝗶𝗴𝗵 𝗟𝗲𝘃𝗲𝗹 𝗗𝗲𝘀𝗶𝗴𝗻
At a high level, we need to support two scenarios, one to upload photos and the other to view photos. Our service would need some blob storage servers to store photos and some database servers to store metadata information.

𝟰. 𝗗𝗲𝘁𝗮𝗶𝗹𝗲𝗱 𝗦𝘆𝘀𝘁𝗲𝗺 𝗗𝗲𝘀𝗶𝗴𝗻
Photo uploads can be slow as they have to go to the disk/storage, whereas reads will be faster, especially when served from the cache. Secondly, our system will be read-heavy. So, to make things efficient, we can have separate servers to serve read and write traffic. This will also allow us to scale and optimize these two operations independently.

𝗮) 𝗥𝗲𝗮𝗱 𝗮𝗻𝗱 𝘄𝗿𝗶𝘁𝗲 𝘄𝗼𝗿𝗸𝗳𝗹𝗼𝘄
Here is the detailed workflow for a photo upload operation:

-All clients will hit the API gateway, which will be the single entry point to our system, distributing the traffic to application servers. We will have dedicated servers for read/write traffic.
-The app-server (write) will do three things. 1) Insert metadata to the database, 2) Upload photo to a cloud blob storage (local or S3), 3) Insert a task in a distributed queue to add this photo to relevant users' newsfeeds. A separate 'Feed Generation Service' (FGS) will work on these tasks to add new photos to relevant users' newsfeeds and store the newsfeed metadata in the database.

The read operations will be served by reading metadata from the cache (Redis/Memcached) and the photo from CDN/blob storage.

𝗯) 𝗗𝗮𝘁𝗮 𝗽𝗮𝗿𝘁𝗶𝘁𝗶𝗼𝗻𝗶𝗻𝗴
To support millions of users, we need to partition the metadata. We can partition based on UserID so that each user's data is stored on one shard.

𝗰) 𝗡𝗲𝘄𝘀𝗳𝗲𝗲𝗱 𝘀𝗲𝗿𝘃𝗶𝗻𝗴
How will we serve newsfeed updates to a user? The user can fetch the newsfeed from the server/cache. Later, the client application can check the server for updates at regular intervals, or the server can push a notification to the client application whenever updates are available.

📌 Ref: 𝗚𝗿𝗼𝗸𝗸𝗶𝗻𝗴 𝘁𝗵𝗲 𝗦𝘆𝘀𝘁𝗲𝗺 𝗗𝗲𝘀𝗶𝗴𝗻 𝗜𝗻𝘁𝗲𝗿𝘃𝗶𝗲𝘄 - https://lnkd.in/giwyzfkT