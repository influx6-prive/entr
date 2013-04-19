Event Notify Test Runner
========================

A utility for running arbitrary commands when files change. Uses
[kqueue(2)][kqueue_2] to avoid polling. `entr` responds to file system events by
executing command line arguments or by writing to a FIFO.

`entr` was written to provide to make rapid feedback and automated testing
natural and completely ordinary.

Installation - BSD & Mac OS
---------------------------

    ./configure
    make test
    make install

Installation - Mac OS/Homebrew
------------------------------

    brew tap mitchty/entr
    brew install entr

Installation - Debian Linux
---------------------------

    apt-get install libkqueue-dev
    ./configure
    make test
    make install

Installation - Red Hat Linux
----------------------------

Get & install [libkqueue][libkqueue]

    ./configure
    make && make rpm
    sudo rpm -ivh pkg/libkqueue-1.0-1.x86_64.rpm

Build entr

    ./configure
    make test
    make install

Examples
--------

Recompile if header files change

    $ find. -name '*.c' | entr make

Launch and auto-reload a node.js server

    $ ls *.js | entr -r node index.js

Convert any altered Markdown in the current directory to HTML using a
FIFO

    $ ls *.md | entr +notify &
    $ while read F
    > do
    >   markdown2html $F
    > done < notify

Releases History
----------------

1.9 New auto-reload option _2013-04-13_

1.8 Loosing a file under watch is always fatal _2012-12-05_

1.7 Successfully stat deleted files before running a command _2012-11-20_

1.6 Works with NFS mounts on Linux, no need for pthreads on BSD _2012-08-10_

1.5 Support interactive applications by opening a TTY _2012-07-29_

1.4 New regression tests and better Linux support _2012-05-22_

1.3 New FIFO mode and better support of Mac OS _2012-05-17_

1.2 Support for Linux via [libkqueue][libkqueue] _2012-04-26_

1.1 Support for Mac OS added. _2012-04-17_  

1.0 Tested on all the major BSDs, included in OpenBSD 5.2 ports under
`sysutils/entr`. _2012-04-12_  


[kqueue_2]: http://www.openbsd.org/cgi-bin/man.cgi?query=kqueue&apropos=0&sektion=0&manpath=OpenBSD+Current&format=html
[libkqueue]: http://www.heily.com/~mheily/proj/libkqueue/dist/
