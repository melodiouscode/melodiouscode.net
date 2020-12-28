---
layout: post
title: Creating a sitemap.xml file with Jekyll
date: '2020-12-28 19:50:00'
image: /images/posts/PXL_20201228_201101439-min.jpg
tags:
- jekyll
- liquid
- sitemap
---

As the previous post on this site explained, I have switched this site to a static site generator. The site generator I chose is called [Jekyll](https://jekyllrb.com/) that can be extended using various add-ons; it also includes a powerful template generator called liquid.

The latest challenge I came across in this migration is creating a sitemap.xml file to allow search engines to discover all the pages on my site. There is a plugin, called Jekyll Sitemap, that can generate a sitemap; however, it doesn't give me the customisation level required. My solution to creating a sitemap.xml file using Jekyll is to embrace the liquid templating system to make it for me!
<!--more-->
Jekyll uses the [Liquid](https://shopify.github.io/liquid/) engine which will parse any textual file that begins with what it calls ["front matter"](https://jekyllrb.com/docs/front-matter/), regardless of the files extension. The first step in creating our sitemap.xml file is creating an empty file named sitemap.xml and adding a front-matter.

<!--kg-card-begin: markdown-->
    ---
    layout: null
    ---

<!--kg-card-end: markdown-->

Jekyll will now start to generate a sitemap.xml file; the next step is to add content to the file. A sitemap requires a specific XML schema; a base node of "urlset" containing a list of "url" nodes for each page, the following is an example.

<!--kg-card-begin: markdown-->

    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
        <url>
            <loc>https://www.melodiouscode.net</loc>
            <lastmod>2020-12-28T19:20:06+00:00</lastmod>
            <changefreq>monthly</changefreq>
            <priority>0.5</priority>
        </url>
    </urlset>

<!--kg-card-end: markdown-->

By iterating through the pages and collections within a Jekyll site, it becomes easy to generate the sitemap.xml file programmatically. The following code snippet is an example of the Liquid syntax required to create our file; it includes some conditional logic to exclude pages. You can find a full copy of the sitemap generator in the sites [code-examples repository](https://github.com/melodiouscode/melodiouscode-snippets/blob/main/creating-a-sitemap-xml-file-with-jekyll/sitemap.xml).

<!--kg-card-begin: markdown-->
    {% raw %}
    {% for collection in site.collections %}
     {% for post in collection.docs %}
      {% unless post.published == false or post.sitemap.exclude == "yes" or page.name == "feed.xml"  %}
        <url>
            <loc>{{ site.liveUrl }}{{ post.url }}</loc>
            {% if post.sitemap.lastmod %}
                <lastmod>{{ post.sitemap.lastmod | date: "%Y-%m-%d" }}</lastmod>
            {% elsif post.date %}
                <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
            {% else %}
                <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
            {% endif %}
            {% if post.sitemap.changefreq %}
                <changefreq>{{ post.sitemap.changefreq }}</changefreq>
            {% else %}
                <changefreq>monthly</changefreq>
            {% endif %}
            {% if post.sitemap.priority %}
                <priority>{{ post.sitemap.priority }}</priority>
            {% else %}
                <priority>0.5</priority>
            {% endif %}
        </url>
      {% endunless %}
     {% endfor %}
    {% endfor %}
    {% endraw %}
<!--kg-card-end: markdown-->

The generator iterates through the pages enumerable followed by the collections list to generate a list of all the Jekyll site's final pages. The filtering uses Jekyll front-matter to allow for exclusions by using a front-matter property called sitemap to store the values used in sitemap generation. The front-matter properties that are not set in a page or posts front-matter are replaced with defaults or alternative values. It is important to remember the exclusion property in the front-matter of the sitemap.xml file; otherwise, your sitemap will reference your sitemap!

This post's header image is a map that hangs on my dining room wall; it is a nautical map of parts of Europe and the Mediterranean. I acquired it on a cruise ship several years ago; it's signed by the captain to honour my wife and I's engagement.

### Download the sitemap generator [here](https://github.com/melodiouscode/melodiouscode-snippets/blob/main/creating-a-sitemap-xml-file-with-jekyll/sitemap.xml).
