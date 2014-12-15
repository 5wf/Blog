---
layout: post
title: "404-Error: Directory beats ASP.NET MVC Routing"
date: 2012-07-29 12:04
author: CI Team
comments: true
categories: [Uncategorized]
tags: []
language: en
---
{% include JB/setup %}

  

<p>I had a little routing problem with an ASP.NET MVC website and the solution brought me a little “Ah! Logic!” Experience – maybe some of you are familiar with this problem as well <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Zwinkerndes Smiley" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-winkingsmile42.png" /></p>
<p><b>Problem:</b></p>
<p>I had a controller named “ReportingController” and I can’t open it with localhost/Reporting. Not even the Debugger worked – just a 404. Localhost/Reporting/Index worked properly and after I simply renamed the controller it worked! (The WTF moment <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Zwinkerndes Smiley" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-winkingsmile42.png" />)</p>
<p>Because I got a little distracted I’ve wrote a <a href="https://twitter.com/robert0muehsig/status/222704828114149377">distress tweet</a>. One of the answers I received was the straight tip from <a href="https://twitter.com/d03n3rfr1tz3">Dirk.</a></p>
<p><img title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb734.png" width="449" height="276" /></p>
<p>Translation: </p>
<p><strong>Robert:</strong> localhost: 8080/Reporting doesn’t work and localhost 8080/Reporting/index doesn’t work either. If I rename the controller in foobar it works o.o</p>
<p><strong>Dirk:</strong> Eventually there is a folder or a virtual pad? </p>
<p><b>Solution:</b></p>  

<p>I had a “Reporting” folder on the Root-layer. ASP.NET deflected the request to this folder and after it didn’t found an index.html or default.html it answers with a 404. All I had to do was renaming the folder and it works. </p>
<p><b>“ContentController” or “ScriptsController” – the easiest way to rebuild it</b></p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image1574.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 10px 10px 0px; padding-left: 0px; padding-right: 0px; display: inline; float: left; border-top: 0px; border-right: 0px; padding-top: 0px" title="image1574" border="0" alt="image1574" align="left" src="{{BASE_PATH}}/assets/wp-images-en/image1574_thumb.png" width="221" height="215" /></a>A little demo project to show you the matter. If you request localhost/Content it is going to end into the folder and there is nothing. Only with Content/Index the MVC pipeline is activated and works properly. </p>
<p>I assume that the ASP.NET pipeline prefers “static” objects and the mainly routing starts afterwards. </p>
<p>Okay… Good to know!</p>
<p>The question is: Is it possible to switch this mechanism off or just unlock specific folders like Content, Scripts and everything else has to pass the routing? Let me know what you think about it. </p>
