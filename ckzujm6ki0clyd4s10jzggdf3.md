## Full Stack development in 2022: trends, frameworks and languages.

# Self-update or be deprecated 

The tech industry is continuously evolving, changing, new tools are made every day and new frameworks are created or mass adopted. The point of this post is to glimpse at what's going on, check the current trends and where the industry is headed.

# Languages

If you ever want to know what language is the most popular a good and don't know where to look the best place might be [TIOBE](https://www.tiobe.com/tiobe-index/):

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645307897259/fLo7CthA7N.png)

Python currently being king but closely followed by C and Java. Let me give a quick explanation on why those languages are the most used.

## Python
One of the selling points of Python is just how easy the syntax is and how it almost reads as pseudocode.   

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645369062253/FmQ2Z4spx.png)
Python has libraries for all your needs and despite being criticized as slow it's widely used everywhere. 
Most projects related to data science or machine learning will rely on Python, not to mention it has three of the most popular web frameworks right now: [Django](https://github.com/django/django), [Flask](https://flask.palletsprojects.com/en/2.0.x/) and [FastAPI](https://github.com/tiangolo/fastapi).

It's the perfect language for beginners but at the same time it's widely adopted everywhere, if you don't know where to start learn Python but good looking trying to figure out the best environment:

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645309138574/RSIZCU2fr.png)

[There's always a relevant xkcd](https://xkcd.com/1987/)

## C
C isn't as trendy or flashy but it's everywhere and does everything. Operating systems, embedded programming, etc. Both [Git](https://github.com/git/git) and [Linux](https://github.com/torvalds/linux) are written mostly in C.

[If it's good enough for Linus then it's good enough for the rest of us.](https://youtu.be/CYvJPra7Ebk)

## Java
Java, owned by Oracle, is enterprise king. Google, Netflix, Amazon, etc use Java in one way or another. 

Most Apache projects are also written in Java - if you are curious to why, here's a [HN reply](https://news.ycombinator.com/item?id=9249913).

Learn Java, learn [Spring](https://spring.io/) and you will never be out of a job. Check out some of the articles and tutorials on this blog about Java and Spring if you don't know where to start. The first post is: How to [Make your first API.](https://bognov.tech/starting-with-spring-boot-how-to-make-a-restful-get-endpoint)

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645310628891/xzMYlXhcx.png)

## PHP
Before JavaScript there was PHP, after JavaScript there's still PHP.  
   
This language went through a lot of iterations over the years to improve the developer's experience. Nowadays it's mainly used as a backend language on the web. It has two of the biggest frameworks: [Laravel](https://laravel.com/) and [Symfony](https://symfony.com/).   

However PHP's main use comes from [WordPress](https://wordpress.org/). If you haven't heard or used WordPress, you should have a look. We don't know the exact statistics but everyone keeps saying that it powers over 33% of the web. Why? [It's fast to set up](https://bognov.tech/how-to-install-wordpress-with-plesk-on-digitalocean), design and have an e-commerce site ready or anything you'd want, there are millions of plugins and it's fairly easy to use for no-coders.   
The perfect CMS, you can have a site with a blog in less than a day and focus on SEO (marketing loves WordPress for how easy it makes positioning) or whatever the business needs.  

If you ever hear that PHP is dead or dying, well, just look at the amount of jobs there are.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645362528737/MlQDPHTMd.png)



# JavaScript

Not long ago [The State of JS 2021](https://2021.stateofjs.com/en-US/) was released. It doesn't take a very large pool of votes but it's widely known in the dev community and worth looking into. It's probably one of the most important surveys to consider if you have anything to do with JavaScript. Most tools/frameworks work with TypeScript as well, if you were in doubt.

## Front-end Frameworks
The big three are there as always there: React, Angular and Vue:

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645311426706/vdvs8XBiH.png)

Last year [Svelte](https://svelte.dev/) made a lot of noise and it's slowly being adopted, the docs have improved a lot and after trying it for a bit I consider myself a fan as well for its ease of use.  
However it's not the only new kid on the block, I've seen a lot of praise for both [SolidJS](https://www.solidjs.com/) and [AlpineJS](https://alpinejs.dev/). 

## Back-end Frameworks
The results aren't going to surprise anyone, if you are a backend developer you have to know Express:

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645312134123/k86FJF5iT.png)

Although the amount of new tools we got this past year has been impressive:

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645312199337/kQDD-GuEw.png)

From what I've seen I believe [Remix](https://remix.run/) is the one receiving the most hype right now but [Astro](https://astro.build/) and [SvelteKit](https://kit.svelte.dev/) could be here to stay.

## Testing? Do people actually..?

Yes, TDD is a thing.  
Jest or Mocha at the top. The usual.   

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645312648863/yA9u52HDI.png)

## Bloated apps for mobile and desktop
Don't freak out if you open your Discord desktop app and you can inspect its source code as if it was an ordinary website. Everything is JavaScript now, well, TypeScript actually.

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645312730862/U51evV8OY.png)

[Electron](https://www.electronjs.org/) and [React Native](https://reactnative.dev/) shouldn't surprise anyone, with Cordova and Ionic following close.

It will be fun to see how [Tauri](https://tauri.studio/) can compete or find its market considering [Flutter is here](https://medium.com/flutter/announcing-flutter-for-windows-6979d0d01fed).

## Build Tools

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645313030393/1Yo0-7WvK.png)

Nothing out of the ordinary, however I expect [Vite](https://vitejs.dev/) to be widely adopted by next year.

## Libraries
Here we have Axios, Lodash, Moment, Redux, etc. Nothing out of the ordinary.

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645313272660/YXKqt0u-N.png)

Out of the list you should know [Redux](https://redux.js.org/) and [Tailwindcss](https://tailwindcss.com/).

# Google shenanigans
Google has been hard at work this last couple of years when it comes to their tools, and I'm not talking about [Kubernetes](https://github.com/kubernetes/kubernetes) here or the awful state of the search engine.

## Go
![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645313643322/N8lyVFfJd.png)
If you are a backend developer you probably have noticed the increased adoption of the [Go language](https://go.dev/). Considering that K8s is written in Go and the amount of companies that have started to use it I'd keep an eye on the language and its ecosystem.

## Flutter
![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645314161818/3QTd2GxYX.png)
Google has decided Facebook (Meta) is too cool with their React Native and [who doesn't want to get rid of Electron](https://medium.com/flutter/announcing-flutter-for-windows-6979d0d01fed)? Enter [Flutter](https://flutter.dev/). 
They might be getting a bit too ambitious here but working with Flutter and Dart is a breeze. 

I've directed a multi-platform project this past year using Flutter + Firebase. It's fairly easy to setup and make an MVP, I recommend it highly for a fast paced project where the client doesn't want a pixel-perfect design, perfect for startups. 

For anything else? Well, as always, **it depends**. 

![imagen.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645315192940/np9-fehbq.png)

# What else is out there?
Terraform, serverless architecture, Rust, micro frontends and everything involved in Web 3.0: blockchain, crypto, NFTs, all that jazz.

# C'est fini

[The cover art is from Joan Cornellà](https://joancornella.net/en/).  

If you think I'm wrong we can argue on Twitter: [hmu @tekbog](https://twitter.com/tekbog).  

Disclaimer: I haven't talked about C#, C++, Ruby, Swift, R, etc because they are out of my area of expertise.  
