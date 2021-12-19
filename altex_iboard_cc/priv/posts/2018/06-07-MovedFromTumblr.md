%{ 
  title: "I moved my blog from Tumblr to Jekyll",
  date: "Sat Jul  7 19:17:55 CEST 2018",
  tags: ["about", "jekyll", "blog", "2018"]
}
---

# Goodbye Tumblr?

Today I successfully imported my Tumblr-blog,
which is on air since 2011, into a local
Jekyll-page.

## May be

My blog will officially move to my E2C instance soon.


# Testing

Let's test some behaviour. Unfortunatelly, imported posts
doesn't support code-highlighting. Will new posts?

  {% highlight elixir %}
  defmodule TestHighlighter do
    def hello do
      IO.puts "Hello, World!"
    end
  end
  {% endhighlight %}

😎 it works! with 
`{% raw %}{% highlight elixir %} .. {% endhighlight %}{% endraw %}`
