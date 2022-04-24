---
title: Have I mentioned loving Extension Methods?
date: 2008-11-06T12:00:06+09:00
description: Coming in C# 3.0
draft: false
hideToc: false
enableToc: true
enableTocContent: true
tags:
- csharp
categories:
- dotnet
---

Here's my new favorite:

```java
public static string AppSetting(this string parameter)
{
   return System.Configuration.ConfigurationManager.AppSettings[parameter];
}
```

Now I can simply call

```"BaseUrl".AppSetting();```
 

Beautiful.
