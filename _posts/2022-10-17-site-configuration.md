---
layout: post
title: "Site Configuration"
date: 2022-10-17 21:47:52 +0200
category: notes
tags: jekyll minima
---

Setting up the whole thing is not complicated.
GitHub [guides][gh-pages] are easy to follow and the default page comes up in minutes,
even when using a [custom domain][gh-pages-custom-domain].
Local development environment and theme customizations may take a little longer.

## Local environment

Following the official [installation guide][jekyll-install] should get the job done.
However, if you are an unlucky user of Apple silicon Mac running macOS 12.6 and have
Xcode version 14 installed, Ruby installation will fail for version 3.1.2.
A workaround for `ruby-install` users is to add the `--enable-shared` flag
([#430][ruby-install-430]):

{% highlight shell %}
% ruby-install 3.1.2 -- --enable-shared
{% endhighlight %}

The fix for the issue has been back-ported from Ruby 3.2.0-preview2 to Ruby 3.1
([#6440][ruby-6440]) and should be released as 3.1.3.

Also missing from the [official tutorial][jekyll-tutorial] is the need for the `webrick`
gem starting from Ruby 3, as explained by [Moncef Belyamani][jekyll-webrick]:

{% highlight shell %}
% bundle add webrick
{% endhighlight %}

## File locations

Static pages have been moved to `_pages` following the notes from
[Michael Rose][jekyll-pages].
Any markdown files left in the site root must be excluded:

{% highlight yaml %}
# _config.yaml
include:
  - _pages
exclude:
  - README.md
{% endhighlight %}

## Theme

Default [`jekyll/minima`][jekyll-minima] is one of the cleanest among popular themes on
GitHub.
Since theme's gem is long outdated, fetching a development version using `remote_theme`
is recommended.
To keep remote theme version under control, it is possible to pin down a
[specific tag or Git ref][jekyll-remote-theme]:

{% highlight yaml %}
# _config.yaml
remote_theme: jekyll/minima@41b97699af658128fa9983e5312ca5516641f335
{% endhighlight %}

Theme configuration includes a skin selection and social links:

{% highlight yaml %}
# _config.yaml
minima:
  skin: auto
  social_links:
    github: boxyrobot
{% endhighlight %}

## Customizations

Theme fonts are replaced with [Source Sans Pro][source-sans-pro] and
[Source Code Pro][source-code-pro], sizes and weights slightly adjusted:

{% highlight html %}
<!-- _includes/custom-head.html -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@400;600&family=Source+Code+Pro:wght@500&display=swap" rel="stylesheet">
{% endhighlight %}

{% highlight scss %}
// _sass/minima/custom-styles.scss
.site-title, h1 {
  font-weight: 600;
}
pre,
code {
  font-size: 0.875em;
  font-weight: 500;
}
{% endhighlight %}

{% highlight scss %}
// _sass/minima/custom-variables.scss
$base-font-family: "Source Sans Pro", $base-font-family;
$code-font-family: "Source Code Pro", $code-font-family;
$base-font-size: 18px;
{% endhighlight %}

Dates are stripped from the permalinks:

{% highlight yaml %}
# _config.yaml
permalink: /:categories/:title/
{% endhighlight %}

Read time is calculated using Liquid filters following the notes from
[David Capello][jekyll-read-time] and added via a site-specific `_layouts/post.html`.
Reading cadence is set using the `words_per_minute` site parameter:

{% highlight yaml %}
# _config.yaml
words_per_minute: 180
{% endhighlight %}

Clock-like glyph was found on [Graphemica][graphemica].

[gh-pages]: https://docs.github.com/en/pages
[gh-pages-custom-domain]: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
[graphemica]: https://graphemica.com/
[jekyll-install]: https://jekyllrb.com/docs/installation/macos/
[jekyll-minima]: https://github.com/jekyll/minima
[jekyll-pages]: https://mademistakes.com/articles/using-jekyll-2016/
[jekyll-remote-theme]: https://github.com/benbalter/jekyll-remote-theme#declaring-your-theme
[jekyll-read-time]: https://davidcapello.com/blog/tips/reading-time-in-jekyll/
[jekyll-tutorial]: https://jekyllrb.com/docs/step-by-step/01-setup/
[jekyll-webrick]: https://www.moncefbelyamani.com/how-to-install-jekyll-on-a-mac-the-easy-way/
[ruby-6440]: https://github.com/ruby/ruby/pull/6440
[ruby-install-430]: https://github.com/postmodern/ruby-install/issues/430
[source-code-pro]: http://fonts.google.com/specimen/Source+Code+Pro
[source-sans-pro]: http://fonts.google.com/specimen/Source+Sans+Pro
