---
title: Protecting Images
date: 2021-04-13
categories: linux
tags: [graphics, watermarks, resizing]
excerpt:
  How to protect pictures by adding watermarks, scaling and disabling the mouse right click option.
toc: true
---

# Protecting Images

## Scaling

Scale your pictures down, so that whilst they look good on your website the resolution is too low to produce a good printed copy. I always resize my pictures so the longest side is no more than 1024px and resolution is no greater than 90ppi.

## Disable Right Click

Another option is to disable the mouse right click option, thereby removing the ability to download the images from the web page. This is achieved by adding the following javascript to the `head` section of your webpages;

```java
<script>document.addEventListener('contextmenu', event => event.preventDefault());</script>
```

## Watermarks

Of course, as soon as your web page has been loaded the pictures will have been copied to the browsers cache, from where they could be saved. With that in mind, I would always recommend you add a watermark to your pictures. You will need to create a suitable watermark, and save it as a `.png`. Mine, which you will see in the bottom right corner of my pictures, is comprised of a line of text sitting on a grey background set to 50% opacity.

The watermark can be overlaid on the pictures using `Imagemagick`. The following script will apply the watermark to every `.jpg` image in the specified directory. The `-gravity` switch can be changed to other points of the compass. In my example `southeast` will place the watermark in the bottom right corner of the pictures. The numbers `320,21` are the width and height (in pixels) of the watermark as it will appear on the pictures.

```bash
mogrify -gravity southeast -geometry +10+10 -draw "image Over 0,0 320,21 '/home/paul/watermark.png'" *.jpg
```

## Automating the Process

Finally, and to make the process straightforward, I have written a script that combines the resizing and watermarking of the pictures, as follows;

```bash
#!/bin/bash

RED='\033[1;31m'
GREEN='\033[0;32m'
NOCOLOR='\033[0m'

echo
echo "This script will resize '.jpg' files in the current directory and apply a watermark to each."

echo -e $RED
cwd=$(pwd)
echo -e "You are currently at '$cwd'"
echo
read -p "Do you wish to proceed (y/n)?" choice
echo -e $NOCOLOR

case $choice in
	y|Y )
		echo "Resizing..."
		echo
		mogrify -resize 1024 -quality 80  *.jpg

		echo "Applying watermark..."
		echo
		mogrify -gravity southeast -geometry +10+10 -draw "image Over 0,0 320,21 '/home/paul/watermark.png'" *.jpg
	;;

	n|N )

		echo "Script terminated" ;;

	* )
		echo "Invalid selection. Script terminated" ;;

esac
```

