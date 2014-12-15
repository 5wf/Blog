---
layout: post
title: "HowTo: Create SQL Table Relationships via Drag´n´Drop"
date: 2009-02-20 01:16
author: robert.muehsig
comments: true
categories: [HowTo]
tags: [HowTo, Relationships, SQL, Tips]
language: en
---
{% include JB/setup %}
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb310.png"><img style="border-right: 0px; border-top: 0px; margin: 0px 10px 0px 0px; border-left: 0px; border-bottom: 0px" height="89" alt="image_thumb3" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb3-thumb1.png" width="134" align="left" border="0" /></a>If you create a relationship between to SQL tables, you get many benefits. The most important benefit (for me) is the <a href="http://en.wikipedia.org/wiki/Data_integrity">integrity of your data</a>. Besides the database-world there is another huge benefit: The relationships are used by many <a href="http://en.wikipedia.org/wiki/Object-relational_mapping">O/R mappers</a> to create a structured object model. You could create such realtionships via different dialogs in the SQL Management Studio / Visual Studio or just do a &quot;Drag&#180;n&#180;Drop&quot; from one table to another one.</p> 
<!--more-->
  <p><strong>Relationships &amp; O/R Mappers</strong>&#160; <br /><a href="http://msdn.microsoft.com/de-de/library/bb386976.aspx">Linq2Sql</a> &amp; <a href="http://msdn.microsoft.com/en-us/library/aa697427(VS.80).aspx">ADO.NET Entity Framework</a> are both O/R mappers built in the .NET Framework (but you could use NHibernate or others as well)&#160; and create entities based on a database. If you have relationships in your database, you will find these relationships later in you object model. To create such realationships in you SQL Database you have 2 (or 3) options:</p>
<p><strong>Option A: With dialogs</strong></p>
<p>Select table -&gt; column -&gt; modify:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb410.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="178" alt="image_thumb4" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb4-thumb2.png" width="316" border="0" /></a> </p>
<p>*right click* -&gt; Relationships...</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb55.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="184" alt="image_thumb5" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb5-thumb1.png" width="309" border="0" /></a> </p>
<p>Add -&gt; Tables and Column Specification:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb72.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="141" alt="image_thumb7" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb7-thumb1.png" width="333" border="0" /></a> </p>
<p>Select table/column:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb93.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="185" alt="image_thumb9" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb9-thumb2.png" width="366" border="0" /></a> </p>
<p>Tada: Relationship created - but you need some clicks to do it. Now option B:</p>
<p><strong>Option B: With an database diagram </strong></p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb101.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="124" alt="image_thumb10" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb10-thumb.png" width="286" border="0" /></a> </p>
<p>2 tables and the red line marks the relationship we wants to add:</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb132.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="117" alt="image_thumb13" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb13-thumb1.png" width="322" border="0" /></a> </p>
<p>... just click on the primary key and drag it on the foreign key::</p>
<p><a href="{{BASE_PATH}}/assets/wp-images-en/image-thumb161.png"><img style="border-right: 0px; border-top: 0px; border-left: 0px; border-bottom: 0px" height="117" alt="image_thumb16" src="{{BASE_PATH}}/assets/wp-images-en/image-thumb16-thumb.png" width="352" border="0" /></a> </p>
<p>Now you&#180;ll see a dialog to specify the relationship. </p>
<p><strong>Result:      <br /></strong>Option B saves more time and is much more &quot;visual&quot; - option C would be: Write the SQL queries manual.</p>
