---
layout: post
title: "Two options to SEO for Octopress"
date: 2017-02-07 20:55
comments: true
keywords: SEO, Octopress
description: SEO for Octopress is very simple
---

>add META **keywords** and **description** is very important for SEO and aslo basic. 


### FIRST

>Add this code in source/_include/header.html

```
{ % capture description % } { % if page.description % } { {
page.description }  } { % elsif page.layout == "home" % } { {
site.description } } { %else% } { { content | raw_content  } } 
{ %endif% }{ % endcapture % } 
```

<!--More-->

### Option One:

>Add **keywords** and **description** in your article.

Every post has this:
```
---
layout: post
title: "Three options to SEO for Octopress"
date: 2017-02-07 20:55
comments: true
---
```
So you just do like following this, add **keywords** and **description**, and
octopress will auto-generate the META info in your HTML file.
```
---
layout: post
title: "Three options to SEO for Octopress"
date: 2017-02-07 20:55
comments: true
keywords: your, keywords, here
desctiption: your description here
---
```
### Option Two:

>Add **keywords** and **description** in your site config file.

open _config.yml, you will see this
```
url: http://snowleung.github.io
title: Software Dev
subtitle: Make World More Beautiful
author: Samuel Leung
simple_search: https://google.com/search
```
new line and add this:
```
description: About learning, programming and happy hacking!
keywords: learning, programing, developer, algorithm
```
octopress will generate META info at all HTML file if you not specify
**keywords** and **description**.
