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
img_path: "{{site.post_img_path}}{{page.path}}/"
---
##### Preface
In this post I will describe how you can get working blog at your domain in 5 minutes.

##### Create GitHub account
Firstly go to [GitHub.com](https://github.com) and create an account in case if you do not have one. Nothing unusual: username, email, password, confirm and you are done.
![GitHub Sign Up]({{site.img_for_posts}}{{page.path}}/github_signup.png)

##### Setup Blog

If we wish to use GitHub as a hosting solution for our blog we have to use [GitHub Pages](https://pages.github.com/). In short it is a system that allows you to host your content at GitHub. It is not like regular hosting solutions but at the end you will receive the same result: website working on your domain. The only limits are ability to host only static files and no possibility to restrict access to your files. Anyway it fits perfectly in my vision of simple blogging.

To simplify blogging GitHub decided to support Jekyll. Jekyll is a templating system for static sites. With it you will not need to write HTML for each page from from scratch. I am not specialist in Jekyll so I decided to reuse existing theme available for free on the Internet. You can google them but me was not successful in it. I just did not like results Google gave for me. My choice was to go to GitHub and search Jekyll themes over there. Just try to search repositories by "Jekyll theme" and sort results by stars. I ended with [Hyde theme](https://github.com/poole/hyde) from @mdo.

After you have found suitable theme on GitHub just fork theme into repository with name "**USERNAME**.github.io":
![Fork Repository]({{site.img_for_posts}}{{page.path}}/fork.png)

You are almost done! Now you should be able to access your site at **USERNAME**.github.io. You should see some example content that author of theme wrote for you. Posts of your blog will should be saved at **_posts** directory. Go to this directory and you should find example content. You can delete it and begin to write your own ;) Just give proper names for your files in **_posts** folder. [date]-[dashed-title].md. The syntax of posts is [Markdown](https://en.wikipedia.org/wiki/Markdown).

##### Use your domain

To use your domain with blog working on GitHub Pages you will need to set CNAME record of it at your Name Server. Also you need to edit CNAME file in the root of your blog repository. Type your custom domain name in it and nothing else.
set cname file to your domain
go to claudflare, add domain, set cname record to USERNAME.github.io
set claudflare nameservers for your domain.
go to claud flare set ssl to flexible. set minifying for scripts, html, css

##### Canonical Name of your Blog
add cname to config.yml


##### Develop with Docker
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 4000:4000 jekyll/jekyll:pages jekyll s

stop - start if edit config.yml.

##### In Conclusion

<ul>
{% for tag in page.tags %}
    <li><a href="/tags/#{{ tag | uri_escape }}">{{ tag }}</a></li>
{% endfor %}
</ul>
