---
layout: post
title: "HowTo: use ASP.NET developments in VMWare & iPhone Simulator on a Mac"
date: 2011-03-20 23:33
author: CI Team
comments: true
categories: [HowTo]
tags: [ASP.NET, iPhone, Mac, VMWare]
language: en
---
{% include JB/setup %}

  <p><a href="{{BASE_PATH}}/assets/wp-images-en/image143.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 10px 0px 0px; padding-left: 0px; padding-right: 0px; display: inline; float: left; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" align="left" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb51.png" width="96" height="185" /></a>Those of you who are lucky owners of a Mac are able to register at the <a href="http://developer.apple.com/">apple developer program</a> for free and download several iPhone developer tools there. Also you can download a simulator for iPhone/iPad which probably works like a real iPhone/iPad. As ASP.NET developer I run Visual Studio in a VM. In my case VMWare Fusion. But how it´s possible to run my web application which is hosted in VM in the host system? <b></b></p>  
  <p>The Source Code is the same like the standard MVC Project type. </p>  <!--more-->  <p><b>Windows configuration </b></p>
<p>Before you start you have to turn off the windows firewall.</p>
<p><b>VMWare configuration </b></p>
<p>The last step is to set the VMWare networkconfiguration to "Bridged":</p>
<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb142.png" width="438" height="286" /></p>
<p>More about the subject Host System and network you will find here.</p>
<p><b>IPConfig/renew</b></p>
<p>After finishing it´s useful to get a new IP address from DHCP (nearly every router use DHCP by default). This is possible by the commando line order "ipconfig/renew". </p>
<p>Now read the new IP Address with Windows and after this you are able to enter this on you Mac in every browser:</p>
<p>Doesn´t matter if you use Chrome with MacOSX:</p>
<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb143.png" width="428" height="299" /></p>
<p>The iPhone Simulator:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image144.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb52.png" width="135" height="240" /></a></p>
<p>Or the iPad:</p>
<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb145.png" width="190" height="244" /></p>  
  <p><b>Debugging?</b></p>
<p>Possible! Breakpoints you define in VM will be put out if you, for example, enter the side with the iPad browser. </p>
<p><b>First Impression:</b></p>
<p>Generally this constellation works. If it´s always the best way to switch between VM and the simulator is the question. But of course it´s more comfortable than running a whole deployment. </p>
<p>If you don´t use VMWare Fusion can find the same settings in Parallels. I think both products are nearly the same anyway. <img style="border-bottom-style: none; border-right-style: none; border-top-style: none; border-left-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Zwinkerndes Smiley" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-winkingsmile16.png" /></p>
