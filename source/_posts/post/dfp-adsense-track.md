---
title: google dfp和adsense 点击转化追踪
tags:#google adsense #google dfp
---

google dfp 点击追踪记录
<script src="https://cdn.jsdelivr.net/npm/jquery@3.3.1/dist/jquery.min.js"></script>
<script type="text/javascript">
if (window!=top){   top.location.href =window.location.href;} 
 var isOverGoogleAd = false;
    var ad = "div[id*='google_ads']";
    $(document).ready(function()
    {
        $("div[id*='div-gpt-ad']").on('mouseover', function () {
            if($(this).attr('id')){
                isOverGoogleAd = true;	 
            }
        });
        $("div[id*='div-gpt-ad']").on('mouseout', function () {
            if($(this).attr('id')){
                isOverGoogleAd = false;
            }
        });
    });
    $(window).blur(function(e){
        if(isOverGoogleAd){
          $.ajax({
                type: "GET",
                url: "https://domain.com",
                xhrFields: {withCredentials: true},
                crossDomain: true,
                });
        }
    });
</script>

google adsense 点击记录
<script src="https://cdn.jsdelivr.net/npm/jquery@3.3.1/dist/jquery.min.js"></script>
<script type="text/javascript">
    var isOverGoogleAd = false;
    var ad = /adsbygoogle/;
    $(document).ready(function()
    {
        $('ins').on('mouseover', function () {
            if(ad.test($(this).attr('class'))){
                isOverGoogleAd = true;
            }
        });
        $('ins').on('mouseout', function () {
            if(ad.test($(this).attr('class'))){
                isOverGoogleAd = false;
            }
        });
    });
    $(window).blur(function(e){
        if(isOverGoogleAd){
            $.ajax({
                type: "GET",
                url: "https://www.domain.com",
                xhrFields: {withCredentials: true},
                crossDomain: true,
            });
        }
    });
</script>



