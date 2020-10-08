---
title: google dfp和adsense 点击转化追踪
tags: adsense dfp
---

google dfp 点击追踪记录
<script src=\"https://cdn.jsdelivr.net/npm/jquery@3.3.1/dist/jquery.min.js\"></script><br>
<script type=\"text/javascript\"><br>
if (window!=top){   top.location.href =window.location.href;} <br>
 var isOverGoogleAd = false;<br>
    var ad = "div[id*='google_ads']";<br>
    $(document).ready(function()<br>
    {<br>
        $("div[id*='div-gpt-ad']").on('mouseover', function () {<br>
            if($(this).attr('id')){<br>
                isOverGoogleAd = true;	 <br>
            }<br>
        });<br>
        $("div[id*='div-gpt-ad']").on('mouseout', function () {<br>
            if($(this).attr('id')){<br>
                isOverGoogleAd = false;<br>
            }<br>
        });<br>
    });<br>
    $(window).blur(function(e){<br>
        if(isOverGoogleAd){<br>
          $.ajax({<br>
                type: "GET",<br>
                url: "https://domain.com",<br>
                xhrFields: {withCredentials: true},<br>
                crossDomain: true,<br>
                });<br>
        }<br>
    });<br>
<\/script><br>

google adsense 点击记录
<script type=\"text/javascript\"><br>
    var isOverGoogleAd = false;<br>
    var ad = /adsbygoogle/;<br>
    $(document).ready(function()<br>
    {<br>
        $('ins').on('mouseover', function () {<br>
            if(ad.test($(this).attr('class'))){<br>
                isOverGoogleAd = true;<br>
            }<br>
        });<br>
        $('ins').on('mouseout', function () {<br>
            if(ad.test($(this).attr('class'))){<br>
                isOverGoogleAd = false;<br>
            }<br>
        });<br>
    });<br>
    $(window).blur(function(e){<br>
        if(isOverGoogleAd){<br>
            $.ajax({<br>
                type: "GET",<br>
                url: "https://www.domain.com",<br>
                xhrFields: {withCredentials: true},<br>
                crossDomain: true,<br>
            });<br>
        }<br>
    });<br>
<\/script>

