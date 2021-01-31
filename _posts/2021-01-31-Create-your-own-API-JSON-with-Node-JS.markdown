---
layout: post
title: How to create your own API JSON with Node JS
description: # Add post description (optional)
img: api.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Blog, Node, JSON, NodeJS]
---

Hello everyone! 

Let me post a work what couldn't find on internet. I did it because wanted to web scrapping some products on internet that were out of stock, and just wanted to be notified once they will get it back. 

So simple I created a NodeJS, it is getting a JSON, created by web scrapping script in Bash

**NodeJS**
{% highlight javascript %}
var http 	= require('http');
var fs 		= require('fs');
var port 	= "1111" ;
const open = require('open');

http.createServer(function(request, response) {
    response.writeHead(200, {
        'Content-Type': 'text/json',
		'Access-Control-Allow-Origin': '*',
		'X-Powered-By':'nodejs'
    });
    fs.readFile('deals.json', function(err, content){
        response.write(content);
        response.end();
    });
}).listen(port);

console.log("Listening on port " + port );
open('http://localhost:'+ port);
{% endhighlight %}

**Bash**

This code is in-line because I did it for crontab =)

{% highlight shell %}
link=`curl -s https://www.shopdutyfree.es/comprar-apple/auriculares/beats/solo3-abiertos-negro-brillante-barato.html -L | grep -qo "0 Unidades"; echo $?`; if [ $link -eq 1 ]; then jo -p link="https://www.shopdutyfree.es/comprar-apple/auriculares/beats/solo3-abiertos-negro-brillante-barato.html" availability=true | jq '.' | cat >> deals.json; echo ',' >> deals.json; fi
{% endhighlight %}

Obviously, deals.json should be in the same folder of the Node script

Thank you so much, hope you like it and bring you new ideas!
