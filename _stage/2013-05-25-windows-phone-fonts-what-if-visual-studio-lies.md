---
layout: post
title: "Windows Phone Fonts & what if Visual Studio lies"
date: 2013-05-25 10:51
author: antje.kilian
comments: true
categories: [Uncategorized]
tags: []
language: en
---
{% include JB/setup %}
<img style="background-image: none; padding-left: 0px; padding-right: 0px; padding-top: 0px; border: 0px;" title="image.png" src="http://code-inside.de/blog/wp-content/uploads/image1828-278x194.png" border="0" alt="image.png" width="278" height="194" />

Today I was confronted with a little Problem: my Windows Phone App refused to show me the Font I choose – also other thinks didn’t work.

Although the Visual Studio Designer did show the Fonts:

<img style="background-image: none; padding-left: 0px; padding-right: 0px; padding-top: 0px; border: 0px;" title="image" src="http://code-inside.de/blog/wp-content/uploads/image_thumb981.png" border="0" alt="image" width="299" height="502" />

Unfortunately there isn’t much left in the Emulator:

<a href="http://code-inside.de/blog-in/wp-content/uploads/image_thumb982.png"><img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border: 0px;" title="image_thumb982" src="http://code-inside.de/blog-in/wp-content/uploads/image_thumb982_thumb.png" border="0" alt="image_thumb982" width="267" height="457" /></a>

Reason for this:

<strong>Windows Phone doesn’t include all the typos Windows does</strong>

That means while choosing a certain typo you should pay attention if they are compatible with the windows phone.

I found these two pages with a list of the supported Fonts:

<a href="http://msdn.microsoft.com/en-us/library/ff806365%28v=vs.95%29.aspx">Fonts in Silverlight for Windows Phone</a>

<a href="http://msdn.microsoft.com/en-us/library/windowsphone/develop/cc189010(v=vs.105).aspx">Text and fonts for Windows Phone</a>

P.S: Don’t worry, Comic Sans is still working <img class="wlEmoticon wlEmoticon-winkingsmile" style="border-style: none;" src="http://code-inside.de/blog-in/wp-content/uploads/wlEmoticon-winkingsmile54.png" alt="Zwinkerndes Smiley" />
