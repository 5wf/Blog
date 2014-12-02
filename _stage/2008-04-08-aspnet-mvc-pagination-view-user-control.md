---
layout: post
title: "ASP.NET MVC - Pagination View User Control"
date: 2008-04-08 22:00
author: codemin
comments: true
categories: [Uncategorized]
tags: [ASP.NET MVC, Paging, User Controls]
---
{% include JB/setup %}
<p>Each website, content management system, blog and so on need &quot;pagination&quot;. A never ending site with &quot;foo-entries&quot; is not very professional. Thats why i created for my ASP.NET MVC sample (a kigg / dotnetnuke similar page) a specific&quot;Pagination View User Control&quot;</p>  <p>In almost every &quot;List&quot; View I implemented my control:</p>  <p><a href="http://code-inside.de/blog-in/wp-content/uploads/image.png"><img style="border-top-width: 0px; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" height="119" alt="image" src="http://code-inside.de/blog-in/wp-content/uploads/image-thumb.png" width="353" border="0" /></a> </p>  <p><a href="http://code-inside.de/blog-in/wp-content/uploads/image1.png"><img style="border-top-width: 0px; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" height="340" alt="image" src="http://code-inside.de/blog-in/wp-content/uploads/image-thumb1.png" width="339" border="0" /></a> </p>  <p>The advantages of such an control: </p>  <p>- look and feel is on each page the same&#160; <br />- changes are very easy to implement</p>  <p>In my sampel I use <a href="http://woork.blogspot.com/2008/03/perfect-pagination-style-using-css.html">this</a> CSS design.</p>  <p><strong><u>Structure</u></strong></p>  <p><a href="http://code-inside.de/blog-in/wp-content/uploads/image2.png"><img style="border-top-width: 0px; border-left-width: 0px; border-bottom-width: 0px; border-right-width: 0px" height="79" alt="image" src="http://code-inside.de/blog-in/wp-content/uploads/image-thumb2.png" width="242" border="0" /></a>&#160; </p>  <p>A typical MVC View User Control</p>  <p><strong><u>Code</u></strong></p>  <p>Pagination.ascx</p>  <div class="wlWriterSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:ac53f895-2c91-4dd0-a0cf-4f84697589b4" style="padding-right: 0px; display: inline; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px"><pre name="code" class="c#">&lt;%@ Control Language="C#" AutoEventWireup="true" CodeBehind="Pagination.ascx.cs" Inherits="Mvc2.Views.Shared.Pagination" %&gt;
&lt;ul class="pagination-clean"&gt;
    &lt;% if (ViewData.HasPreviousPage)
        { %&gt;
          &lt;li class="previous"&gt;&lt;a href="&lt;%=ViewData.PageActionLink.Replace("%7Bpage%7D", (ViewData.PageIndex - 1).ToString())%&gt;"&gt;Â« Previous&lt;/a&gt;&lt;/li&gt;
     &lt;% }
       else
        { %&gt;
          &lt;li class="previous-off"&gt;Â« Previous&lt;/li&gt;
     &lt;% } %&gt;
                  
     &lt;%for (int page = 1; page &lt;= ViewData.TotalPages; page++)
        { 
        if (page == ViewData.PageIndex)
            { %&gt;
              &lt;li class="active"&gt;&lt;%=page.ToString()%&gt;&lt;/li&gt;
         &lt;% }
        else
            { %&gt;
              &lt;li&gt;&lt;a href="&lt;%=ViewData.PageActionLink.Replace("%7Bpage%7D", page.ToString())%&gt;"&gt;&lt;%=page.ToString()%&gt;&lt;/a&gt;&lt;/li&gt;
         &lt;% }
        } 
              
       if (ViewData.HasNextPage)
            { %&gt;
              &lt;li class="next"&gt;&lt;a href="&lt;%=ViewData.PageActionLink.Replace("%7Bpage%7D", (ViewData.PageIndex + 1).ToString())%&gt;"&gt;Next Â»&lt;/a&gt;&lt;/li&gt;
         &lt;% }
       else
            { %&gt;
               &lt;li class="next-off"&gt;Next Â»&lt;/li&gt;
         &lt;% } %&gt;
&lt;/ul&gt; </pre></div>

<p>Pagination.ascx.cs</p>

<div class="wlWriterSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:8b9e87b3-1e2f-449a-ac88-24470d161034" style="padding-right: 0px; display: inline; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px"><pre name="code" class="c#">using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace Mvc2.Views.Shared
{
    public class PaginationViewData
    {
        public int PageIndex { get; set; }
        public int TotalPages { get; set; }
        public int PageSize { get; set; }
        public int TotalCount { get; set; }
        public string PageActionLink { get; set; }
        public bool HasPreviousPage
        {
            get
            {
                return (PageIndex &gt; 1);
            }
        }

        public bool HasNextPage
        {
            get
            {
                return (PageIndex * PageSize) &lt;= TotalCount;
            }
        }
    }

    public partial class Pagination : System.Web.Mvc.ViewUserControl&lt;PaginationViewData&gt;
    {
        public Pagination()
        {

        }
    }
}
</pre></div>

<p>The ViewData is strongly typed by the PaginationViewData class.</p>

<p><strong><u>How to use - Helper &quot;PagedList&quot;</u></strong></p>

<p>It is very easy to use, if you are already use the PageList class:</p>

<div class="wlWriterSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:747bd65b-d4f4-419c-8b99-3398597fee78" style="padding-right: 0px; display: inline; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px"><pre name="code" class="c#">using System;
using System.Data;
using System.Configuration;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
using System.Xml.Linq;
using System.Collections.Generic;

namespace Mvc2.Helpers
{
    public class PagedList&lt;T&gt; : List&lt;T&gt;
    {
        public PagedList(IQueryable&lt;T&gt; source, int index, int pageSize)
        {
            this.TotalCount = source.Count();
            this.PageSize = pageSize;
            this.PageIndex = index;
            this.AddRange(source.Skip((index - 1) * pageSize).Take(pageSize).ToList());

            int pageResult = 0;
            for (int counter = 1; pageResult &lt; this.TotalCount; counter++)
            {
                pageResult = counter * this.PageSize;
                this.TotalPages = counter;
            }
        }

        public int TotalPages
        {
            get;
            set;
        }

        public int TotalCount
        {
            get;
            set;
        }

        public int PageIndex
        {
            get;
            set;
        }

        public int PageSize
        {
            get;
            set;
        }

        public bool HasPreviousPage
        {
            get
            {
                return (PageIndex &gt; 1);
            }
        }

        public bool HasNextPage
        {
            get
            {
                return (PageIndex * PageSize) &lt;= TotalCount;
            }
        }
    }

    public static class Pagination
    {
        public static PagedList&lt;T&gt; ToPagedList&lt;T&gt;(this IQueryable&lt;T&gt; source, int index, int pageSize)
        {
            return new PagedList&lt;T&gt;(source, index, pageSize);
        }

        public static PagedList&lt;T&gt; ToPagedList&lt;T&gt;(this IQueryable&lt;T&gt; source, int index)
        {
            return new PagedList&lt;T&gt;(source, index, 10);
        }
    }
}
</pre></div>

<p>The original code wrote <a href="http://blog.wekeroad.com/2007/12/10/aspnet-mvc-pagedlistt/">Rob Conery</a> - in my version is the first page the number 1, not 0 - a user could confused by the link to page number 0 ;)</p>

<p><strong><u>How to use- in the view page</u></strong></p>

<p>I render the control by using the in-build &quot;Html.RenderUserControl&quot; helper:</p>

<p></p>

<div class="wlWriterSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:e712fce1-e593-4adb-9427-c2264e6d7928" style="padding-right: 0px; display: inline; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px"><pre name="code" class="c#">    &lt;%=Html.RenderUserControl("~/Views/Shared/Pagination.ascx", new Mvc2.Views.Shared.PaginationViewData()
      {
          PageIndex = ViewData.EntryList.PageIndex,
          TotalPages = ViewData.EntryList.TotalPages,
          PageActionLink = Url.Action("List","Entry", new { category = ViewData.Category, page = "{page}"}),
          TotalCount = ViewData.EntryList.TotalCount,
          PageSize = ViewData.EntryList.PageSize
      }, null)%&gt;</pre></div>

<p></p>

<p>The properties of the control and of the PagedList are almost the same - only the &quot;<strong>PageActionLink</strong>&quot; is a specific property. The &quot;<strong>PageActionLink</strong>&quot; is the action Link to your controller - &quot;/Management/Tag/2&quot; route to your <strong>&quot;Management&quot;-Controller</strong> and <strong>&quot;Tag&quot;-ActionMethod</strong> with the <strong>page</strong> parameter. The &quot;page = {page}&quot; parameter is only a template for the real page number, which will be replaced in my control:</p>

<p></p>

<div class="wlWriterSmartContent" id="scid:812469c5-0cb0-4c63-8c15-c81123a09de7:33d6efe7-5ffc-4189-a145-73061fd7a7b6" style="padding-right: 0px; display: inline; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px"><pre name="code" class="c#">&lt;li&gt;&lt;a href="&lt;%=ViewData.PageActionLink.Replace("%7Bpage%7D", page.ToString())%&gt;"&gt;&lt;%=page.ToString()%&gt;&lt;/a&gt;&lt;/li&gt;</pre></div>

<p></p>

<p>The URL helper method encode the { and } to %7B and %7D. I can&#180;t explain it very well in english - one quick look in the source code (pagination.ascx) is very helpful ;)</p>

<p>Feel free to use it.</p>

<p><strong>PS: English blogging is hard :/ ;)</strong></p>
