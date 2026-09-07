# FW Desktop - AMD Ryzen AI MAX+ 395

Note: All tests to AQC107

## WisdPi framework module

Note: All tests done from Rear USB4 port

### dmesg output when device plugged in (to rear USB4 port)

```
[  169.249330] usb 6-1: new SuperSpeed Plus Gen 2x1 USB device number 2 using xhci_hcd
[  169.261043] usb 6-1: New USB device found, idVendor=0bda, idProduct=815a, bcdDevice=30.00
[  169.261492] usb 6-1: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 0 ep 0x83: setting to 16
[  169.261510] usb 6-1: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 1 ep 0x83: setting to 16
[  169.261512] usb 6-1: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 2 ep 0x83: setting to 16
[  169.261514] usb 6-1: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 3 ep 0x83: setting to 16
[  169.261747] usb 6-1: Int endpoint with wBytesPerInterval of 8 in config 2 interface 0 altsetting 0 ep 0x83: setting to 16
[  169.261947] usb 6-1: Int endpoint with wBytesPerInterval of 8 in config 3 interface 0 altsetting 0 ep 0x83: setting to 16
[  169.262287] usb 6-1: New USB device strings: Mfr=1, Product=2, SerialNumber=7
[  169.262291] usb 6-1: Product: USB 10/100/1G/2.5G/5G/10G LAN
[  169.262293] usb 6-1: Manufacturer: Realtek
[  169.262295] usb 6-1: SerialNumber: 000334C8D6******
[  169.456379] r8152-cfgselector 6-1: reset SuperSpeed Plus Gen 2x1 USB device number 2 using xhci_hcd
[  169.612806] r8152 6-1:1.0 enp196s0f3u1: renamed from eth0
```

### USB connectivity

There are a few things going on here.  The device shows only "10000M" ports available, and that is the
maximum speed at which the r8159 connects.  However, it will not give full 10 gigabit throughput.

When the r8159 is connected to the module ports on the front of the Framework Desktop case, then there seems to be
a 5Gbit USB hub between the host controller and the ports, so the connection to the r8159 is only 5000M.
This is clearly not ideal, so it was not tested.

When connected to the back USB-C "USB 4" ports, then the connection shows the "10000M" speed.  This is what was
used for this testing.

### "lsusb -t" relevant output:

Front port (left):
```
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 002: Dev 002, If 0, Class=Hub, Driver=hub/2p, 5000M
        |__ Port 001: Dev 003, If 0, Class=Vendor Specific Class, Driver=r8152, 5000M
```

Front port (right):
```
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 002: Dev 002, If 0, Class=Hub, Driver=hub/2p, 5000M
        |__ Port 002: Dev 004, If 0, Class=Vendor Specific Class, Driver=r8152, 5000M
```

Rear USB4 port (lower):
```
/:  Bus 006.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/1p, 10000M
    |__ Port 001: Dev 002, If 0, Class=Vendor Specific Class, Driver=r8152, 10000M
```

### iperf TCP test, 30 seconds, single stream

```
$ iperf3 -c *** -t 30
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   812 MBytes  6.80 Gbits/sec    0   1.28 MBytes
[  5]   1.00-2.00   sec   810 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]   2.00-3.00   sec   808 MBytes  6.78 Gbits/sec    0   1.41 MBytes
[  5]   3.00-4.00   sec   810 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]   4.00-5.00   sec   810 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]   5.00-6.00   sec   808 MBytes  6.78 Gbits/sec    0   1.41 MBytes
[  5]   6.00-7.00   sec   810 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]   7.00-8.00   sec   808 MBytes  6.78 Gbits/sec    0   1.41 MBytes
[  5]   8.00-9.00   sec   808 MBytes  6.78 Gbits/sec    0   1.41 MBytes
[  5]   9.00-10.00  sec   808 MBytes  6.78 Gbits/sec    0   1.41 MBytes
[  5]  10.00-11.00  sec   810 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]  11.00-12.00  sec   808 MBytes  6.77 Gbits/sec    0   1.41 MBytes
[  5]  12.00-13.00  sec   809 MBytes  6.79 Gbits/sec    0   1.41 MBytes
[  5]  13.00-14.00  sec   808 MBytes  6.78 Gbits/sec    0   1.48 MBytes
[  5]  14.00-15.00  sec   810 MBytes  6.79 Gbits/sec    0   1.48 MBytes
[  5]  15.00-16.00  sec   807 MBytes  6.77 Gbits/sec    0   1.48 MBytes
[  5]  16.00-17.00  sec   809 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  17.00-18.00  sec   810 MBytes  6.79 Gbits/sec    0   2.21 MBytes
[  5]  18.00-19.00  sec   808 MBytes  6.77 Gbits/sec    0   2.21 MBytes
[  5]  19.00-20.00  sec   809 MBytes  6.79 Gbits/sec    0   2.21 MBytes
[  5]  20.00-21.00  sec   808 MBytes  6.77 Gbits/sec    0   2.21 MBytes
[  5]  21.00-22.00  sec   808 MBytes  6.77 Gbits/sec    0   2.21 MBytes
[  5]  22.00-23.00  sec   808 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  23.00-24.00  sec   808 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  24.00-25.00  sec   809 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  25.00-26.00  sec   808 MBytes  6.77 Gbits/sec    0   2.21 MBytes
[  5]  26.00-27.00  sec   808 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  27.00-28.00  sec   808 MBytes  6.78 Gbits/sec    0   2.21 MBytes
[  5]  28.00-29.00  sec   808 MBytes  6.77 Gbits/sec    0   2.21 MBytes
[  5]  29.00-30.00  sec   810 MBytes  6.79 Gbits/sec    0   2.21 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  23.7 GBytes  6.78 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  23.7 GBytes  6.78 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, reverse direction

```
$ iperf3 -c *** -t 30 -R
Reverse mode, remote host *** is sending
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   1.00-2.00   sec   917 MBytes  7.70 Gbits/sec
[  5]   2.00-3.00   sec   919 MBytes  7.70 Gbits/sec
[  5]   3.00-4.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   4.00-5.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   5.00-6.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   6.00-7.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   7.00-8.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   8.00-9.00   sec   918 MBytes  7.70 Gbits/sec
[  5]   9.00-10.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  10.00-11.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  11.00-12.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  12.00-13.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  13.00-14.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  14.00-15.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  15.00-16.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  16.00-17.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  17.00-18.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  18.00-19.00  sec   917 MBytes  7.70 Gbits/sec
[  5]  19.00-20.00  sec   919 MBytes  7.70 Gbits/sec
[  5]  20.00-21.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  21.00-22.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  22.00-23.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  23.00-24.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  24.00-25.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  25.00-26.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  26.00-27.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  27.00-28.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  28.00-29.00  sec   918 MBytes  7.70 Gbits/sec
[  5]  29.00-30.00  sec   918 MBytes  7.70 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  26.9 GBytes  7.70 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  26.9 GBytes  7.70 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, bidirectional

```
$ iperf3 -c *** -t 30 --bidir
[ ID][Role] Interval           Transfer     Bitrate         Retr  Cwnd
[  5][TX-C]   0.00-1.00   sec   728 MBytes  6.10 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   0.00-1.00   sec   862 MBytes  7.22 Gbits/sec
[  5][TX-C]   1.00-2.00   sec   733 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   1.00-2.00   sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]   2.00-3.00   sec   733 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   2.00-3.00   sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]   3.00-4.00   sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   3.00-4.00   sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]   4.00-5.00   sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   4.00-5.00   sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]   5.00-6.00   sec   733 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   5.00-6.00   sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]   6.00-7.00   sec   733 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   6.00-7.00   sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]   7.00-8.00   sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   7.00-8.00   sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]   8.00-9.00   sec   732 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   8.00-9.00   sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]   9.00-10.00  sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]   9.00-10.00  sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]  10.00-11.00  sec   733 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]  10.00-11.00  sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]  11.00-12.00  sec   733 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]  11.00-12.00  sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]  12.00-13.00  sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]  12.00-13.00  sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]  13.00-14.00  sec   732 MBytes  6.14 Gbits/sec    0   1.61 MBytes
[  7][RX-C]  13.00-14.00  sec   862 MBytes  7.23 Gbits/sec
[  5][TX-C]  14.00-15.00  sec   734 MBytes  6.15 Gbits/sec    0   1.61 MBytes
[  7][RX-C]  14.00-15.00  sec   861 MBytes  7.23 Gbits/sec
[  5][TX-C]  15.00-16.00  sec   728 MBytes  6.11 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  15.00-16.00  sec   860 MBytes  7.21 Gbits/sec
[  5][TX-C]  16.00-17.00  sec   732 MBytes  6.14 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  16.00-17.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  17.00-18.00  sec   731 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  17.00-18.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  18.00-19.00  sec   730 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  18.00-19.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  19.00-20.00  sec   730 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  19.00-20.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  20.00-21.00  sec   731 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  20.00-21.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  21.00-22.00  sec   730 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  21.00-22.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  22.00-23.00  sec   731 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  22.00-23.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  23.00-24.00  sec   730 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  23.00-24.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  24.00-25.00  sec   730 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  24.00-25.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  25.00-26.00  sec   729 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  25.00-26.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  26.00-27.00  sec   731 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  26.00-27.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  27.00-28.00  sec   730 MBytes  6.13 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  27.00-28.00  sec   860 MBytes  7.22 Gbits/sec
[  5][TX-C]  28.00-29.00  sec   730 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  28.00-29.00  sec   861 MBytes  7.22 Gbits/sec
[  5][TX-C]  29.00-30.00  sec   729 MBytes  6.12 Gbits/sec    0   3.41 MBytes
[  7][RX-C]  29.00-30.00  sec   861 MBytes  7.22 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID][Role] Interval           Transfer     Bitrate         Retr
[  5][TX-C]   0.00-30.00  sec  21.4 GBytes  6.14 Gbits/sec    0            sender
[  5][TX-C]   0.00-30.00  sec  21.4 GBytes  6.14 Gbits/sec                  receiver
[  7][RX-C]   0.00-30.00  sec  25.2 GBytes  7.22 Gbits/sec    0            sender
[  7][RX-C]   0.00-30.00  sec  25.2 GBytes  7.22 Gbits/sec                  receiver

iperf Done.
```
