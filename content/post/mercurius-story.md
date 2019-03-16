+++
date = "2016-11-16"
title = "The story behind the Mercurius framework"
tags = ["golang"]
+++

In August of this year, I went to a Go metup here in Brazil more specifically in São Paulo to talk a bit about my experiences with GopherJS (a compiler from Go to JavaScript). 
When it was over, Jeff Prestes came to me and ask for help to migrate his statup applications to Go.
At that moment I was very happy because although I was studying Go a little over a year and a half ago, I had never worked professionally with the language, and then said that i could help.
We had some more conversations and in September I started working on [Novatrix](https://www.novatrix.com.br) four hours a day.

My first project at Novatrix was to build a dashboard that showed data about the [Máquina Taxi](http://www.maquinataxi.com) application, one of the Novatrix's products, when i had already introduced Jeff to a functional prototype of the Máquina Taxi Admin, he asked me to extract anything other than business logic of the application, to another Github repository to serve as a starter for the next applications to be developed. From this the Mercurius framework was born.

The Máquina Taxi Admin was an application built on top of [Macaron framework](https://go-macaron.com) with some add-ons like i18n, cache, jade template engine support, session, oauth2 server, jwt, pprof, gzip and sqlx for database communication.
Some of these add-ons are already available in Macaron's plug-in catalog and others are created by us, But regardless of who created what, everything would have to be available on Mercurius and ready for use.

In order for this application skeleton to be ready for use we had to fill in some gaps as a database configuration and the keys of the authentication tokens that changed with each application.

The simplest solution we found was to create a CLI that asks some questions for us and generates the application based on our answers.

Mercurius is an open source framework that gives you speed to create new 'Go' applications. It let you more focused on your business than in your backend. The code is available [here](https://github.com/novatrixtech/mercurius).

I take the end of this post to give a special thanks to Jeff Prestes, who gave me the opportunity to start working professionally with Go. Today besides working at Novatrix, I also work with [Nuveo](https://www.nuveo.ai/) with Go, but it was because of Jeff that I started with Go professionally. So here's my thank you Jeff!!

In next post i will write about The technical part of develop Mercurius CLI. I hope you have enjoyed it and until the next post.