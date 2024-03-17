---
title: Convertible Using Ffmpeg to Convert Audio Files
full Title: Convertible Using Ffmpeg to Convert Audio Files
author: quantixed
URL: https://quantixed.org/2021/11/20/convertible-using-ffmpeg-to-convert-audio-files/
published date: 2021-11-20
category: articles
source: reader
tags: [life, pal, medium/articles, author/quantixed, reader/reader, date/2024-03-03, area/reader]
created: 2024-03-17
assigned to: people/pal
priority: P4
work: document
---
author:: [[quantixed]]
note:: 
source:: [[reader]]
url:: [articles URL](https://quantixed.org/2021/11/20/convertible-using-ffmpeg-to-convert-audio-files/)
image_url:: [articles image URL](https://i0.wp.com/quantixed.org/wp-content/uploads/2017/12/cropped-qlogo512x512-01.png?fit=512%2C512&ssl=1)
category:: [[articles]]
date:: [[2024-03-17]]
last_highlighted_date:: [[2024-03-03]]
published_date:: [[2021-11-20]]
summary:: The document provides a tech tip on using ffmpeg, a command-line tool, to convert audio files, specifically addressing the conversion of opus files to mp3. It explains the commands needed for the conversion, including how to transfer metadata. Additionally, it offers a one-liner command to convert multiple files in folders and subfolders, enhancing the process compared to using Audacity. The author concludes that this workflow is more efficient for converting files and transferring metadata and artwork, preferring it over their previous method.

![rw-book-cover](https://i0.wp.com/quantixed.org/wp-content/uploads/2017/12/cropped-qlogo512x512-01.png?fit=512%2C512&ssl=1)

## Highlights
### id687332179
[[2024-03-02]] 23:47
> `find` `. -iname` `'*.opus'` `-``exec` `bash` `-c` `'D=$(dirname "{}"); B=$(basename "{}"); mkdir "$D/mp3/"; ffmpeg -i "{}" -ab 320k -map_metadata 0:s:a:0 -id3v2_version 3 "$D/mp3/${B%.*}.mp3"'` `\;`


