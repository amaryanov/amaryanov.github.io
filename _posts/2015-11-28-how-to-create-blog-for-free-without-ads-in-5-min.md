---
layout: post
title: How to create blog for free without ads in 5 min
---

create account at GitHub
github supports Jekyll
you can google for Jekyll themes
search for Jekyll these at GitHub
fork theme into USERNAME.github.io repository
if you have a domain for blog:
set cname file to your domain
go to claudflare, add domain, set cname record to USERNAME.github.io
set claudflare nameservers for your domain.
go to claud flare set ssl to flexible. set minifying for scripts, html, css
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

develop locally:
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 4000:4000 jekyll/jekyll:pages jekyll s

stop - start if edit config.yml.
