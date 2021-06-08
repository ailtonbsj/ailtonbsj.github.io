---
layout: post
title:  "Some utils commands and tools for multimedia"
date:   2019-05-10 14:01:00 -0300
categories: tutorial linux video
---
This is a list of some utils command for linux tool for multimedia:
```bash
# Slice part of video in mp4
# Where:
# -ss   is initial time position,
# -to   is final time position,
# -t    is the duration of video
ffmpeg -i src.mp4 -ss 00:00:10 -to 00:00:40 -vcodec libx264 -acodec copy out.mp4
ffmpeg -i src.mp4 -ss 00:00:10 -t 00:00:30 -vcodec copy -acodec copy out.mp4


# Resize all images
mogrify -resize 600 *.jpg
mogrify -resize x400 *.jpg

# Remove EXIF and apply rotation
mogrify -auto-orient *.jpg

# Remove EXIF
mogrify -strip *.jpg

# Change quality of all images
mogrify -quality *.jpg

# Convert all images
mogrify -format png -path out *.jpg

# Convert to pdf
convert input.jpg -page a4 output.pdf

# Crop multiples images with size and offset
convert -extract 150x150+0+0 *.jpg prefix.jpg

# Image to Text OCR
sudo apt install tesseract-ocr

# Autocrop images
autocrop -i folderIn -o folderOut -r folderErr

```
This script rename files sequentially:
```bash
#!/bin/bash

# DESCRIPTION: Rename a lot of files sequentially
# USAGE:
#   ./thisscript.sh *.jpg

filesArr=("$@")
sizeFiles="${#filesArr[@]}"
totalDigits=${#sizeFiles}
counter=0
for f in "$@"; do
	((counter++))
	mv $f $(printf "%0""$totalDigits""d.${f##*.}" $counter)
done
```


This script automatic rename photos with text inside:
```bash
#!/bin/bash

# DESCRIPTION: Rename image based of content using OCR
# USAGE:
#   ./thisscript.sh *.jpg

for f in "$@"; do
    #convert -extract 181x85+0+0 input.jpg s1.jpg
    convert -extract 55x24+135+25 "$f" /tmp/s1.jpg

    #convert -extract 181x85+0+85 input.jpg s2.jpg
    convert -extract 181x40+0+130 "$f" /tmp/s2.jpg

    convert -density 300 /tmp/s1.jpg -colorspace Gray -negate -depth 8 -strip -background white -alpha off /tmp/1.tiff
    convert -density 300 /tmp/s2.jpg -colorspace Gray -depth 8 -strip -background white -alpha off /tmp/2.tiff

    tesseract --psm 7  /tmp/1.tiff /tmp/1
    tesseract --psm 7  /tmp/2.tiff /tmp/2

    mv "$f" "$(sed 's/[^0-9]//g' /tmp/1.txt),$(sed 's/[^A-Za-z ]//g' /tmp/2.txt | xargs).jpg"
done
```
