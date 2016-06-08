---
layout: post
title: "[Octopress] Add Google AdSense to Octopress "
comments: true
category: experience

---

## Apply for Google AdSense

My first request of AdSense is rejected because of "__Site does not comply with Google policies__". I do not know the exact reason, but I did the following things to get it through: 

1. I registered a top-level .COM domain name to replace the original github page's domain.

2. I added "Privacy Policy" page, and added the link to the bottom of each blog post. 

3. I re-wrote the "About Me" page, and added in administrator email address. 

4. I updated a few more posts, making it more than 580 posts in total. 

5. I set up Google Webmaster Tools, and updated sitemap.xml in the configurations. 

6. I resubmitted my request of AdSense again. 

## Put AdSense in your blog

1. Create a new file: source/_includes/asides/advertise.html

2. Copy and paste the code from AdSense, eg. 

        <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
        <!-- ad-name -->
        <ins class="adsbygoogle"
             ...............
        <script>
        (adsbygoogle = window.adsbygoogle || []).push({});
        </script>

3. Go to _config.yml, and look for "default_asides", then add "asides/advertise.html, " in the beginning of the array

    default_asides: [asides/advertise.html, asides/category_list.html, asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]

4. Now you've added advertisement in your side menu.

5. Go to source/_layouts/post.html and look for: 

    \<h1\>Comments\</h1\>
    
6. Below the h1 tag, add your AdSense code, again. 

7. Now you've added advertisement above your comment area.

Thanks for the effort from [this reference](https://www.hi29.net/post/2013/11/30/octopresszen-mo-fang-adsense/).

## Updates

Apr 9th update: my re-submission of Google AdSense is not approached, because of "not enough content". I don't know what else to do, so I switched to another ad platform. 

Apr 11th update: For the first time ever, my blog has more than 1,000 visit per day. 

{% img middle /assets/images/google-analytics-20150411.png %}
