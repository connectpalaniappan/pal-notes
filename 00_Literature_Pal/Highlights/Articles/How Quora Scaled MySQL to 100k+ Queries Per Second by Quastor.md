---
title: How Quora Scaled MySQL to 100k+ Queries Per Second
full Title: How Quora Scaled MySQL to 100k+ Queries Per Second
author: Quastor
URL: 
published date: 2024-03-30
category: articles
source: reader
tags: [medium/articles, author/Quastor, reader/reader, date/2024-03-30, area/reader]
created: 2024-03-30
assignedTo: people/pal
priority: P4
work: document
---
author:: [[Quastor]]
note:: 
source:: [[reader]]
url:: 
image_url:: [articles image URL](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)
category:: [[articles]]
date:: [[2024-03-30]]
last_highlighted_date:: [[2024-03-30]]
published_date:: [[2024-03-30]]
summary:: Vamsi Ponnekanti is a software engineer at Quora and he wrote a fantastic article delving into the different factors of database load and the specific steps the engineering teams took for optimization.


![rw-book-cover](https://readwise-assets.s3.amazonaws.com/static/images/article3.5c705a01b476.png)

## Highlights
### id700191781
[[2024-03-30]] 17:28
> Scaling Database Reads with Caching and Query Optimization

- [n] [[caching]] and query optimization for scaling  * [View Highlight](https://read.readwise.io/read/01ht8qjrd15pnyw6ep7xt4ksfq)


## New highlights added April 5, 2024 at 1:41 PM
### id702705770
[[2024-04-05]] 12:59
> **Read Volume** - How many read requests can you handle per second. Quora scaled this with improving their caching strategy (changing the structure to minimize cache misses) and also by optimizing inefficient read queries.


### id702705784
[[2024-04-05]] 13:00
> **Write Volume** - How many write requests can you handle per second. Quora isn’t a write-heavy application. The main issue they were facing was with replication between the primary-replica nodes. They fixed it by changing how writes are replayed


### id702705796
[[2024-04-05]] 13:00
> **Data Size** - How much data is stored across your disks. Quora optimized this by switching the MySQL storage engine from InnoDB (*the default*) to RocksDB.


### id702705861
[[2024-04-05]] 13:01
> **Large Scan Queries** - If you have a query that’s scanning a large number of rows, change it to use [pagination](https://link.mail.beehiiv.com/ss/c/u001.LUZYrxblx92g0_IcD8eBHXxUIcBGV_xFdUN9QhvXB5qkb1thcmZxLoMCQHVpaeykxXOBfB0_JeIiZEUFlWNOL6VydGZT8JIyPsKWc4-15UyT4r7jqb48JPCPzWoAH9dwbTcDym3IDN1m44nPdaG-dgnn3SmcCnsusvdfOJ7Qz6N0qhgAbzZNOvvZ-f6F1o8ipGSPn7dVzJLz328xVUCAXin0ZP_nknTkqcANs0slhvmeZ-Jn6IYnIOsi0gsXyNW3CEMp3icfCdsLA6lIeXaC0KWDJ1Ft0eKwvmGh3xPsqXU/453/VgpKnf6jR2ud19Tke0QlIQ/h25/h001.kUuRJ_KmcFaQsI0feWF_ujZsyzUg8KP4F8sjmtDjQ0U) so that query results are retrieved in smaller chunks. This helps ensure the database isn’t doing unnecessary work.


### id702706577
[[2024-04-05]] 13:09
> **Slow Queries** - There’s many reasons a query can be slow: no good index, unnecessary columns being requested, inefficient joins, etc. [Here’s](https://link.mail.beehiiv.com/ss/c/u001.iOwnnfCBjAhkBYm2nnsew0TY_eelKhWz37x6sGqE3SUZbF1L2RLYsaF66-vIFpAe2bHMsAZ_-cdtrsrk7x9CE3W2hUN6w2sbmfiXsDnPDIUdAHSXcnORehhMKRrAX1Sj-ba9ts4DqVGIkvldT3GaCT9hadVVcTOkP-DNMvEfcDp0YqMqnVtGysV83_77oRXVbgEJkWMlaz2ol2tvvyeO8rHFkDclU_0sFgAbki2Ii1LhcSFBGxXTkAXpZnHUSAoqkNgg6Z11M7DAhX1RReS7yxGkUcfIahv46SSmBoVn4cM/453/VgpKnf6jR2ud19Tke0QlIQ/h26/h001.2xt2r0skmTvHXxdrM--HEcWG5s_oQckOfFcHKSEptBI) a good blog post on how to find slow queries and optimize them.


### id702706790
[[2024-04-05]] 13:13
> they found that inefficient caching (lots of cache misses) was the cause for a lot of unnecessary database load.


### id702707186
[[2024-04-05]] 13:14
> **Fetching a user’s language preferences** - Quora needed to check what languages a user understands. Previously, they’d query the cache with *(user_id, language_id)* and receive a yes/no response. A query of *(carlos_sainz, spanish)* would be checking if the user Carlos Sainz understood spanish. They’d run this query for all 25 languages Quora supported - (*carlos_sainz, english*), (*carlos_sainz, french*)*,* etc. 
> This led to a large key-space for the cache (*possible keys were all user_ids multiplied by the number of languages*) and it resulted in a huge amount of cache misses. People typically just know 1 or 2 languages, so the majority of these requests resulted in *No*. This was causing a lot of unnecessary database load. 
> Quora changed their cache key to just using the user id (*carlos sainz*) and changed the payload to just send back all the languages the user knew. This increased the size of the payload being sent back (*a list of languages instead of just yes/no*) but it meant a significantly higher cache hit rate.
> With this, Quora reduced the QPS on the database by over 90% from these types of queries


## New highlights added April 5, 2024 at 8:22 PM
### id702743749
[[2024-04-05]] 15:31
> **Inefficient Caching for Sparse Data Sets** - Another issue with caching that Quora frequently ran into was with *sparse* data sets in one dimension. For example, they might have to query the database to see if a certain question needs to be redirected to a different question (*this might happen if the same question is reposted*).
> The vast majority of questions *don’t* need to be redirected so Quora would be getting only a few “redirects” and a large number of “don’t redirect”.
> When they just cached by *question_id*, then the cache would be filled with *No’s* and only a few *Redirects*. This took up a ton of space in the cache and also led to a ton of cache misses since the number of “redirects” was so sparse. 
> Instead, they started caching *ranges*. If question ids *123* - *127* didn’t have any redirects for any of the questions there, then they’d cache that range has having all No’s instead of caching each individual question id. This led to large reductions in database load for these types of queries, with QPS dropping by 90

- [n] Cache:: 
   Optimization:: cache misses + number, use range cache to reduce the cache size thereby the cache misses too.  * [View Highlight](https://read.readwise.io/read/01htqz8a97eqy1dhcttw9pk42e)


### id702750177
[[2024-04-05]] 15:32
> Having optimal data retention policies is crucial.

- [n] Database optimization:: 
   Storage, retain only needed data i.e. archive historical data  * [View Highlight](https://read.readwise.io/read/01htqzcq8962v7dytpbpm45x5q)


### id702753168
[[2024-04-05]] 15:34
> RocksDB is a key-value store developed at Facebook that is a fork of Google’s [LevelDB](https://link.mail.beehiiv.com/ss/c/u001.GaP25kixWOTuE1E3XPYxBYaNyUGZyVKJhuXIbGlJOOLuvMNvHIad8AFKiSEY72NkOFjilok25hzwpFkRw2NlcYbJ8cJVST_euXXOZ31Jg4cpsKeBLhxrl3z8DFoLMpUGbxq3I9blX6ZvDZ-LxOuUGLMu0GSgtYFqeY3QnNUeCXVJs63cjUsH4JubjVskOBuCWoZg7uOhXC-dE44KTYutuQ/453/VgpKnf6jR2ud19Tke0QlIQ/h28/h001.GzsjHeREUcOCu3sjpLzV9ubVZPmt1wRwD4VbMlgN-Xg). It’s commonly swapped in as the storage engine (the storage engine is responsible for how data is stored and retrieved from disk) for NoSQL databases.

- [n] Rocksdb storage engine is better than innodb storage engine, interms of space efficiency.  * [View Highlight](https://read.readwise.io/read/01htqzeby1dja92y6bt0wz16pr)


### id702754286
[[2024-04-05]] 15:42
> One of the big benefits is increased compression efficiency. Your data is written to disk in a block of data called a *[page](https://link.mail.beehiiv.com/ss/c/u001.iOwnnfCBjAhkBYm2nnsew8YInh8ddto0Hd0zDoUzjAb09zpDZRZhHdfe8oXl08HH7XNL7uJVu6fieDCaqHahM-Men6WPIQb9xaWDeySuzt6udeYjmOpaztkeOf-J67vOtGsmIa5LAf6VXdgnYAwS_pvRUZzfZMkc8hEvDho8KDmVRcOJPOk2JC0_3hvrt33-ytVfaz4zm0kFbJNYgckhaTQVumo1uWzuS0FoFhzgpQ8tA1JMeLJcqi5LsUSBXNOY/453/VgpKnf6jR2ud19Tke0QlIQ/h33/h001.J1w3H3upwhjshSuXACxsqY1DanqFPTREUzpF1I0GTTE)*. Databases can read/write data one page at a time. When you request a particular piece of data, then the entire page is fetched into memory.
> With InnoDB, page sizes are fixed (default is 16 KB). If the data doesn’t fill up the page size, then the remaining space is wasted. This can lead to extra fragmentation.
> With RocksDB, you have variable page sizes. This is one of the biggest reasons RocksDB compresses better. For an in-depth analysis, I’d highly suggest reading the Facebook [blog post](https://link.mail.beehiiv.com/ss/c/u001.GaP25kixWOTuE1E3XPYxBaCcSR5Ag7fjcGmLGcrBjv-YKG5vsJv-sQ6j6ysikRbnTGugkVzLCgiDPXUWx0i2KEMcgKGVHuDbC4Oj2U-lk3OEBrjsfbZVqUveOp09pH_-iszKq3i16yLMxEKQGATYPSsn4Z75DKMjwP4dyO5s2GoltvWK-Euib67hErxN3YlQut2GM2mw1wXLJ0ZUPe5E0teUPjnPz5lHDGN6Q11-LW-VAhKPM7gSKkRrdrAtF8YQ9yLIanKI50DGHP26QDC_y8Hqwkg_ty6TLBc8CoQ8BWo/453/VgpKnf6jR2ud19Tke0QlIQ/h34/h001.9zfr0RI_tbbfkfWRM8CczLOt34EiI3Mp69bn8qSvtZs).
> Facebook was able to cut their storage usage *in half* by migrating to MyRocks.
> At Quora, they were able to see an 80% reduction in space for one of their tables. Other tables saw 50-60% reductions in space.

- [n] Storage optimization:: rocksdb has efficient compression efficiency 
   Variable size of rocksdb help to make the space more efficient instead of fixed size pages offered by innodb 
   Is there a metric for storage size reduction? #people/pal  * [View Highlight](https://read.readwise.io/read/01htqzg9ef4nxt6qpn7bcnw6p4)


### id702755337
[[2024-04-05]] 15:44
> With Quora, their database load *is not* write heavy. If they had any write-heavy workloads, then they used [HBase](https://link.mail.beehiiv.com/ss/c/u001.GaP25kixWOTuE1E3XPYxBYaNyUGZyVKJhuXIbGlJOOK1tjgqFF3S1QAJyhGby4nnleRT6FaOStHgTaon2RomF_nrxAjd8RsGeOACkyPSqSeGfDCVRuW5uib02Zk4HowinJzrd6BGIDagUKp3Sku3E75ZmI2yeXmO3FnivemPurvmbFGu4pTbKCFVeygA4NN5QMPWqKP9vnbWi5nz2ZALIokKbFIDU4wV8hAzDpqZPSQ/453/VgpKnf6jR2ud19Tke0QlIQ/h35/h001.rOIriuWluKZUM_j8BxfrAZFXYm1GPbsnrcDbjAkme_4) (a write-optimized distributed database modeled after Google [Bigtable](https://link.mail.beehiiv.com/ss/c/u001.GaP25kixWOTuE1E3XPYxBYaNyUGZyVKJhuXIbGlJOOJeek1AmlZ8smvHQDL0DOXqwNA-6cn8XUHIHotjf5_8IqY23rliOUQnDB6yUdjikEd1HkzN05ABNiufLwruceX_Mr-Qnfa6OgN_fihLm-q59fwQv2WpqzR41PHLqgubSNQhmnuwtkrAhrNzdIxtWicXLObdLxANP-aROV_i5qdCig/453/VgpKnf6jR2ud19Tke0QlIQ/h36/h001.AfIVYm9dXQ0dWis7S_9JJNNhEAmrYaLXXJAdlfGottk)) instead of MySQL.

- [n] Write heavy, quora use a column wide data store such as hbase. Otherwise the default is MySQL.  * [View Highlight](https://read.readwise.io/read/01htqzz76stwfk59wg46h9j4rw)


### id702818161
[[2024-04-05]] 18:48
> core issue was that replication replay writes happen *sequentially* by default, even if the writes happened concurrently on the primary.

- [n] How can writes happen concurrently at primary? 
   Optimization:: replaced sequential replication to parallel replication.  * [View Highlight](https://read.readwise.io/read/01htragwb60fc962bgn1ya6ca8)


### id702818246
[[2024-04-05]] 18:48
> temporary solution Quora used was to move heavy-write tables off from one MySQL primary node onto another node with less write pressure.

- [n] Moving the write load to a different node alleviated the load pressure. But was not scalable.  * [View Highlight](https://read.readwise.io/read/01htrakgj6z8yx9q41pkt1wwgx)


### id702818314
[[2024-04-05]] 18:53
> permanent solution was to incorporate MySQL’s parallel replication writes feature.

- [n] Parallel replication feature was more helpful with consistency.  * [View Highlight](https://read.readwise.io/read/01htran1nqphx6k55ref1hrqqy)


