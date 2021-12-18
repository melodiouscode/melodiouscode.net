---
layout: post
title: Why I hate Path.Combine
date: '2018-04-14 07:03:36'
image: /images/posts/mike-enerio-87677-unsplash-min.jpg
tags:
- development
- dotnet
- c-sharp
---

As most .NET developers will know there is a Path.Combine() method in System.IO which can be used to (you guessed it) combine two file paths. Unfortunately, it sucks; it sucks bad.

<figure class="kg-card kg-image-card"><img src="/images/content/examples-min.png" class="kg-image" alt="some examples of Path.Combine use"></figure>

As you can see it functions just as you would expect in the first three lines; but it sucks on the last three. Why would Microsoft not implement a path separator check; adding or removing the separator where applicable? A very good question in my opinion; so I have my own implementation.

<!--kg-card-begin: markdown-->

    using System;
    using System.IO;
    using System.Linq;
    
    public static class Pathy {
    	public static string Combine(string path1, params string[] paths) {
    		return paths.Aggregate(path1, Combine);
    	}
    	
    	private static string Combine(string path, string path2) {
    		char spliter = Path.DirectorySeparatorChar;
    		
    		if (path == null) {
    			throw new ArgumentException("Base path can not be null", nameof(path));
    		}
    		
    		if (path2 == null) {
    			throw new ArgumentException("Sub path can not be null", nameof(path2));
    		}
    		
    		path = path.Trim().TrimEnd(spliter);
    		path += spliter;
    		path += path2.Trim().TrimStart(spliter);
    		
    		return path;
    	}
    }

<!--kg-card-end: markdown-->

Pathy.Combine() takes two or more paths in the same way that Path.Combine() does and correctly merges them based on the default Path.DirecotrySeperatorChar as used by the current environment.

Feel free to use and abuse this bit of code; it is provided with no warranty or guarantees. You can also find it on &nbsp;[GitHub](https://github.com/melodiouscode/pathy/blob/master/pathy.cs).

The header image used on this page was provided for free by [Mike Enerio](https://unsplash.com/@mikeenerio) via [unsplash.com](https://unsplash.com/@mikeenerio) thanks Mike!

