---
title: Zopim
contributors:
  - user:     fpleme
    name:     Fernão Paes Leme
    
  - user:     reed
    name:     Nick Reed
issues:
  - repo:     rails/turbolinks
    number:   131
---

# Zopim Live Chat Widget

> **[zopim.com/product](https://www.zopim.com/product)**

### Official Implementation

```html
<body>
  <script>
  window.$zopim || (function(d,s){
    var z = $zopim = function(c){
      z._.push(c)
    }, $ = z.s = d.createElement(s), e = d.getElementsByTagName(s)[0];
    z.set = function(o){
      z.set._.push(o)
    };
    z._= [];
    z.set._ = [];
    $.async = !0;
    $.setAttribute('charset','utf-8');
    $.src = '//cdn.zopim.com/?MY_APP_KEY';
    z.t = +new Date;
    $.type='text/javascript';
    e.parentNode.insertBefore($,e)
  })(document,'script');
  </script>
</body>
```

### Solution

Remove the supplied javascript and add the following to your application's javascript.

```javascript
function zopim_chat(){
  $('[__jx__id], embed#__zopnetworkswf').remove();
  window.$zopim = null;
  (function(d,s){
    var z = $zopim = function(c){
      z._.push(c)
    }, $ = z.s = d.createElement(s), e = d.body.getElementsByTagName(s)[0];
    z.set = function(o){
      z.set._.push(o)
    };
    z._ = [];
    z.set._ = [];
    $.async = !0;
    $.setAttribute('charset','utf-8');
    $.src = '//cdn.zopim.com/?MY_APP_KEY';
    z.t = +new Date;
    $.type = 'text/javascript';
    e.parentNode.insertBefore($,e)
  })(document,'script');
}

$(document).on("ready page:load", function() {
  zopim_chat();
});

```
