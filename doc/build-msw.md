WINDOWS BUILD NOTES
===================
this doc is for old bitcoin dev environment.
new env is not match the following.

Compilers Supported
-------------------
TODO: What works?
Note: releases are cross-compiled using mingw running on Linux.


Dependencies
------------
Libraries you need to download separately and build:

	name            default path               download
	--------------------------------------------------------------------------------------------------------------------
	OpenSSL         \openssl-1.0.1k-mgw        http://www.openssl.org/source/
	Berkeley DB     \db-4.8.30.NC-mgw          http://www.oracle.com/technology/software/products/berkeley-db/index.html
	Boost           \boost-1.5x.0-mgw          http://www.boost.org/users/download/
	miniupnpc       \miniupnpc-2.0-mgw         http://miniupnp.tuxfamily.org/files/

Their licenses:

	OpenSSL        Old BSD license with the problematic advertising requirement
	Berkeley DB    New BSD license with additional requirement that linked software must be free open source
	Boost          MIT-like license
	miniupnpc      New (3-clause) BSD license

Versions used in this release:

	OpenSSL      1.0.1k
	Berkeley DB  4.8.30.NC
	Boost        1.5x.0
	miniupnpc    2.0


OpenSSL
-------
MSYS shell:

un-tar sources with MSYS 'tar xfz' to avoid issue with symlinks (OpenSSL ticket 2377)
change 'MAKE' env. variable from 'C:\MinGW32\bin\mingw32-make.exe' to '/c/MinGW32/bin/mingw32-make.exe'

	cd /c/openssl-1.0.1k-mgw
	./config
	make

Berkeley DB
-----------
MSYS shell:

	cd /c/db-4.8.30.NC-mgw/build_unix
	sh ../dist/configure --enable-mingw --enable-cxx
	make

Boost
-----
MSYS shell:

	downloaded boost jam 3.1.18
	cd \boost-1.5x.0-mgw
	bjam toolset=gcc --build-type=complete stage

MiniUPnPc
---------
UPnP support is optional, make with `USE_UPNP=` to disable it.

MSYS shell:

	cd /c/miniupnpc-2.0-mgw
	make -f Makefile.mingw
	mkdir miniupnpc
	cp *.h miniupnpc/

Yenten
-------
MSYS shell:

	cd \yenten
	sh autogen.sh
	sh configure
	mingw32-make
	strip yentend.exe
