Installation
============

**TLDR: [http://asciinema.org/a/6863](http://asciinema.org/a/6863)**

Make sure .env is configured to alter your enviroment variables. I'd recommand using [autoenv](https://github.com/kennethreitz/autoenv) or [foreman](https://github.com/ddollar/foreman) or run

    DOCKER_URL=http://127.0.0.1:5555

Requires [Vagrant](http://downloads.vagrantup.com/tags/v1.3.5) + [VirtualBox](https://www.virtualbox.org/wiki/Downloads) to be installed.

Next install [fig](https://github.com/orchardup/fig/).

    $ sudo pip install fig

With all the requirements setup, let's boot up everything.

    $ vagrant up
    $ fig up

To check everything has work, go to [http://127.0.0.1:8000](http://127.0.0.1:8000).