---
title: "A couple of nights struggling with php/mysql on a Jekyll website"
layout: post
date: 2020-01-19 10:24
image: /assets/images/posts/jekyll-logo-light-solid.png
tag:
- jekyll
- php
- svg
categories:
- Project
author: flelain
description: lessons learnt while adding a subscription offer to the blog
---

Ok, let's be straight from the start: it's been a while since I set up my last LAMP stack (Linux/Apache/Mysql/Php). I humbly admit that I had to brush up on my basics for the two latters. Still... one can find quite easily some pre-formatted php code to populate a simple mysql database through an HTML form! Because, fundamentally, I didn't need much more than this to offer a kind of subscription service on this blog. In fact, I spent most of my time coping with the integration of a php script -that is to say something a bit "dynamic"- within <a href="https://jekyllrb.com/">Jekyll</a>, a website generator, tailored for... static content. But, that was not the only issue I had to face... :)

## Jekyll and php scripts: what I learnt
I won't get into every technical detail of my various attempts. I will rather point out the lessons I learnt:

- Jekyll parses and processes in a specific manner markdown and html files, relying on their extensions - respectively .md and .html. Thus, don't expect your php files to be treated the exact same way. Which concretely implies that:
  1. you can't use markdown language in your php scripts: Jekyll won't render it - and your browser won't deal with it neither
  2. any of the other Jekyll items like variables, filters or tags can't be used.

-  your php files, as part of your site contents, still benefit from the Jekyll layouts you defined. That means that you can still apply the same **look & feel** to the pages issued from your .php (header, footer, ...). Just keep using the standard front matter expected by Jekyll:
{% highlight raw %}
---
layout: page
title: Subscribe
---
{% endhighlight %}

- if you use a project-wide permalink like
{% highlight raw %}
permalink: /:title/
{% endhighlight %}
to alias your pages, it won't work for any files which are not html or markdown. For instance, you'll have to point to your *script.php* page with its full name (and not an alias like *script*)

## Mysql admin
Installing a mysql server is straightforward on Linux, everything is made so easy through package management - thanks to the opensource community. Then connecting to it as root is as easy when you are root on the OS too. You put everything you need in place (1 database and 1 table with 4 fields in my case; DB admins, please don't make fun of me!) and... eventually, when it comes to the connection to your database from your PHP script, you give what you thought your mysql credentials were and... it fails! And once again, it took me some time to understand what was happening there. In fact, by default, on Linux - at least with my combination Ubuntu/mysql v14, mysql links your DB root account to your root/sudo system account. Very handy when on your server, you still have to create a new DB admin or alter the config of your root mysql account to grant access to the database through the php script.

I found <a href="https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost/:">here, on Stackoverflow,</a> the tips which helped me to get through this issue.

## SVG image format
Besides, while adding my subscription icon, I had the occasion to get introduced to *SVG* format, which stands for *Scalable Vector Graphic* (<a href="https://en.wikipedia.org/wiki/Scalable_Vector_Graphics">Wikipedia</a> for more info). This is a very useful format to render nice images, whatever the size you want it to be displayed and whatever the browser you use.

---
To wrap it up: when I step back, it finally does not look as terrible as I thought :) Maybe it was really only a matter of diving again into a web developer mindset and go get back some old memories!..
Now, with a living database containing subscribers and their email, my first obvious next step will be to automate email notifications as soon as a new post is published... some sleepless nights ahead?!.. :)

Thanks for reading!

---

*Pourquoi ai-je écrit ce billet en anglais ? Simplement parce que je pense qu'il s'adresse tout aussi bien à l'audience habituelle de ce blog qu'à n'importe quel autre contact, ami ou collègue anglophone que je pourrais avoir au Canada (ou n'importe où ailleurs) et que mes pérégrinations techniques pourraient intéresser. Et je considère que vous maîtrisez plutôt bien l'anglais si vous êtes arrivés jusque-là ! (enfin, l'anglais tel qu'écrit par un Français quoi...)*

*Why did I write this post in English? Simply because I think it's aimed at this blog regular French audience as well as any other English-speaking contact, friend, colleague, ... that I might have here in Canada (or wherever actually) and interested in my technical adventures. And I assume you master English pretty well if you've made it up to here! (well, the sort of English a French writes...)*
