---
layout: post
title: VSCO-like presets online, a side project
tags: image-research vsco
categories: developer
date:   2017-01-30 15:05:14 -0500
comments: true
--- 

[__VSCO__](https://vsco.co) has been one of the most popular mobile apps for editing and filtering images. 
If you are a photographer, you probably know that there is also a VSCOFilm - a set of Lightroom presets 
for easy image filtering.


The algorithms VSCO used are pretty complicated, which means it's kind of hard to imitate. But if you simply type "VSCO online" into Google, 
a website named [_VSCO-like Filters Online_](http://maxim-xu.github.io/vsco-like) would show up.

<img style="width:100%;display:inline-block" alt="vsco online search result" src="{{ site.baseurl }}/public/images/vsco-online-search-result.png" />
<br />
<img style="width:100%;display:inline-block" alt="vsco online search result" src="{{ site.baseurl }}/public/images/screenshot-vsco-like.png" />
Yep. This is my work.

I made it not because I am an expert of making filters or image research (which I'm definitely not), but because 
no one else made a thing that allows people to apply VSCO image filters without installing anything. To be more specific, I couldn't find anything if I google '_VSCO online_' or '_VSCO filters online_' 
before I made it myself!

Don't get me wrong. This is definitely _not_ something. You may wonder how I managed to make VSCO-like filters 
onto the web. It's actually easier than you'd think - as long as you have the Lightroom presets.

<img style="width:48%;display:block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/curve1.png" />
In Lightroom (I actually used Adobe Camera Raw), once you've satisfied with the filtering or enhancing work, just click _save settings..._. 
You'll be saving an XMP file, which could be opened in a text editor and would look like this: 

<img style="width:100%;display:inline-block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/xmp-screenshot.png" />
Scroll down a little bit, you'll find the __RGB Curve Points__ for the FUJI Astia 100F preset.

<img style="width:50%;display:block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/xmp-curves.png" />
Now that we've got the key optical values of the filter, we're going to implement it in _Javascript_ 
 with the help of a canvas manipulation library called [__CamanJS__](http://camanjs.com/).

<img style="width:100%;display:block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/astia-js.png" />
Add a little bit saturation value to colorize a little...<br />
Add a little bit noise (grain) to make it more like a film photo...<br />
Finally, set the RGB curves, which really is the essentail part of the filter...
Done!

__Before__
<img style="width:100%;display:block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/vsco-before.jpg" />
__After__ (FUJI Astia 100F )
<img style="width:100%;display:block; margin-left:0" alt="bw Photo" src="{{ site.baseurl }}/public/images/vsco-after.jpeg" />

It's not perfect, and I doubt it'll ever be...But at least it works!