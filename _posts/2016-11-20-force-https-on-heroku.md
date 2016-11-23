---
layout: post
title: Force HTTPS on Heroku
---

## Problem
If you have a Java application running on Heroku you may want to force secure https connections. In fact if your Heroku app is connected to a listing on the Salesforce AppExchange you may not accept regular http requests. The way heroku routes your requst makes it impossible to tell the origin using most conventional patterns in web frameworks.

## Solution

Heroku does send a `x-forwarded-proto` header that can be used to determine if the origin is http or https.

Here is an example in Java that utilizes [Spark's Before Filter](http://sparkjava.com/documentation.html#filters) to intercept the header and then drop any non https requests.


{% highlight java linenos%}

  public static void main(String[] args)
{
    // Before-filters are evaluated before each request, and can read the 
    // request and read/modify the response.
    before((request, response) -> {
        //force to https                          
        if(!"https".equalsIgnoreCase(request.headers("x-forwarded-proto"))){
            // if the x-forwared-proto header does not equal https throw exception
            throw new UnsupportedOperationException("only http alllowd");
        }
    });
}

{% endhighlight %}
