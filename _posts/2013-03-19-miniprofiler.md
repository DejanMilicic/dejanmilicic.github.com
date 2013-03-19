---
layout: post
category : lessons
tagline: ""
tags : [asp.net, profiler, tutorial]
---
{% include JB/setup %}

Here is short reminder how to set up [Miniprofiler](http://miniprofiler.com/) on your ASP.NET website

## Overview 

### What is Miniprofiler?

### How to install?

Easiest way is to install via Nuget Manager

  ```
  PM> Install-Package MiniProfiler
  ```

### How to set up tracking of your site

In Global.asax.cs add following lines

  ```
  protected void Application_BeginRequest(object sender, EventArgs e)
  {
    if (Request.IsLocal)
    {
      MiniProfiler.Start();
    } 
  }
  ```

  ```
  protected void Application_EndRequest(object sender, EventArgs e)
  {
    MiniProfiler.Stop();
  }  
  ```
  
These will start and stop Miniprofiler for each request made on you website.

Now for the reporting support - add following to your pages

  ```
  <head>
    <%= MiniProfiler.RenderIncludes() %>
  </head>
  ```

And that is basically it, you now have profiling set up

### Track performance of your code

For every piece of code you would like to measure execution time, wrap it up in following

  ```
  using (MiniProfiler.Current.Step("Description of the code executed"))
  {
    // your code here
  }
  ```