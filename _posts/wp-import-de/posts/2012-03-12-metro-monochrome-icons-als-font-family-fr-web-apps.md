---
layout: post
title: "Metro / Monochrome Icons als Font-Family für Web-Apps"
date: 2012-03-12 01:16
author: Robert Muehsig
comments: true
categories: [Allgemein]
tags: [Icon, Icons, Metro]
language: de
---
{% include JB/setup %}
<p><a href="{{BASE_PATH}}/2011/11/25/kostenlose-icons-im-metro-lookmonochromminimalist-icons/">Metro-Icons</a> werden in allen Arten von User-Interfaces (egal ob Web, Desktop oder Phone-App) immer beliebter. Da diese Icons einfarbig sind, kann man einen cleveren Trick nutzen um diese Icons skalierbar und flexibel in seinem Projekt zu nutzen.</p> <p><strong>Metro Icons in WinJS Applikationen</strong></p> <p>Ausschlaggebend für diesen Blogpost war dieser Post “<a href="http://www.jonathanantoine.com/2012/03/05/winjs-out-of-the-box-available-icons/">Metro apps – a lot of icons are available out of the box</a>”. Microsoft war recht clever und hat die eingebauten Metro-Icons als Schriftart “Segoe UI Symbol” bereitgestellt.</p> <p><strong>Icons als Schriftart, warum?</strong></p> <p>Um seine Icon-Welt skalierbar (d.h. für verschiedene Auflösungen), in verschiedenen Größen und in verschieden Spielarten (Farben etc.) vorrätig zu haben müsste man sich schon größere Gedanken machen. Es bietet sich doch aber an, ein bereits gut funktionierendes System zu nutzen – daher die Wahl auf die Schriftarten. Schriftarten können skalieren und verschiedene Farben annehmen und noch mehr…</p> <p><strong>Font-Awesome – für Twitter Bootstrap, aber auch für alle anderen WebApps</strong></p> <p><a href="http://fortawesome.github.com/Font-Awesome/">Font-Awesome</a> hat die <a href="{{BASE_PATH}}/2012/02/02/twitter-bootstrap-2-0-released-release-prsentation/">Twitter Bootstrap</a> Icons als Schriftart hinterlegt und sollte in allen gängigen Browsern funktionieren. </p> <p><strong>Vorteile</strong></p> <p>- Skalierbarkeit! Vectorgrafiken halt…</p> <p>- Alles was ich mit CSS und Schriftarten machen kann, kann ich auch mit den Icons machen!</p> <p>- Asset-Management wird dadurch erheblich vereinfach</p> <p>- …</p> <p>Die Idee find ich ziemlich clever – jedenfalls hatte ich dies bislang bei Web-Applikationen so noch nicht gesehen, auch wenn es schon ewig “Symbol-Schriftarten” gibt (MS Symbol… ;) ).</p>
