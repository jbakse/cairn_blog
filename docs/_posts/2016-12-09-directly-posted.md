---
layout: post
title:  "Directly Posted"
date:   2016-12-09 13:12:54 -0500
categories: shaders
author: Justin Bakse
---

This is just some thing!

A simple paragraph with an ID attribute.
{: #para-one}

abc
{:ref-name: #myid .my-class}
xyz


<div class="aside" markdown="1">
Okay so this isn't true.

This **might** be true;
</div>

easy | peasy

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

A simple paragraph with an ID attribute.
{: #para-one}


Hello

> A blockquote with a title
{:title="The blockquote title"}
{: #myid}

{:.ruby}
    Some code here

    Some More


{::comment}
This text is completely ignored by kramdown - a comment in the text.
{:/comment}
