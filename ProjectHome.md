# libnfc #
This is development site of libnfc, the **Free/Libre Near Field Communication (NFC) Library**.

Important: due to googlecode restrictions, libnfc's download section is now hosted at https://bintray.com/nfc-tools/sources/libnfc

If you are new to libnfc, you should browse its dedicated wiki page[¹] to collect useful information and have a look to our forum[²].

What can you do with libnfc?

There are plenty of projects based on libnfc.
A few of them originate from the same development team, you can find more info on them on the nfc-tools wiki[³] and nfc-tools project[⁴]

## Installation ##
Installation steps are different depending on version you are willing to install.

### Stable version ###
Please follow instructions present in our main website.
http://www.libnfc.org/documentation/installation

### Development version ###
Fetch current version using Git as described in this page: http://code.google.com/p/libnfc/source/checkout

You can compile development version using:
#### Under MacOSX, GNU/Linux, `*`BSD and probably a lot of POSIX systems ####
Note: If you want all libnfc hardware drivers, you will need to have libusb (library and headers) plus on `*`BSD and GNU/Linux systems, libpcsclite (library and headers).

```
autoreconf -vis
./configure --enable-doc
make
sudo make install
```

If you want to (re)generate documentation:
```
make doc
```

## Links ##
  * `[1]` **Dedicated wiki page**: http://nfc-tools.org/index.php?title=Libnfc
  * `[2]` **Forum**: http://www.libnfc.org/community
  * `[3]` **Official wiki**: http://nfc-tools.org/
  * `[4]` **nfc-tools project**: http://nfc-tools.googlecode.com