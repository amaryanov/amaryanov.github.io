---
layout: post
title: How to create blog for free without ads in 5 min
published: true
tags:
  - blog
  - github
  - github pages
  - https
  - cloudflare
  - docker
category: tech
---

##### Preface
In this post I will describe how you can get working blog at your domain in 5 minutes.

##### Create GitHub account
Firstly go to [GitHub.com](https://github.com) and create an account in case if you do not have one. Nothing unusual: email, password, confirm and you are done.
![GitHub Sign Up]({{ site.baseurl }}public/img/a{{page.path}}/github_signup.png "GitHub Sign Up")

##### Setup Blog
github supports Jekyll
you can google for Jekyll themes
search for Jekyll these at GitHub
fork theme into USERNAME.github.io repository

##### Use your domain
set cname file to your domain
go to claudflare, add domain, set cname record to USERNAME.github.io
set claudflare nameservers for your domain.
go to claud flare set ssl to flexible. set minifying for scripts, html, css

##### Canonical Name of your Blog
add cname to config.yml
add js script to the head:
{% if jekyll.environment == "production" %}
   {% include check_host_proto.html %}
{% endif %}
check_host_proto.html:
<script type="text/javascript">
  var host = "{{ site.cname }}";
  if (window.location.host != host)
      window.location.host = host;
  else if (window.location.protocol != "https:")
      window.location.protocol = "https";
</script>

##### Develop with Docker
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 4000:4000 jekyll/jekyll:pages jekyll s

stop - start if edit config.yml.

##### In Conclusion

<ul>
{% for tag in page.tags %}
    <li><a href="/tags/#{{ tag | uri_escape }}">{{ tag }}</a></li>
{% endfor %}
</ul>
