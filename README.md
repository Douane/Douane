# Douane

Douane is a firewall that filter and limit the outgoing network traffic per application.

You can allow network traffic for some applications and deny network traffic for others.

### How it is working

When Douane is started it will watch the ougoing network traffic and as soon as an unknown application generate some traffic Douane will block it and ask you if you allow it or not:

![Douane - Question window](https://pbs.twimg.com/media/BNIv_V2CEAAPPyi.png:large)

The application is composed of 3 parts written in different programmtion languages.

#### Linux kernel module

The [Linux Kernel Module](https://en.wikipedia.org/wiki/Loadable_kernel_module) is the heart of Douane as it will catch outgoing network packets and find owning application.

Written in C it use [Netfilter](http://www.netfilter.org/) to watch the network traffic.

#### Daemon process

This is the brain of Douane as it will ask you and remind your decisions to allow/deny network traffic.

Written in C++ it provide a [D-Bus](dbus.freedesktop.org/) server that I will describe soon, a [GTK 3](http://www.gtk.org/) part to ask you when an unknown application is sending network packets written with [gtkmm 3](http://www.gtkmm.org/) and [boost](http://www.boost.org/) to clue some parts.

#### Configurator

Finally the configurator allow you to edit the configuration (rules, load on boot, ...).

![Douane - Configurator](https://pbs.twimg.com/media/BNdVVAOCQAI8CRr.png:large)

The configuration is written in [python 3](http://www.python.org/) and GTK 3 using [PyGObject](https://live.gnome.org/PyGObject), is open source and is an interface to the D-Bus server provided by the daemon process.

The twitter area on the right is my [GtkTwitterBox](https://github.com/zedtux/gtktwitterbox).

### Feature requests and Bug reporting

If you found a bug or have an idea to improve Douane your input is more than welcome!

[Fill in a new Github issue](https://github.com/zedtux/Douane/issues/new) in this project and I will have a look at it.


**For the first release the application I didn't implemented so much features in order to keep it simple as possible in order to focus more on the stability of the application.**

**Now that the application is quite stable (let's see for bug report) I can implement new features so do not hesitate to ask!!**

### Licencing

As of today the Douane kernel module and daemon process are closed source but the configurator is open source. Also the D-Bus server should give you access to a lot of information that could help you in building new application based on filtered out-going traffic.

### Dependencies

**LKM:**

    dkms linux-headers-`uname -r`

**Daemon:**

    liblog4cxx10-dev libboost-filesystem-dev libboost-regex-dev libboost-signals-dev libgtkmm-3.0-dev libdbus-c++-dev libdbus-1-dev

**Configurator:**

    gksu
