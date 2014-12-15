---
layout: post
title: "HowTo: jQuery hosted CDN version & local „Fallback“"
date: 2011-02-06 09:58
author: CI Team
comments: true
categories: [HowTo]
tags: [CDN, Fallback, jQuery]
language: en
---
{% include JB/setup %}

  
  <p><a href="{{BASE_PATH}}/assets/wp-images-en/image120.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 10px 0px 0px; padding-left: 0px; padding-right: 0px; display: inline; float: left; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" align="left" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb29.png" width="182" height="74" /></a><a href="http://docs.jquery.com/Downloading_jQuery">jQuery</a> is one of the populates javascript frameworks. But it´s not the smallest one. To save traffic and reduce the waiting time while loading you should try out the "CDN" (hosted) jQuery version. But how is it possible to run a local backup plan in emergency case? Go on reading if you are interested in the answer...</p>  
  <!--more-->  <p><b>JQuery CDN</b></p>  <p>jQuery it self´s, Google and Microsoft are offering jQuery (+ some well-known Plugins) for linking on their servers. More about this you can read <a href="http://docs.jquery.com/Downloading_jQuery#CDN_Hosted_jQuery">here</a>.</p>  <p><b>Why should I do this?</b></p>  
  <p>There are several reasons for using the hosted version:</p>  <p>Â· You save the traffic. jQuery and co. are able to take a lot of space on the traffic.</p>  <p>Â· Google and co. <a href="http://en.wikipedia.org/wiki/Content_delivery_network">CDNs</a> are created to do this job. If someone is able to offer such content very fast than networks like this.</p>  <p>Â· For a long time browsers are not able to load more than two Javascript files from one domain. If you use jQuery from google.com your Browser will be able to load other application specific files at the same time. If this is important today is the question <img style="border-bottom-style: none; border-right-style: none; border-top-style: none; border-left-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Zwinkerndes Smiley" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-winkingsmile11.png" /></p>  <p>Â· Many people use Google or Microsoft services or visit websites which are linked by their jQuery Version. That means, you have the big chance, that your browser already cached jQuery somewhere - shorter waiting times while loading!</p>  <p>Â· More information´s you will find on the <a href="http://developer.yahoo.com/performance/rules.html">Yahoo best practices site</a>.</p>  <p><b>Which CDN is the best for me? Microsoft or Google? </b></p>  
  <p>At least both services are almost equal if we talk about the jQuery hosting. But probably there are more people using Google CDN - that means you have bigger chances if you use Google. On the other hand Microsoft included some gadgetry for ASP.NET developer with the Script Manager - but actually we don´t need it <img style="border-bottom-style: none; border-right-style: none; border-top-style: none; border-left-style: none" class="wlEmoticon wlEmoticon-smilewithtongueout" alt="Smiley mit herausgestreckter Zunge" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-smilewithtongueout.png" /></p>  <p>Here is a little discussion on Stackoverflow: <a href="http://stackoverflow.com/questions/1447184/microsoft-cdn-for-jquery-or-google-cdn">Microsoft CDN for JQuery or Google CDN?</a></p>  <p><b>Why shouldn´t we use it? </b></p>  
  <p>Of course there are also some disadvantages. You can´t use it for intern applications (but you don´t need it there) and also you need to trust the provider - anyway there is a kind of dependency. </p>  <p><b>What happens if there are any kinds of problems on Google/Microsoft/jQuery CDN?</b></p>  
  <p>Hm... In my opinion you shouldn´t be scared that one of the CDNs will go down but maybe there could be a problem reaching the CDN. Because of this I recommend you to create your own Backup and link it in emergency cases:</p>  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:082465c2-6699-46ca-a086-1095a41e23fd" class="wlWriterEditableSmartContent"><pre name="code" class="c#">&lt;script src="//code.jquery.com/jquery-1.4.4.min.js"&gt;&lt;/script&gt;
&lt;script&gt;!window.jQuery &amp;&amp; document.write(unescape('%3Cscript src="LOKALER_JQUERY_PFAD"%3E%3C/script%3E'))&lt;/script&gt;</pre></div>

<p>Instead of "LOKALER_JQUERY_PFAD" you easily enter your own pad. In line one CDN jQuery is linked by jQuery. Little hint: If we talk about a HTTP side <a href="http://code.jquery">http://code.jquery</a>.... Will be used. But HTTPS sides are called https:// ... . That´s because of this "//" Syntax. </p>

<p><b>If code.jQuery.com is down anyway </b></p>

<p>With Java Script the local version will be linked in this case automatically. </p>
