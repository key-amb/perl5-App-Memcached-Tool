# NAME

__memcached-tool__ - A porting of [memcached/memcached-tool](https://github.com/memcached/memcached/blob/master/scripts/memcached-tool)

# SYNOPSIS

General:

    # Ported style from original memcached-tool
    memcached-tool <host[:port] | /path/to/socket> [mode] [options]

    # Without 1st arg, connects 127.0.0.1:11211 by default
    memcached-tool [mode] [options]

    # You can provide <addr> or <mode> by option style
    memcached-tool --addr|-a <host[:port] | /path/to/socket> --mode|-m <mode> [options]
    memcached-tool --mode|-m <mode> [options]

Modes Summary:

    memcached-tool [addr] [options]          # same with 'display'
    memcached-tool [addr] display  [options] # show slabs
    memcached-tool [addr] stats    [options] # show general stats
    memcached-tool [addr] settings [options] # show settings stats
    memcached-tool [addr] dump     [options] # dumps keys and values

Mode for Development:

    memcached-tool [addr] sizes [options]    # shows sizes stats

Type `memcached-tool man` to check the risk of this command.

Help or Manual:

    memcached-tool help|-h|--help
    memcached-tool man|--man

# DESCRIPTION

This script is a porting of
[memcached/memcached-tool](https://github.com/memcached/memcached/blob/master/scripts/memcached-tool)
which is in the public domain.

Follwing description comes from man(1) of original _memcached-tool_:

The first parameter specifies the address of the daemon either by a hostname,
optionally followed by the port number (the default is 11211), or a path to
UNIX domain socket. The second parameter specifies the mode in which the tool
should run.

# MODES

Following description comes from man(1) or usage of original _memcached-tool_.

- __display__

    Print slab class statistics. This is the default mode if no mode is specified.
    The printed columns are:

    - __#__

        Number of the slab class.

    - __Item\_Size__

        The amount of space each chunk uses. One item uses one chunk of the
        appropriate size.

    - __Max\_age__

        Age of the oldest item in the LRU.

    - __Pages__

        Total number of pages allocated to the slab class.

    - __Count__

        Number of items presently stored in this class. Expired items are not
        automatically excluded.

    - __Full?__

        Yes if there are no free chunks at the end of the last allocated page.

    - __Evicted__

        Number of times an item had to be evicted from the LRU before it expired.

    - __Evict\_Time__

        Seconds since the last access for the most recent item evicted from this
        class.

    - __OOM__

        Number of times the underlying slab class was unable to store a new item.

- __stats__

    Print general-purpose statistics of the daemon. Each line contains the name of
    the statistic and its value.

- __dump__

    Make a partial dump of the cache written in the add statements of the
    memcached protocol.

- __settings__

    Show settings stats.

- __sizes__

    Shows sizes stats.

    __WARNING__: This is a development command.

    As of 1.4 it is still the only command which will lock your memcached instance
    for some time.

    If you have many millions of stored items, it can become unresponsive for several
    minutes.

    Run this at your own risk. It is roadmapped to either make this feature optional
    or at least speed it up.

# OPTIONS

- __-t|--timeout=Int__

    Sets connection timeout. Default is 5 seconds.

- __-d|--debug__

    Shows debug logs.

# SEE ALSO

[App::Memcached::Tool](https://metacpan.org/pod/App::Memcached::Tool),
__memcached(1)__,
[http://www.memcached.org/](http://www.memcached.org/)

# AUTHORS

YASUTAKE Kiyoshi <yasutake.kiyoshi@gmail.com>

# LICENSE

Copyright (C) 2015 YASUTAKE Kiyoshi.

This library is free software; you can redistribute it and/or modify it under
the same terms as Perl itself.  That means either (a) the GNU General Public
License or (b) the Artistic License.
