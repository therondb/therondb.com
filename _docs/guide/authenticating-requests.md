---
class: docs guide authenticating
layout: doc
permalink: /docs/guide/authenticating-requests.html
title: Authenticating Requests
---

# Authenticating Requests

Most applications need to know the identity of a user. Knowing a user’s identity
allows an application to provide a customized experience and grant them
permissions to access their data. The process of proving a user’s identity is
called authentication.

## Requests Lifecycle

Theron sends requests to your server in the following cases:

- Each time you create a new database streaming subscription using [`watch()`](../api/Theron.html#watch),
  Theron sends a new request to your server, unless the SQL query isn't cached.

- Each time you subscribe to a channel using [`join()`](../api/Theron.html#join),
  Theron fetches a signature from your server unless your application in the development mode.

To append authentication data to those requests, Theron provides the
[`setAuth()`](../api/Theron.html#setAuth) method.

## Authenticating Requests

Let’s say you have [the JWT authentication mechanism](https://jwt.io) that
defines a compact and self-contained way for securely transmitting information
between parties.  In order to sign each Theron's request to your server, append
the appropriate headers:

{% highlight javascript linenos%}
theron.setAuth({
  headers: { 'Authorization': 'Bearer eyJhbGciOiJIUzI1NiJ9.VGhlcm9u.twb3AZHNU4t_7KSyJsyNCW6JlkznjFeec0yhXsMspsE' }
});
{% endhighlight %}

Or do it using params:

{% highlight javascript linenos %}
theron.setAuth({
  params: { accessToken: 'eyJhbGciOiJIUzI1NiJ9.VGhlcm9u.twb3AZHNU4t_7KSyJsyNCW6JlkznjFeec0yhXsMspsE' }
});
{% endhighlight %}

Now, each Theron's request to your server is signed, and we can move to [the security section](./securing-channels.html).
