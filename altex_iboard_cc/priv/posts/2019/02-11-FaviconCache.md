%{
  title: "favicon.ico and the cache",
  date: "Mon Feb 11 20:33:59 CET 2019",
  tags: ["andi", "2019", "simplicity"],
  author: "Andi"
}
---
## You've changed the favicon.ico for your website but browsers still show the old version?

### Here is a solution:

In your HTML-code find and replace

```html
<html>
  <head>
  ...
   <link rel="icon" 
         href="/favicon.ico" 
         type="image/x-icon"/>
  ...
  </head>
  ...
</html>
```

with

```html
<html>
  <head>
  ...
   <link rel="icon" 
         href="/favicon.ico?v=201902112029" <---- put a timestamp here
         type="image/x-icon"/>
  </head>                              
  ...
</html>
```


and change the timestamp, every time you publish a new favicon.ico-file.

This is still the simplest way to force browsers to reload the icon.
Using some kind of a web-framework, automating this step in a template
should be easy. Some pseudo code looks like this

```html
<html>
  <head>
  ...
   <link rel="icon" 
         href="/favicon.ico?v=<%= buildtime_parameter() %> 
         type="image/x-icon"
   />
  ...                                  
  </head>                             
  ...
</html>
```

_Happy coding!_


