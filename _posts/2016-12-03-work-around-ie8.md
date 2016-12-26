---
layout: post
title: "Work around CSS styling for IE8"
date: 2016-12-03 20:33:00 +0800
categories: front-end
---

# Work around CSS styling for IE8

Frontend technology is booming today. However it's not for IE8. 
As there is still some usages of IE8, frontend developers have to find work around before droping IE8 support.

Here are some work around I am using.

* Cannot support SVG

Use image files as fallback

* Background opacity with rgba

Add fallback which do not use opacity

* Media query

Use [respond.js](https://github.com/scottjehl/Respond) to support this

* Border-radius, box-shadow, border-image

Use [CSS3 Pie](http://css3pie.com/)


