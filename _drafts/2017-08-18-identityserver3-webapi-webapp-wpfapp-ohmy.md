---
layout: post
title: "IdentityServer3 with WindowsAuthentication with ASP.NET WebApi & ASP.NET & WPF App"
description: "In the recent month I was working on our identity system. The main problem was that we have larger range of application types. This blogpost demonstrate how to use a WindowsAuth IdentityProvider in ASP.NET MVC and WebApi and inside a WPF App in combination with IdentityServer3."
date: 2017-08-18 23:15
author: Robert Muehsig
tags: [OpenId Connect, JWT, IdentityServer3, OAuth]
language: en
---
{% include JB/setup %}

__Please note__: In my sample and in this blogpost I cover IdentityServer 3, because last year when I created working on the sample and our real implementation IdentityServer4, a rewrite and with .NET Core in mind was in beta. My guess is, that most stuff should still apply even if you are using IdentityServer4, but I didn't test it.

## Overview

The sample consists of the following projects:

__IdentityTest.IdServerHost:__ That's the central IdentityServer in our solution. It contains all "client" & "identityprovider" settings.
__IdentityTest.WinAuth:__ This is our Windows-Authentication provider. Because of the nature of WindowsAuth it needs to be an extra project. This needs to be hosted via IIS (or IIS Express) with Windows authentication enabled. The ASP.NET app acts as a bride and will convert the Windows-Auth ticket into a saml token. It is more or less like a mini-ADFS
__IdentityTest.WebApp:__ The WebApp itself can be used via browser and also hosts a WebApi. The WebApi is secured by the IdServerHost and one page will trigger the authentication against our IdServerHost.
__IdentityTest.WpfClient:__ With the WPFApp we want to get a AccessToken via a WebBrowser-Control from the IdServerHost and call the WebApi that is hosted and secured by the very same IdServerHost.

The IdentityServer team did a great job and have a large __[sample repository on GitHub](https://github.com/IdentityServer/IdentityServer3.Samples)__. 

I will talk about each part. Now lets beginn with...

### The IdServerHost

The IdentityServerHost is a plain ASP.NET application. To include the IdentityServer3 you need to add this [NuGet-Package](https://www.nuget.org/packages/IdentityServer3/).

The code is more or less identical with the [Minimal-Sample](https://github.com/IdentityServer/IdentityServer3.Samples/tree/master/source/WebHost%20(minimal)/WebHost), but I __disabled the SSL__ requirements for my demo.

Be aware: The IdentityServer use a certificate to sign the tokens, but this has nothing to do with the SSL certificate. This was a hard learning curve for me and IISExpress or something messed things up. In the end I disabled the SSL requirements for __for my development enviroment__ and could start to understand how each part is communicating with each other. 
The signing certificate in the sample is the sample .pfx file from the offical samples.

Remember: __DO USE SSL IN PRODUCTION.__ Oh - and use the Cert-Store for the signing certificate as well! 

Besides the SSL stuff the most important stuff might be the [client-registration](https://github.com/Code-Inside/Samples/blob/master/2016/IdentityTest/IdentityTest.IdServerHost/Configuration/Clients.cs) and the [identity-provider-registration](https://github.com/Code-Inside/Samples/blob/79fda88113a4736a465ab275fe0745dfc6aefa9a/2016/IdentityTest/IdentityTest.IdServerHost/Startup.cs#L45-L65).


