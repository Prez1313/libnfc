# Product version #
Since 1.2.x, we use a this numbering schemes:
The libnfc's version is composed as "A.B.C", where the number A denotes the libnfc version, the number B denotes the major revision of the libnfc, and the number C indicates the minor revision of the libnfc.
The major revision is used according to the traditional even-odd system version numbering system. The minor revision is changed whenever security patches, bug fixes, new features or drivers are implemented in the libnfc.

# Library version (libtool) #
The library number is determined following:
http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html

# Debian version #
## Releases ##
The debian version follow the standard:
The libnfc debian package version is composed as "A.B.C-D, where "A.B.C" comes from libnfc's version and D denotes the debian package version.

## Upstream version ##
In this case, the libnfc debian package version is composed as "A.B.CpreN.D-0", where "A.B.C" is the last released libnfc version, "N" is the next minor libnfc version and "D" denotes the debian package pre-version.


e.g. Starting from 1.5.0pre1.2-0...

That is, 1.5.0pre1 is the upstream version ("1.5.1 in preparation")
and .2 is the upstream revision number of the debian subdirectory.
```
Event                           New version number in debian/changelog
------------------------------  --------------------------------------
Make another change in debian/  1.5.0pre1.3-0
Release                         1.5.1-0
Start new branch after release  1.5.1pre2.0-0
```