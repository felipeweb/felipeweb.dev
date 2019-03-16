+++
date = "2016-04-08"
title = "Writing Go on front-end with GopherJS"
tags = ["Golang", "JavaScript", "Front-end"] 
+++

It is increasingly common backend languages have a compiler for javaScript, enabling us to use the same code in the backend and in the browser.

Clojure, Scala and kotlin already support to compile your code for JavaScript, in Go it's completely possible too.

In this post we will see how to do it.

##### 1) We need to download the `GopherJS` to our `GOPATH`
```bash
go get -u github.com/gopherjs/gopherjs
```

##### 2) We need to write our Go code that we want to compile for JavaScript
```Go
package main

import (
	"github.com/gopherjs/gopherjs/js"
	"fmt"
)

func main() {
	js.Global.Get("document").Call("write", "Say hello to GopherJS")
	fmt.Println("GopherJS")
}
```
In the first line of main function, we get the `document`JavaScript object and call your method `write` passing the string `Say hello to GopherJS` as argument. In the second line we are doing the same as `console.log("GopherJS")`

##### 3) We need compile our Go code for JavaScript
```bash
gopherjs build -o app.js
```
###### We compile and minify the `.js` file passing `-m` as argument
```bash
gopherjs build -m -o app.js
```

##### 4) We need to include the JavaScript file in our HTML file
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Intro GopherJS</title>
</head>
<body>
<script src="js/app.js"></script>
</body>
</html>
```

Now we finish it. We can startup our server and see it run on browser.

![](/img/intro-gopher-js.png)

This post project is on my [github](https://github.com/felipeweb/blog-posts/tree/master/intro-gopherJS) see you in next post