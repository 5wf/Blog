---
layout: post
title: "HowTo: Introduction in to MetaWebLog API"
date: 2010-09-15 20:01
author: CI Team
comments: true
categories: [HowTo]
tags: []
language: en
---
{% include JB/setup %}
<img title="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb199.png" border="0" alt="image" width="132" height="130" align="left" />

This Blogspot is based on Scott Hanselmans "WeeklySourceCode", where MetaWebLog API was the subject of today. In the Blogspot he relates that MS use the Windows Live Writer also to administrate their own websites. The tool is absolutely practical and it works with MetaWebLog API.




With this tool it´s possible to create "CMS" Content with standard tools like for example Word or the Windows Live Writer.

<strong>Why should I use this?</strong>

The ordinary end user is used to have a basic WYSIWYG editor. There are some nice Editors like for example tinyMCE. But the main problem I recognized while using such web-based solutions, is the often adventurously offered possibilities of handling pictures.

The ordinary user likes to move pictures into word by copy and paste and to angle some effects there. If you are a website operator and you would like to give your clients an easy to handle Frontend, than you have to implement MetaWebLog API.

<strong>Standard Tools</strong>

The main advantage is given by the nice clients. There is for example the Windows Live Writer:

<img title="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb200.png" border="0" alt="image" width="244" height="212" />

But also Word from the version of 2007:

<img title="image" src="{{BASE_PATH}}/assets/wp-images-de/image_thumb201.png" border="0" alt="image" width="360" height="241" />

<strong>Technical background:</strong>

The MetaWebLog API isn´t based on SOAP but on XML Remote Process Call (RPC). In fact it is just another transmission of XML. An Example from Wikipedia:

<pre class="c#">
&lt;?xml version="1.0"?&gt;
&lt;methodCall&gt;
  &lt;methodName&gt;examples.getStateName&lt;/methodName&gt;
  &lt;params&gt;
    &lt;param&gt;
        &lt;value&gt;&lt;i4&gt;40&lt;/i4&gt;&lt;/value&gt;
    &lt;/param&gt;
  &lt;/params&gt;
&lt;/methodCall&gt;
</pre>

The MetaWebLog API has a fixed set of methods. But therefore <a href="http://nayyeri.net/" target="_blank">Keyvan Nayyeri</a> already created a interface for ASP.NET in 2008.

<pre class="c#">
namespace NotABlog
{
    public interface IMetaWeblog
    {
        #region MetaWeblog API

        [XmlRpcMethod("metaWeblog.newPost")]
        string AddPost(string blogid, string username, string password, Post post, bool publish);

        [XmlRpcMethod("metaWeblog.editPost")]
        bool UpdatePost(string postid, string username, string password, Post post, bool publish);

        [XmlRpcMethod("metaWeblog.getPost")]
        Post GetPost(string postid, string username, string password);

        [XmlRpcMethod("metaWeblog.getCategories")]
        CategoryInfo[] GetCategories(string blogid, string username, string password);

        [XmlRpcMethod("metaWeblog.getRecentPosts")]
        Post[] GetRecentPosts(string blogid, string username, string password, int numberOfPosts);

        [XmlRpcMethod("metaWeblog.newMediaObject")]
        MediaObjectInfo NewMediaObject(string blogid, string username, string password, MediaObject mediaObject);

        #endregion

        #region Blogger API

        [XmlRpcMethod("blogger.deletePost")]
        [return: XmlRpcReturnValue(Description = "Returns true.")]
        bool DeletePost(string key, string postid, string username, string password, bool publish);

        [XmlRpcMethod("blogger.getUsersBlogs")]
        BlogInfo[] GetUsersBlogs(string key, string username, string password);

        [XmlRpcMethod("blogger.getUserInfo")]
        UserInfo GetUserInfo(string key, string username, string password);

        #endregion
    }
}

</pre>

This interface was implemented by Scott Hanselman into his demo project:

<pre class="c#">
string IMetaWeblog.AddPost(string blogid, string username, string password,
    Post post, bool publish)
{
    if (ValidateUser(username, password))
    {
        string id = string.Empty;
        string postFileName;
        if (String.IsNullOrEmpty(post.title))
            postFileName = Guid.NewGuid() + ".html";
        else
            postFileName = post.title + ".html";

        File.WriteAllText(Path.Combine(LocalPublishPath, postFileName), post.description);

        return postFileName;
    }
    throw new XmlRpcFaultException(0, "User is not valid!");
}
</pre>

I was asking my self what happened to the pictures: they are formed into "NewMediaObject" and it´s possible to convert them as byte array.

<strong>Demo projects by Scott Hanselman </strong>

As I said before, this "HowTo" is based on a <a href="http://www.hanselman.com/blog/TheWeeklySourceCode55NotABlogALocalXMLRPCMetaWebLogEndpointThatLiesToWindowsLiveWriter.aspx" target="_blank">Post of Scott</a>. He also released his demo project and I already tried to send files from Windows Live Writer or Word and it works with the described methods.
