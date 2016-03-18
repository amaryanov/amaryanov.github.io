---
layout: post
title: Blog for free without ads working via HTTPS
published: true
tags:
  - blog
  - github
  - github pages
  - https
  - cloudflare
  - docker
category: tech
description: In this post I will describe how you can get working blog at your domain in 5 minutes.
---

{% include img_path.inc %}

##### Preface
In this post I will describe how you can get working blog at your domain in 5 minutes.

##### Create GitHub account
Firstly go to [GitHub.com](https://github.com) and create an account in case if you do not have one. Nothing unusual: username, email, password, confirm and you are done.
![GitHub Sign Up]({{img_path}}/github_signup.png)
Now you are ready to setup your blog.

##### Setup Blog

Good news is that GitPages supports Jekyll templating system. As it stands from the description on their site: Jekyll is a simple, blog-aware, static site generator. With help of it we can create templates for different pages on the site. And for posts also. This means that after creating templates on time you will only add content of your posts and will not care about stuff like HTML, CSS, etc.
So we wish to use GitHub as a hosting solution for our blog.This means we have to use [GitHub Pages](https://pages.github.com/). In short it is a system that allows you to host your content at GitHub. It is not like regular hosting solutions but at the end you will receive the same result: website working on your domain. The only limits are ability to host only static files and no possibility to restrict access to your files. Anyway it fits perfectly in my vision of simple blogging.

I am not specialist in Jekyll so I decided to reuse existing theme available for free on the Internet. You can google them but I was not successful in it. I just did not like results Google gave for me. My choice was to go to GitHub and search Jekyll themes over there. Just try to search repositories by "Jekyll theme" and sort results by stars. I ended with [Hyde theme](https://github.com/poole/hyde) from @mdo.

After you have found suitable theme on GitHub just fork theme into repository with name "**USERNAME**.github.io":
![Fork Repository]({{img_path}}/fork.png)

You are almost done! Now you should be able to access your site at **USERNAME**.github.io. You should see some example content that author of theme wrote for you. Posts of your blog should be saved at **_posts** directory. Go to this directory and you should find example content in it. You can delete them and begin to write your own posts in this directory ;) Just give proper names for your files in **_posts** folder. [date]-[dashed-title].md. The syntax of posts is [Markdown](https://en.wikipedia.org/wiki/Markdown).
At the end I will give you some useful tips about structure of directories. But now just clone your new repository on your computer and make some small changes from the next paragraph if you wish to use your custom domain.

##### Use your domain

Here I will describe how you can use your domain for just created blog and how to make it accessible through HTTPS without buying a certificate.
Create file CNAME in the root folder of your blog. Put your domain name in it. Next go to your domain settings console and add CNAME record "**USERNAME**.github.io". Simple! **USERNAME**.github.io CNAME = your domain, your domain CNAME = **USERNAME**.github.io.
Now we wish to have our blog working through HTTPS. Easy to say and actually easy to do ;)
Go to [CloudFlare](https://www.cloudflare.com/). Sign up if you are not a CDN geek same as me and do not have an account on it. Add site (your domain). Once again go to your domain settings console and now change nameservers to CloudFlare's. Then come back to CloudFlare (CF) console and wait until it detects that you have changed NS records for your domain. Once it is done you can go to Crypto tab and set SSL setting to Flexible. Be aware, "flexible" means that traffic from browser to CF will be encrypted but from CF to GitPages will be Plain Text. But if you are the same as me just wish to see green lock icon in browser and make crawlers think of your blog with more respect then this solution is the best.


Also do not forget to add CNAME field in **_config.yml** in root of the blog folder. In the next paragraph I will give some tips about writing posts.

##### Writing posts

In case you wish to see your changes before you push your them at GitHub you can use Docker to have same environment that compiles your blog on GitPages servers. [Here](https://github.com/jekyll/docker) you can find all information regarding running Jekyll in Docker. For GitPages we need to use "pages" tag of Jekyll image:

docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 4000:4000 jekyll/jekyll:pages jekyll server

Run this command in the blog folder and you will have your blog running on 4000 port of your computer.

In case you make changes in **_config.yml** you need to stop and start Docker again.

After adding images to my posts I faced with problem that all my images are located in the same folder. Because I am pragmatic programmer I wish to have structure even in my blog images. My solution is that: I added "posts_img" field in **_config.yml** with value "/public/img/for" and created folder "for_posts" in /public/img/. In case if I wish to add image to new post firstly I create post then copy its file name and create folder with the same name in folder "/public/img/for_posts". In this new folder I put my image and in post text I refer to this image by such path: {{site.posts_img}}{{page.path}}/some.png. It is easy to read and it is easy to have structure in images folder in such way.

It is limited number of plugins Jekyll on GitPages supports. Main feature I expected to find was absent. It is generated pages for categories. The only compromise I found is it to have tags on each post and to have tags page which lists all tags and posts related to them. If you wish to have something same at your blog you can find my implementation at my [GitHub repository](https://github.com/anovmari/anovmari.github.io). Look at tags.md and at the beginning and end of this post's Markdown.

Wish to mention two iOS apps I have found useful for editing posts and uploading images to my blog:

 * [Octopage](https://itunes.apple.com/us/app/octopage-blogging-jekyll-markdown/id649843345?mt=8&uo=6&at=1000lHq&ct=) - GitPages editor. Nothing else. Just simple and clean design for typing text in posts.
 * [Working Copy](https://itunes.apple.com/us/app/working-copy/id896694807?mt=8&uo=6&at=1000lHq&ct=) - powerful Git client on iOS with Markdown editor. It is easy to upload (push) any files with it and edit your posts. If choose between Octopage and Working Copy I would choose Working Copy. It is much powerful.

If you paranoiac like me you will find useful these apps for images preprocessing:

 * [Exif Viewer](https://itunes.apple.com/us/app/exif-viewer-free-by-fluntro/id979066584?mt=8&uo=6&at=1000lHq&ct=) - useful to remove Exif data like your device info and your location info.
 * [Pixelgarde](https://itunes.apple.com/us/app/pixelgarde/id414677492?mt=8) - also for exif removal.
 * [Photo Rubber](https://itunes.apple.com/us/app/photo-rubber-photograph-shading/id891969768?mt=8) - shading off. Useful when you need to hide some one face on your photos ;)

##### In Conclusion

As a conclusion I wish to wish you to have many great posts! It is not only just typing texts but something that make us proud of the fact that we think we make this world little bit better ;)

##### Tags:
<ul>
{% for tag in page.tags %}
    <li><a href="/tags/#{{ tag | uri_escape }}">{{ tag }}</a></li>
{% endfor %}
</ul>
