# simple-webdev

Thanks to the magic of [Docker](http://docker.io/) and a lot of hard
work from system packagers of [Fedora](http://fedoraproject.org/) and
[CentOS](http://centos.org/), it's possible to have a *really simple* web
development container running **Apache**, *PHP**, and **SQLite**.

As the title of this Docker container warned you, it's intended to be
really simple. Don't expect any fancy SQL server like MySQL, Postgres,
MariaDB, or anything like that. Look elsewhere (or fork and modify).


## Usage

### Blah-blah-blah

So, what can you do with this 'simple-webdev' container? Well, for
starters, you can host anything that just requires Apache and PHP. If
there's a database needed, then use SQLite if available. Sure, this
means you can't get a vanilla WordPress installed, but you can
definitely get MediaWiki up and running with minimal effort. ownCloud
may even work too. Also, you can get static sites working or host your
own custom PHP. (But I guess that almost goes without saying, right?)

### A warning

While you can drop files in the container at `/var/www/html/`, they will
be nuked every time you stop the container. To avoid this pitfall, be
sure to layer in more permament storage. An example is provided in the
next section.

### Intended usage

Let's say you have a directory called `my_files` contained in your
current working directory. Also, for the sake of this example, you might
want a server running locally at port `8888`. With these assumptions,
you can run the following:

`docker run -p 8888:80 -v $PWD/my_files:/var/www/html garrett/webdev-simple`

And, after a short while*, you will have a server at
<http://localhost:8888/> serving all your precious files.

\* Where "short" is near instantatneous, except for the very first time
(as Docker will need to download the necessary image before proceeding).


## Misc.

### Rolling your own

You don't need to touch this git repo, unless you want to build your own
image. If that's the case, you'll want to clone the repo (or a fork of
this repo) and then run `docker build -t yourname/your-fork-here .` in
the directory of the checkout.

If you want to customize things, edit the docker file called `Dockerfile`.

Thankfully, Docker is smart and caches all the steps in your Docker file
that it can, so development of your container is pretty quick and easy.

### Running as a user (and not root!)

If you haven't already, you'll want to set up the `docker` command to be
called by your user, because it's The Right Thing to Do™.

On Fedora, setting this up looks like the following:
`sudo usermod -a -G docker YOUR_USERNAME`

(It's probably similar elsewhere too. If you don't have sudo set up yet,
then run the command as root, minus the `sudo` part.)

After running the above command, be sure to sign out and sign back in to
a new user session.

### Installing Docker

If you don't have Docker set up, [check out the wonderful Docker docs on
the subject](http://docs.docker.io/installation/).

#### Quick links to installing on commonly used systems

* [Fedora](http://docs.docker.io/installation/fedora/)
  (TL;DR: `sudo yum -y install docker-io && sudo systemctl enable docker
  && sudo systemctl start docker`)
* [RHEL/CentOS](http://docs.docker.io/installation/rhel/)
  (TL;DR: It's similar to Fedora, except use `sudo service docker start && sudo chkconfig docker on` instead of systemctl.)
* [openSUSE](http://docs.docker.io/installation/openSUSE/)
  (TL;DR: Add a repo, zypper it in, and systemctl it up!)
* [Ubuntu](http://docs.docker.io/installation/ubuntulinux/)
  (TL;DR: It depends. Read the docs and figure it out for your version.)
* [OS X](http://docs.docker.io/installation/mac/)
  or [read an even a simpler
  guide](http://arnaudchenyensu.com/how-to-install-docker-on-mac-os-x/)
  (TL;DR: It's complicated. But works.)
* [Windows](http://docs.docker.io/installation/windows/)
  (TL;DR: It's complicated too, but works in a way similar to OS X, but
  It's probably not as nice to use as anything else listed above.)

## License

CC0 / Public Domain — have fun!
https://creativecommons.org/publicdomain/zero/1.0/
