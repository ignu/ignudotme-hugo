---
title: Low impact Ajax with jQuery and ASP.NET MVC
date: 2008-11-09T12:10:30.229Z
enableToc: false
enableTocContent: false
tags:
  - jquery
  - javascript
---

Here’s a simple way to avoid postbacks in your site, still be SEO friendly and degrade gracefully to JavaScript free browsers (and handle middle clicks and copy&paste) in ASP.NET MVC using jQuery.
First, we’ll create an alternate MasterPage called **No.master** with no content, only one **ContentPlaceHolder**:
<asp:ContentPlaceHolder ID=“MainContent” runat=“server” />
Now, we’re able to tell via HTTP Headers if a Request is an Ajax Request, so we’ll write a new method in our Controller Base class to toggle the master page:

```csharp
protected string GetMasterPageName()
{
     if (this.IsAjaxRequest())
         return “No”;

     return “Site”;
}
```

And now, whenever we return a View in our Controllers, we’ll use the overload that takes in the name of a View


```csharp
return View(“Edit”, GetMasterPageName(), postServices.GetByID(id))
```

So when a request comes in normally, we are returned full mark-up.  If the request is AJAX, we only return HTML for that view.
We won’t modify the url of our links, however we’ll give them all a class so we can grab then in jQuery.

```php
<a href=“/Post/Show/<%=post.ID %>” class=“ajaxLink”><%= post.Subject %></a>
```

Then we’ll wire a method called displayLink to all our ajaxLinks’ click event handlers:

```javascript
$(‘.ajaxLink’).click(displayLink);
```

And in that function we’ll make an AJAX call to the link’s target (its href attribute value) using the jQuery $.get method, update our main content area and return **false** in order to cancel the click event of the link:

```javascript
displayLink = function() {
    $.get($(this).attr(‘href’), function(response) {
        $(‘#mainContent')’html(response);
    });
    return false;
};
```
And that’s’it.  I would (and did) refactor the JavaScript and add a loading graphic, but I’m’just awestruck at how you can Ajaxify an application in ~12 lines of code.

