---
title: Adding Comments to a Wintersmith Blog
author: me
date: 2013-12-17 15:00
template: article.jade
comments: true
---

Adding user comments to a default Wintersmith blog is super simple using disqus and jade templates.

<span class="more"></span>

First register with [disqus.com](http://disqus.com) and add your wintersmith blog.  This will give you a unique disqus id for your blog.

Then create a jade mixin for disqus' javascript snippet.  You can copy and paste my code here, just remember to change `your-disqus-forum-id` to your unique disqus forum id.

`templates/disqus.jade`
```jade
mixin disqus()
  div#disqus_thread

  script.
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'your-disqus-forum-id'; // required: replace example with your forum shortname

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();

  noscript.
    Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
```

Next include your newly created disqus jade snippet in your article template.  I have included my disqus comments between the navigation and the about block.  As you can see below, I am using a conditional block in order to easily enable and disable comments on a per-article basis.

`templates/article.jade`
```jade
block prepend footer
  include disqus

  div.nav
    a(href=contents.index.url) « Full Blog

  if page.metadata.comments
    mixin disqus()
```

Now you can enable comments for any blog articles by simply adding `comments: true` to an article's meta data.

`contents/articles/your-article/index.md`
```
---
title: Some Article
author: me
date: 2013-12-16 15:00
template: article.jade
comments: true
---
```