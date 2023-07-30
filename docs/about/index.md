# Welcome to my Blog!


{{< music url="/audio/intuition.mp3" name=intuition artist=salemelise cover="/images/Blade_Runner_Black_Lotus_29_1.webp" autoplay="true">}}

> # Hello World!
<img src="/images/bladerunner.webp" >

> ## Thanks for these friends :heart_eyes: !
> 

<div class="flink" id="article-container">
<div class="friend-list-div" >

{{< friend name="SuperSASS" url="https://blog.supersassw.com/" logo="/images/supersass.jpg" word="My mentor" >}}

</div>
</div>

> ## Who Am I

I am particularly interested in Roman history,in which Caesar Augustus is my favorite character.I was born in September,so i named myself as 
Septemus.I'm just a college student and i use this site to keep my notes,that's all.

> ## How Old Is This Blog?
<script type=text/javascript>
    var now = new Date();
    function createtime() {
        var grt = new Date("01/11/2023 16:38:52");//此处修改你的建站时间或者网站上线时间
        now.setTime(now.getTime() + 250);
        var years = (now - grt) / 1000 / 60 / 60 / 24 / 365;
        var ynum = Math.floor(years);
        var days = (now - grt) / 1000 / 60 / 60 / 24;
        var dnum = Math.floor(days);
        var hours = (now - grt) / 1000 / 60 / 60 - (24 * dnum);
        var hnum = Math.floor(hours);
        if (String(hnum).length === 1) {
            hnum = "0" + hnum;
        }
        var minutes = (now - grt) / 1000 / 60 - (24 * 60 * dnum) - (60 * hnum);
        var mnum = Math.floor(minutes);
        if (String(mnum).length === 1) {
            mnum = "0" + mnum;
        }
        var seconds = (now - grt) / 1000 - (24 * 60 * 60 * dnum) - (60 * 60 * hnum) - (60 * mnum);
        var snum = Math.round(seconds);
        if (String(snum).length === 1) {
            snum = "0" + snum;
        }
        var elements = document.getElementsByClassName("timeDate");
        var i;
        for (i = 0; i < elements.length; i++) {
            /*因为建站时间还没有一年，就将之注释掉了。需要的可以取消*/
            elements[i].innerHTML =  "It has been " + ynum + " years " + (dnum - ynum * 365) + " days ";
        }
        elements = document.getElementsByClassName("times");
        for (i = 0; i < elements.length; i++) {
            /*因为建站时间还没有一年，就将之注释掉了。需要的可以取消*/
            elements[i].innerHTML = hnum + " hours " + mnum + " mins " + snum + " secs since my blog has been brought to this world!";
        }
    }

    setInterval("createtime()", 250);
</script>
:hugs:
<span class=liveTime>
    <span class=timeDate>Loading days...</span>
    <span class=times>Loading secs...</span>
</span>
<!-- It has been years months days hours mins secs since my blog has been brought to this world! -->

