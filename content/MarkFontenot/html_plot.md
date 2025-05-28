---
title: "Can You Embed .html Plots using Plotly?"
date: 2025-05-28
draft: false
description: "Magic Time"
slug: "plotly"   # if you use, needs to be different for every post
tags: ["authors", "config", "docs"]
authors:
  - "mark_fontenot"
showAuthorsBadges : false
---

## Testing .html image embedding

We are attempting to embed a Plotly graph in a Hugo Blog Post. The first attempt was to use an `include_relative` shortcode.  

`{% include_relative birth_death_eu2.html %}`

However, that did not prove fruitful.  After more research, we discovered that we needed to create use an `iframe` shortcode because the Plotly graph was contained in a fully HTML document. 

First we need to create a new *short code* to handle the iframe.  
1. At the root of the blog directory, create a `layouts` folder, and inside of it, create a `shortcodes` folder. You can use `mkdir -p layouts/shortcodes` from the root of the blog repo to achieve this.  
2. Inside `layouts/shortcodes`, create a file named `iframe.html` and put the code that follows inside: 
```html
<iframe
  src="{{ .Site.BaseURL }}{{ .Get "src" }}"
  width="{{ .Get "width" | default "100%" }}"
  height="{{ .Get "height" | default "400" }}"
  frameborder="0"
  allowfullscreen
  loading="lazy">
</iframe>
```
3. Put the html file that contains the Plotly graph in the `static` folder. 
4. Embed the file inside the markdown of the blog post with the following

```{{</* iframe src="birth_death_EU2.html" width="100%" height="600" */>}}```

### Here is the example:

Here is an interactive graph:

{{< iframe src="birth_death_EU2.html" width="100%" height="600" >}}

