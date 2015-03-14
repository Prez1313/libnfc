# libnfc-1.4 #

The aim of this release is to stabilise the current libnfc infrastructure.  The library has grown quite hard recently but a few things are prone to long-term issues. In order to avoid posteponing an update of the libnfc, we focus on polishing the code and implementing better error management before releasing a 1.4 stable release.

## Error reporting ##

The following graphs represent the communication involved when sending a command to a NFC device (here a device with a PN532 connected via USB), and the dotted arows represent possible communication chanels not use in that context.  As you can see, the current architecture is a bit simple (less arrows for communication) but really confusing because some function calls cannot be done directly at the chip driver level and so the code mix direct call to device driver with indirect calss through the chip driver.

### Previous call path ###
<table><tr><td><img src='http://libnfc.googlecode.com/svn/wiki/graphs/libnfc-1.3.png' /></td><td>
<ol><li>pn53x_transceive()<br>
</li><li>pn53x_usb_transceive()<br>
</li><li>usb_bulk_write() The command is send to the device<br>
</li><li>usb_bulk_read() The device sends an ACK / NACK<br>
</li><li>Depending on the status<br>
<ol><li>usb_bulk_read() if the command was send successfuly to read the command result<br>
</li><li>return an error otherwise (5.2.1, 5.2.2) (<b>function terminates</b>)<br>
</li></ol></li><li>return the command result<br>
</li><li>usb_bulk_write() Send an ACK to the device (not done currently)<br>
</li><li>return the command result<br>
</td></tr></table></li></ol>


### New call path ###
<table><tr><td><img src='http://libnfc.googlecode.com/svn/wiki/graphs/libnfc-1.4.png' /></td><td>
<ol><li>pn53x_transceive()<br>
</li><li>pn53x_usb_transceive()<br>
</li><li>usb_bulk_write() The command is send to the device<br>
</li><li>usb_bulk_read() The device sends an ACK / NACK<br>
</li><li>The reply is returned to the PN53x management code<br>
</li><li>Depending on the result<br>
<ol><li>If the device ACKed the command, execution continues  was sent successfuly<br>
</li><li>An error is returned bach to the USB interface and propagates to the library (6.2.1, 6.2.2, 6.2.3) (<b>function terminates</b>)<br>
</li></ol></li><li>usb_bulk_read() The device sends the response<br>
</li><li>The response is returned to the PN53x management code<br>
</li><li>A request for ACK is sent to the USB interface<br>
</li><li>usb_bulk_write() Send an ACK to the device<br>
</li><li>return the command result<br>
</td></tr></table></li></ol>

In the old implementation (libnfc-1.3 and before), each device driver did it's own error detection (if any) and a lot of code was redundant (if not forgotten).  The new implementation is slightly more complex but it's only a transition to what we would like to have in libnfc-1.6.

ETA: september 2010

---

# libnfc-1.6 #

The focus for 1.6 is a better abstraction of NFC devices.  As of 1.3.x, we already have concepts of drivers and chips, but the overall architecture is pn53x-centric, and while there is no plan to support any other chip at the time of writing, this could became a major issue when we will decide to do so.  It has so been decided to rework the way NFC devices are handled and provide a device agnostic and consistent API for NFC targets manipulation


## Better abstraction ##

### Expected call path ###
<table><tr><td><img src='http://libnfc.googlecode.com/svn/wiki/graphs/libnfc-1.6.png' /></td><td>
<ol><li>pn53x_transceive()<br>
</li><li>pn53x_usb_transceive()<br>
</li><li>usb_bulk_write() The command is send to the device<br>
</li><li>usb_bulk_read() The device sends an ACK / NACK<br>
</li><li>The reply is returned to the PN53x management code<br>
</li><li>Depending on the result<br>
<ol><li>A request to read the response is send to the USB interface if the command was sent successfuly<br>
</li><li>An error is returned if the command was not sent correctly (<b>function terminates</b>)<br>
</li></ol></li><li>usb_bulk_read() The device sends the response<br>
</li><li>The response is returned to the PN53x management code<br>
</li><li>A request for ACK is sent to the USB interface<br>
</li><li>usb_bulk_write() Send an ACK to the device<br>
</li><li>return the command result<br>
</td></tr></table></li></ol>

The goal is to provide consistent and reusable interfaces (API) that could be as follows:

### Drivers API ###
  * driver\_init
  * driver\_list\_devices
  * driver\_connect
  * driver\_transceive
  * driver\_disconnect
  * driver\_free

### Interfaces API ###
  * interface\_init
  * interface\_list\_device
  * interface\_open
  * interface\_read
  * interface\_write
  * interface\_close
  * interface\_free

ETA: TBD

---

# libnfc-1.8 #

Nothing discussed yet.  I guess there is a log of nfc-ip stuff here.

ETA: TBD