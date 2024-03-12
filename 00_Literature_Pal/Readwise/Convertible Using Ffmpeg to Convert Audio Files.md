# Convertible: Using Ffmpeg to Convert Audio Files

![rw-book-cover](https://i0.wp.com/quantixed.org/wp-content/uploads/2017/12/cropped-qlogo512x512-01.png?fit=512%2C512&ssl=1)

## Metadata
- Author: [[quantixed]]
- Full Title: Convertible: Using Ffmpeg to Convert Audio Files
- Category: #articles
- Document Tags: [[life]] [[Pal]] [[status/highlight_pending]] 
- Summary: The document provides a tech tip on using ffmpeg, a command-line tool, to convert audio files, specifically addressing the conversion of opus files to mp3. It explains the commands needed for the conversion, including how to transfer metadata. Additionally, it offers a one-liner command to convert multiple files in folders and subfolders, enhancing the process compared to using Audacity. The author concludes that this workflow is more efficient for converting files and transferring metadata and artwork, preferring it over their previous method.
- URL: https://quantixed.org/2021/11/20/convertible-using-ffmpeg-to-convert-audio-files/

## Highlights
- `find` `. -iname` `'*.opus'` `-``exec` `bash` `-c` `'D=$(dirname "{}"); B=$(basename "{}"); mkdir "$D/mp3/"; ffmpeg -i "{}" -ab 320k -map_metadata 0:s:a:0 -id3v2_version 3 "$D/mp3/${B%.*}.mp3"'` `\;` ([View Highlight](https://read.readwise.io/read/01hr1dmkjkby6yw960ffscfjgw))
# Convertible: Using Ffmpeg to Convert Audio Files

![rw-book-cover](https://i0.wp.com/quantixed.org/wp-content/uploads/2017/12/cropped-qlogo512x512-01.png?fit=512%2C512&ssl=1)

## Metadata
- Author: [[quantixed]]
- Full Title: Convertible: Using Ffmpeg to Convert Audio Files
- Category: #articles
- Document Tags: [[life]] [[pal]] [[status/highlight_pending]] 
- Summary: The document provides a tech tip on using ffmpeg, a command-line tool, to convert audio files, specifically addressing the conversion of opus files to mp3. It explains the commands needed for the conversion, including how to transfer metadata. Additionally, it offers a one-liner command to convert multiple files in folders and subfolders, enhancing the process compared to using Audacity. The author concludes that this workflow is more efficient for converting files and transferring metadata and artwork, preferring it over their previous method.
- URL: https://quantixed.org/2021/11/20/convertible-using-ffmpeg-to-convert-audio-files/

## Highlights
- `find` `. -iname` `'*.opus'` `-``exec` `bash` `-c` `'D=$(dirname "{}"); B=$(basename "{}"); mkdir "$D/mp3/"; ffmpeg -i "{}" -ab 320k -map_metadata 0:s:a:0 -id3v2_version 3 "$D/mp3/${B%.*}.mp3"'` `\;` ([View Highlight](https://read.readwise.io/read/01hr1dmkjkby6yw960ffscfjgw))
# Convertible: Using Ffmpeg to Convert Audio Files

![rw-book-cover](https://i0.wp.com/quantixed.org/wp-content/uploads/2017/12/cropped-qlogo512x512-01.png?fit=512%2C512&ssl=1)

## Metadata
- Author: [[quantixed]]
- Full Title: Convertible: Using Ffmpeg to Convert Audio Files
- Category: #articles
- Document Tags: [[life]] [[pal]] [[work/highlight]] 
- Summary: The document provides a tech tip on using ffmpeg, a command-line tool, to convert audio files, specifically addressing the conversion of opus files to mp3. It explains the commands needed for the conversion, including how to transfer metadata. Additionally, it offers a one-liner command to convert multiple files in folders and subfolders, enhancing the process compared to using Audacity. The author concludes that this workflow is more efficient for converting files and transferring metadata and artwork, preferring it over their previous method.
- URL: https://quantixed.org/2021/11/20/convertible-using-ffmpeg-to-convert-audio-files/

## Highlights
- `find` `. -iname` `'*.opus'` `-``exec` `bash` `-c` `'D=$(dirname "{}"); B=$(basename "{}"); mkdir "$D/mp3/"; ffmpeg -i "{}" -ab 320k -map_metadata 0:s:a:0 -id3v2_version 3 "$D/mp3/${B%.*}.mp3"'` `\;` ([View Highlight](https://read.readwise.io/read/01hr1dmkjkby6yw960ffscfjgw))
