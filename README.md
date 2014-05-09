bgems
=====

Proof-of-concept binary gems to simplify ruby deployment.

A bgem is a packed version of an installed rubygem.  You need to install
the gem first, normally, before you can create a .bgem.  However you
don't need to run the same ruby as installed the gem to pack it. You
need `tar` available.

Create a directory of bgems from a GEM\_HOME like so:

    $ bin/bgems-pack --gem-home $GEM_HOME

That will pack all your gems into `./bgems`.

There's a very simple installer, too:

    $ $GEM_HOME=~/.gems bin/bgem-install ./bgems/$WHATEVER.bgem

Native Dependencies
-------------------

If you're on Debian, pack your gems like so:

    $ bin/bgems-pack --gem-home=$GEM_HOME --depends

This will iterate over the native extensions, and use `ldd` and `dpkg
-S` to figure out which apt packages are dependencies of your gems.
This information is included in the .bgem file for you to use if you
wish to build `.deb` packages.  It's not currently used by
`bgem-install`, but it could be.

.bgem File Format
-----------------

A `.bgem` is just a tar file.  It includes the gem source, the
specification, and any binaries.  If you include `--depends`, it'll also
have `DEBIAN/<gem>.Depends` file listing the package names, one per
line.

Author
-----

Alex Young <alex@blackkettle.org>
