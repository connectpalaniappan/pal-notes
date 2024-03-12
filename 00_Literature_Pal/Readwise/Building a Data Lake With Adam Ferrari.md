# Building a Data Lake With Adam Ferrari

![rw-book-cover](https://wsrv.nl/?url=http%3A%2F%2Fsoftwareengineeringdaily.com%2Fwp-content%2Fuploads%2F2024%2F02%2Fsed_logo.png&w=100&h=100)

## Metadata
- Author: [[Software Engineering Daily]]
- Full Title: Building a Data Lake With Adam Ferrari
- Category: #podcasts
- URL: https://share.snipd.com/episode/dc0b821f-c59a-4d6b-8129-a47ce47ce1b5

## Highlights
- Advantages of Trino Engine and Iceberg Tables
  Summary:
  The Trino Engine is highly efficient for data exploration and quick responses, enabling users to swiftly access and analyze data in real-time.
  Iceberg tables have gained popularity for their advanced features like integration with parquet files and a directory of files that enhance data organization and retrieval compared to traditional formats.
  Transcript:
  Speaker 1
  Yeah, certainly. I mean, I will say though, it's maybe not for the most demanding real time, but it's amazing. The Trino Engine is blisteringly fast. And so I used it for years before joining Starburst and as an interactive user just trying to get at my data. And it's really amazingly conducive to data exploration, you know, getting quick answers to questions. I remember a lot of times being in meetings and a question coming up and just being able to quickly like type some sequel answer business question real time. So it's great, especially I think for, you know, like that kind of human data access, it's amazingly fast. And again, it depends. It depends on like how smart you've set up your data and like it depends on all those variables. But in terms of what you tend to deliver on it, it is actually a pretty amazing technology.
  Speaker 2
  And you mentioned iceberg tables a couple of times. And I feel like it's something that is becoming more and more popular. And it feels like, you know, the way to the industry is kind of leaning towards iceberg tables moving away from other types of formats. What is it that iceberg tables are doing that has made them popular? And what is it, you know, how is it different than essentially some of the formats that had been used in the past?
  Speaker 1
  I mean, it's really beautiful in that it layers on all the work of formats of like it layers on things like par K. So if you were to actually, if you look at an iceberg, it's actually it's a whole directory of files underneath there in the iceberg table. And there are different segments and updates and parts of that table structure. If you then crack into one of the underlying leaf files, it's going to be a par K or similar. ([Time 0:24:09](https://share.snipd.com/snip/b5ad3924-805e-4608-b001-00ab86dd3826))
# Building a Data Lake With Adam Ferrari

![rw-book-cover](https://wsrv.nl/?url=http%3A%2F%2Fsoftwareengineeringdaily.com%2Fwp-content%2Fuploads%2F2024%2F02%2Fsed_logo.png&w=100&h=100)

## Metadata
- Author: [[Software Engineering Daily]]
- Full Title: Building a Data Lake With Adam Ferrari
- Category: #podcasts
- URL: https://share.snipd.com/episode/dc0b821f-c59a-4d6b-8129-a47ce47ce1b5

## Highlights
- Advantages of Trino Engine and Iceberg Tables
  Summary:
  The Trino Engine is highly efficient for data exploration and quick responses, enabling users to swiftly access and analyze data in real-time.
  Iceberg tables have gained popularity for their advanced features like integration with parquet files and a directory of files that enhance data organization and retrieval compared to traditional formats.
  Transcript:
  Speaker 1
  Yeah, certainly. I mean, I will say though, it's maybe not for the most demanding real time, but it's amazing. The Trino Engine is blisteringly fast. And so I used it for years before joining Starburst and as an interactive user just trying to get at my data. And it's really amazingly conducive to data exploration, you know, getting quick answers to questions. I remember a lot of times being in meetings and a question coming up and just being able to quickly like type some sequel answer business question real time. So it's great, especially I think for, you know, like that kind of human data access, it's amazingly fast. And again, it depends. It depends on like how smart you've set up your data and like it depends on all those variables. But in terms of what you tend to deliver on it, it is actually a pretty amazing technology.
  Speaker 2
  And you mentioned iceberg tables a couple of times. And I feel like it's something that is becoming more and more popular. And it feels like, you know, the way to the industry is kind of leaning towards iceberg tables moving away from other types of formats. What is it that iceberg tables are doing that has made them popular? And what is it, you know, how is it different than essentially some of the formats that had been used in the past?
  Speaker 1
  I mean, it's really beautiful in that it layers on all the work of formats of like it layers on things like par K. So if you were to actually, if you look at an iceberg, it's actually it's a whole directory of files underneath there in the iceberg table. And there are different segments and updates and parts of that table structure. If you then crack into one of the underlying leaf files, it's going to be a par K or similar. ([Time 0:24:09](https://share.snipd.com/snip/b5ad3924-805e-4608-b001-00ab86dd3826))
