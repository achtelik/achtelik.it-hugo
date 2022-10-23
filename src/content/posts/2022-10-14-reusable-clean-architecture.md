---
title:  "Reusable Clean Architecture"
date: 2022-10-14
categories: software development
header_img: /img/2022-10-13.png
---

The following package structure is my personal preferred project structure.

Beside the fact to use a sustainable clean architecture, the main goal of the following example structure is: **To have
a project, which allows a team to reuse the technical setup.**
This is achievable by the separation into <span style="color:#9673A6;">modules</span> and <span style="color:#9673A6;">
basics</span>. Just replace the <span style="color:#9673A6;">modules</span> <span style="color:#6C8EBF;">topics</span>
with new <span style="color:#6C8EBF;">topics</span> and reuse the <span style="color:#9673A6;">
basics</span> <span style="color:#6C8EBF;">topics</span>.

*Names are just smoke and mirrors. Feel free to find your own naming!*

<div class="post-image">
  <a href="/img/2022-10-14.svg" target="_blank">
    <img src="/img/2022-10-14.svg"/>
  </a>
  <p>Source: Matthias Achtelik</p>
</div>
<!--more-->

<span style="color:#9673A6;">modules</span> & <span style="color:#9673A6;">basics</span>

* <span style="color:#9673A6;">modules</span> = Package for business use cases which are unique for each application.
* <span style="color:#9673A6;">basics</span> = Package for technical use cases which are reusable in each application.

<span style="color:#6C8EBF;">topics</span>

* <span style="color:#6C8EBF;">topics</span> = Packages to split up code into specific use cases. Topics can have
  multiple levels, see notifications, mails and pushes.
    * <span style="color:#6C8EBF;">business topics</span> = part of the modules package
    * <span style="color:#6C8EBF;">technical topics</span> = part of shares, because you can reuse it in the next
      application

<span style="color:#82B366;">commons</span>

* <span style="color:#82B366;">commons</span> is a package to centralize code, which is used by multiple topics. It can
  contains all types of layers.

<span style="color:#D79B00;">layers</span>

* <span style="color:#D79B00;">layers</span> are for the code separation into clear responsibilities.
    * <span style="color:#D79B00;">entrypoints</span> = These are the start points for your process inside the applications. We separate them by
      technologies.
        * <span style="color:#D6B656;">rest</span> = For REST-API endpoints.
        * <span style="color:#D6B656;">job</span> = For schedulers which are triggers processes by time.
    * <span style="color:#D6B656;">...</span> = Other technologies could be jms, soap, or other stuff.
    * <span style="color:#D79B00;">applications</span> = This layers links the entrypoints with the domains layers and the domains layer with itself. It
      allows to add additional framework features like dependency injection, transaction management and caching.
        * <span style="color:#D6B656;">configs</span> = Contains configuration and property classes or other framework specific stuff.
        * <span style="color:#D6B656;">services</span> = Includes classes to implement framework specific services and funcionalities.
    * <span style="color:#D79B00;">domains</span> = This contains your main business logic. Have to be independent from other layers and should be as much
      as possible framework agnostic.
        * <span style="color:#D6B656;">adapters</span> = Interfaces which have to be implemented by dataproviders.
        * <span style="color:#D6B656;">models</span> = Your business objects which represents your data.
        * <span style="color:#D6B656;">services</span> = The main part for your business logic.
    * <span style="color:#D79B00;">dataproviders</span> = This are the outgoing points for your process/application to call external systems. We separate
      them by technologies.
        * <span style="color:#D6B656;">db</span> = To store and load data from a database.
        * <span style="color:#D6B656;">rest</span> = To make external REST http calls to other systems.
        * <span style="color:#D6B656;">...</span> = Other technologies could be jms, file, or other stuff.

<span style="color:#666666;">tests</span>

* <span style="color:#666666;">tests</span> is a package which contains additional classes to simplify your tests. For example:
    * <span style="color:#666666;">testdata</span> = Builders and factories to create test data.
    * <span style="color:#666666;">base</span> = Classes which create the basic setup for your tests. For example to:
        * Setup a database and other test dependencies.
        * Create a web context.
        * ...
    * <span style="color:#666666;">archUnit</span> = I really like https://www.archunit.org/. It helps to test architecture decisions. It allows you to:
        * Check your package structure.
        * Check for dependencies cycles.
        * Check naming conventions.
