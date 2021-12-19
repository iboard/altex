%{ 
  title: "Javascript, 23 Years A Nightmare",
  author: "Andi",
  tags: ["2018", "andi", "dev", "javascript"]
}
---
Yesterday I found this on twitter.
![23 years of Javascript](/assets/posts/2018/23yrsJavascript.jpg)
> 04 Dec, 1995. Published in The Sentinel of Carlisle, Pennsylvania.

I wonder how it can happen that, in 23 years, nobody fixed at least the 
stupidest errors of that crock.

Sure, I'm not a Javascript expert –and I never will be– but from a language, 
almost every developer is coerced to use, I expect I can use it a little bit more 
intuitively.

Today I almost went crazy while trying to find out where the bug in this 
little snippet of code hides.

My httml: 

{% highlight html %}
<div class="listing-entry">....</div>
{% endhighlight %}

My Javascript:

{% highlight javascript %}
function findAncestor (el, cls) {
  var className = el.className;
  console.log( "At the top?", className, cls );
  if( className == cls ) {
    console.log("Top element clicked");
    return el; // it's me
  } else {
    while ((el = el.parentElement) && !el.classList.contains(cls));
    return el;
  }
}
{% endhighlight %}

With this code, the console never showed me "Top element clicked" but prints
```At the top? listing-entry listing-entry```

"Aaaarrrrrrrgh, I hate this nonsense!" was my first thought. And obviously
`className` can't be the same as `cls`.

I replaced 

{% highlight javascript %}
  console.log( "At the top?", className, cls );
{% endhighlight %}

with 

{% highlight javascript %}
  console.log( "At the top?", "'"+className +"', '"+cls+"'" );
{% endhighlight %}

and, sure enought I found out that the strings doesn't match because 
`el.className` actually was `listing-entry<blank>`.

So, my final code looks like

{% highlight javascript %}
function findAncestor (el, cls) {
  var className = el.className.trim();
  console.log( "At the top?", className, cls );
  if( className == cls ) {
    console.log("Top element clicked");
    return el; // it's me
  } else {
    while ((el = el.parentElement) && !el.classList.contains(cls));
    return el;
  }
}
{% endhighlight %}


You might think, "ya, but where is the problem, wasn't it easy to fix?".
Yes, it was easy to fix. Anyway, *Why, Javascript, why? Why you torture me so much?*


<iframe width="560" height="315" src="https://www.youtube.com/embed/dzc5vW9Ze44" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

