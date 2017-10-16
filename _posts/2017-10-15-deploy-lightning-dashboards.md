---
layout: post
title: Deploy Lightning Dashboards
---

## Problem
You've created a shiny new Lightning Dashboard and you want to deploy it. You tried adding what you thought was the folderName/DeveloperName to the Dashboard section of your package.xml but your retrieval is not working. 

## Solution

In Winter 18 Lightning Dashboards have a non-obvious *DeveloperName*. Once you have this and the folderName you're good to go. There are two different ways to retrieve these values.

#### Option 1 - SOQL
You can retrieve the Dasbhoard DeveloperName in SOQL. 

{% highlight SQL linenos%}

  [SELECT ID, Title, DeveloperName FROM Dashboard]

{% endhighlight %}

Then you can also retrieve the folder's developername through SOQL.

{% highlight SQL linenos%}

  [SELECT ID, Name, DeveloperName FROM Folder]

{% endhighlight %}


#### Option 2 - REST API
Note that the Metadata API does not return info on Lightning Dashboards as of winter18. They are accessible through the REST API. Workbench is one way to explore the REST API. The DeveloperName for the dashboard can be accessed at `/services/data/v41.0/analytics/dashboards/{Id of dashboard}/describe` 

i.e. [Get Dashboard Results](https://developer.salesforce.com/docs/atlas.en-us.api_analytics.meta/api_analytics/analytics_api_dashboard_get_results.htm#)




Your folder name will look familiar. Your Lightning Dashoboard will not. You'll have to put both of them together in your package.xml.

{% highlight xml linenos%}

  -----
  <types>
    <members>My_Dashboards/WRQDotewHIuojpuybuYTOjWnFQanUg</members>
    <name>Dashboard</name>
  </types>

  -----

{% endhighlight %}
