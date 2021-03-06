---
layout: post
title: "HowTo: Setup of WebDeploy / MSDeploy"
date: 2011-04-03 11:42
author: CI Team
comments: true
categories: [HowTo]
tags: [MSDeploy, Web Deploy]
language: en
---
{% include JB/setup %}


<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 10px 0px 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" align="left" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb397.png" width="192" height="135" />A long time ago I´ve already spoken about MSDeploy. It was about how to integrate MSDeploy into your Building process. But I haven´t talked a lot about server configuration. That´s what I´m going to change today because sometimes MSDeploy or WebDeploy is used to be a little bit bitchy ;-)</p>
<p>So how to configurate MSDeploy/WebDeploy?</p>  

<p><b>Basics</b></p>
<p>I assume that you have IIS7 or better. Here it´s not difficult to install the Web Deployment Tool with the <a href="http://www.microsoft.com/web/downloads/platform.aspx">Web Platform installer</a> - it´s not integrated default (that means not at the moment).</p>
<p><b>Download</b>: <a href="http://www.iis.net/download/webdeploy">Web Deploy Download</a></p>
<p><b>Windows services</b></p>
<p>There are two important windows services you are used to have:</p>
<p>- Web Deployment Agent Services</p>
<p>- Web Management Services</p>
<p><img title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb398.png" width="441" height="68" /></p>
<p>You can also use CMD:</p>
<p>- Net start msdepsvc</p>
<p>- Net start wmsvc</p>  

<p><b>Configure IIS: Management services</b></p>  

<p>One of the most important points for the configuration you will find in the "Feature View" of the "Management Services":</p>
<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb399.png" width="244" height="136" /></p>
<p>Here we need to be sure that "Enable Remote Connection" is crossed:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image150.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb58.png" width="462" height="164" /></a></p>
<p>You need to stop the service to change the configurations but don´t forget to restart after you finished <img style="border-bottom-style: none; border-right-style: none; border-top-style: none; border-left-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Zwinkerndes Smiley" src="{{BASE_PATH}}/assets/wp-images-en/wlEmoticon-winkingsmile17.png" /></p>
<p><b>There is another configuration you need to change: Management Service Delegation</b></p>
<p><strong><a href="{{BASE_PATH}}/assets/wp-images-en/image151.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb59.png" width="240" height="198" /></a></strong></p>  

<p>Under "edit Feature Settings" you need to permit all administrators - that means: <b>mark the first Checkbox!</b></p>
<p><strong><a href="{{BASE_PATH}}/assets/wp-images-en/image152.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb60.png" width="502" height="245" /></a></strong></p>
<p><b>Activate the Firewall</b></p>  

<p>MSDeploy uses the TCP Port "8172" but you are able to change this at the "Management Service" point:</p>
<p><img style="background-image: none; border-bottom: 0px; border-left: 0px; padding-left: 0px; padding-right: 0px; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb403.png" width="385" height="218" /></p>
<p>Either you add the Port manual into the Fir</p>
<p>ewallsettings or you use this CMD call:</p>
<p>Netsh firewall add portopening TPC 8172 WdeployAgent</p>
<p><b>Create a website</b></p>
<p>As far as I know there must be a website already been integrated (look at "Sites") because Webdeploy doesn´t do this by itself - but maybe I´m wrong with that. In fact for me it just worked if I´m integrated the site before. </p>
<p>In my example the site is called "test" and I´ve changed the AppPool to .NET 4.0 (otherwise you are going to get an error message if the WebApp asks for it)</p>  

<p><b>Deploy!</b></p>  

<p><a href="{{BASE_PATH}}/assets/wp-images-en/image153.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 0px 10px 0px 0px; padding-left: 0px; padding-right: 0px; display: inline; float: left; border-top: 0px; border-right: 0px; padding-top: 0px" title="image" border="0" alt="image" align="left" src="{{BASE_PATH}}/assets/wp-images-en/image_thumb61.png" width="179" height="240" /></a>That´s what the Visual Studio Publish Screen could look like. At Service URL the IP address is enough!</p>
<p>At "Site/application" I´ve done some Tests with that it will be deployed directly on the web site. But it´s also possible to create some under folders or with a click on "Mark as IIS app" it´s going to create some Web Applications beneath the Web site (automatically). </p>  
  

<p><strong>For Web hoster</strong></p>
<p>If you plan to do this professional I recommend <a href="http://learn.iis.net/page.aspx/516/configure-the-web-deployment-handler/">this link</a> to you. This is about how to give specific users specific rights. </p>
<p><strong>Links</strong></p>
<p>AS I said before sometimes Web Deploy or MS Deploy is used to be a bit bitchy. More about his subject you will find on several sites in the web. </p>
<p>For me was the article of <a href="http://weblogs.asp.net/scottgu/archive/2010/09/13/automating-deployment-with-microsoft-web-deploy.aspx">ScottGu</a> and <a href="http://blogs.iis.net/kateroh/archive/2009/06/05/troubleshooting-common-msdeploy-issues.aspx">Troubleshooting</a> a big help.</p>
