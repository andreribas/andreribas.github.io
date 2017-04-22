---
layout: post
title:  "Trabajando con Jekyll y Docker"
date:   2016-09-09 16:47:24 +0300
categories: jekyll docker
lang: es
ref: working-with-jekyll-and-docker
---
Running an application inside a container is a great way of having fine control on what is installed on your system while being able to run the most up to date version of it. As that was the approach chosen to run this site during development it just make sense to be the first tutorial to be published here (and because I don't want to forget how to do it :wink:).


The main containerization platform nowadays (if not the only one) is the almighty [Docker][docker] and that's what we'll be using here. The main advantage of a container over a virtualization is being lighter, faster and coolest. :sunglasses:

The simplest way to start the built-in server is to run the following command:

```bash
$ docker run --rm --volume=$(pwd):/srv/jekyll -it -p 127.0.0.1:4000:4000 jekyll/jekyll
```

But a better way of doing that is to create a bash function called jekyll, so you can use it as a regular app on your machine. To do so add the following lines to your `~/.bashrc` file:

```bash
jekyll() {
    docker run --rm --volume=$(pwd):/srv/jekyll -it -p 127.0.0.1:4000:4000 jekyll/jekyll jekyll $@
}
```

Now things get as easy as running the following into your jekyll project directory:

```bash
$ jekyll s
```

The only issue you might have and I haven't figured out a solution yet is if you're serving the page locally and try to run another jekyll command at the same time. The problem with that is that the first command is assigned to the local port 4000 and when the second call is made to the app it fails trying to assign the same port.

[docker]: https://www.docker.com/
