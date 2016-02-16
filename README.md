[![PyPI version](https://badge.fury.io/py/pytelemetrycli.svg)](https://badge.fury.io/py/pytelemetrycli) [![Join the chat at https://gitter.im/Overdrivr/pytelemetry](https://badges.gitter.im/Overdrivr/pytelemetry.svg)](https://gitter.im/Overdrivr/pytelemetry?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Stories in Ready](https://badge.waffle.io/Overdrivr/pytelemetrycli.svg?label=ready&title=Ready)](http://waffle.io/Overdrivr/pytelemetrycli)

## pytelemetry command line interface

This tool enables superior communication with any embedded device. It is for you if:

* you are using `printf` to debug your application
* you are all the time re-writing custom protocols for the serial port
* you need a **reliable** and **error-tolerant** communication protocol
* you want to finely tune your application without loosing time compiling & flashing just to tune a parameter
* you want to **plot** parameters on the device in **real-time**
* your embedded device has very limited resources and will tolerate only a lightweight communication library

## overview
pytelemetry-cli is a **command line interface**. It provides a set of commands to connect to a device, read, plot and write data on it.

![Overview](https://raw.githubusercontent.com/Overdrivr/pytelemetrycli/master/overview.png)

pytelemetry-cli relies on [`pytelemetry`](https://github.com/Overdrivr/pytelemetry)
[![PyPI version](https://badge.fury.io/py/pytelemetry.svg)](https://badge.fury.io/py/pytelemetry)
to implement the specific communication protocol.

To communicate with the device, you only need to make your device use the [`telemetry`](https://github.com/Overdrivr/pytelemetry)
library.

## principle
The underlying communication protocol mostly follows the [PubSub](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)(publish/subscribe) messaging pattern.

> [..] messages are published to "topics" or named logical channels. Subscribers in a topic-based system will receive all messages published to
> the topics to which they subscribe [..].
> *Source: Wikipedia*

## interface and plot widget
Aan example of listing serial ports `ls -s`, connecting to a device through COM20 `serial com20 --bauds 115200`, listing all received topics `ls` and opening a plot on topic touch `plot touch`

![Console example](https://raw.githubusercontent.com/Overdrivr/pytelemetrycli/master/console.png)

![Plot example](https://raw.githubusercontent.com/Overdrivr/pytelemetrycli/master/graph.png)


## installation
`pytelemetrycli` requires python 3.5+, PyQt4 and numpy.

### Windows
It is recommended to download [`numpy`](http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) and [`PyQt4`](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pyqt4) wheels python packages (courtesy of Christoph Gohlke).

In case you were wondering, **no** you **don't** have to install Qt. The binary wheel is enough.

Then install with pip the downloaded files

```bash
pip install numpy-x.xx.x+vanilla-cp3x-none-winxxx.whl
pip install PyQt4-x.xx.x-cp3x-none-winxxx.whl
```

Then, simply install `pytelemetrycli` with pip as usual

```bash
pip install pytelemetrycli
```

### Mac OS
The easiest way to install numpy and PyQt4 seem to be using `homebrew`.
lease note that you should also have installed python 3.5 with homebrew for this to work correctly.
Also, avoid to have another python 3.5 distribution on your system otherwise you will face import issues as well.

```bash
brew install python3
brew install pyqt --with-python3
pip3 install pytelemetrycli
```

### Linux

?

## setup for embedded devices
To setup telemetry on any embedded device, please refer to the [`Telemetry`](https://github.com/Overdrivr/Telemetry) repository.

If you only wish to test the command-line interface, you can also directly flash a test firmware from our own [collection](#)
*Note: in process. In the future we will support a variety of devices so you can quickly start on with the command line.*

## List of commands
The command line interface can be started like this
```
python3 -m pytelemetrycli.cli
```
or more simply
```
pytlm
```
If everything is installed properly, `:>` should welcome you.
```
pytelemetry terminal started. (type help for a list of commands.)
:> _
```

### help [command]
Without arguments, you get a list of all available commands. Otherwise the full `command` documentation.

### ls
```bash
Without options, prints a list of all received topics.
With the --serial flag, prints a list of all available COM ports

Usage: ls [options]

Options:
-s, --serial     Use this flag to print a list of all available serial ports
```

### serial
```bash
Connects pytelemetry to the serial port.

Usage: serial <port> [options]

Options:
-b X, --bauds X        Connection speed in bauds  [default: 9600]
```

### print
```bash
Prints X last received samples from <topic>.

Usage: print <topic> [options]

Options:
-a X, --amount X        Amount of samples to display [default: 1]
```

### pub
```bash
Publishes a (value | string) on <topic>.

Usage: pub <topic> <value> (--u8 | --u16 | --u32 | --i8 | --i16 | --i32 | --f32 | --s)
```

### plot
```bash
Plots <topic> in a graph window.

Usage: plot <topic>
```

### disconnect
```bash
Disconnects from any open connection.

Usage: disconnect
```

### quit
```bash
Exits the terminal application.

Usage: quit
```
