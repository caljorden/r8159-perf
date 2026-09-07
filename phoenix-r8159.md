# Framework Laptop 13 - AMD Ryzen 7 7840u

Note: All tests to AQC107

## WisdPi framework module

### dmesg output when device plugged in (Expansion port 2)

```
[   97.276490] usb 2-2: new SuperSpeed Plus Gen 2x1 USB device number 2 using xhci_hcd
[   97.289189] usb 2-2: New USB device found, idVendor=0bda, idProduct=815a, bcdDevice=30.00
[   97.289723] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 0 ep 0x83: setting to 16
[   97.289734] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 1 ep 0x83: setting to 16
[   97.289739] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 2 ep 0x83: setting to 16
[   97.289743] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 3 ep 0x83: setting to 16
[   97.290068] usb 2-2: Int endpoint with wBytesPerInterval of 8 in config 2 interface 0 altsetting 0 ep 0x83: setting to 16
[   97.290358] usb 2-2: Int endpoint with wBytesPerInterval of 8 in config 3 interface 0 altsetting 0 ep 0x83: setting to 16
[   97.290812] usb 2-2: New USB device strings: Mfr=1, Product=2, SerialNumber=7
[   97.290818] usb 2-2: Product: USB 10/100/1G/2.5G/5G/10G LAN
[   97.290822] usb 2-2: Manufacturer: Realtek
[   97.290825] usb 2-2: SerialNumber: 000334C8D6******
[   97.481161] r8152-cfgselector 2-2: reset SuperSpeed Plus Gen 2x1 USB device number 2 using xhci_hcd
[   97.680030] r8152 2-2:1.0 enp193s0f3u2: renamed from eth0
```

### USB connectivity

This is relatively simple.  The device shows only "10000M" ports available, and that is the
speed at which the r8159 connects.  However, it will not give full 10 gigabit throughput.

### "lsusb -t" relevant output:

Expansion port 1:
```
/:  Bus 008.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/1p, 10000M
    |__ Port 001: Dev 002, If 0, Class=Vendor Specific Class, Driver=r8152, 10000M
```

Expansion port 2 (used for this testing):
```
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 002: Dev 002, If 0, Class=Vendor Specific Class, Driver=r8152, 10000M
```

### iperf TCP test, 30 seconds, single stream

```
$ iperf3 -c *** -t 30
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   709 MBytes  5.94 Gbits/sec    0   1.35 MBytes
[  5]   1.00-2.00   sec   706 MBytes  5.92 Gbits/sec    0   1.44 MBytes
[  5]   2.00-3.00   sec   738 MBytes  6.20 Gbits/sec    0   1.63 MBytes
[  5]   3.00-4.00   sec   763 MBytes  6.40 Gbits/sec    0   1.72 MBytes
[  5]   4.00-5.00   sec   766 MBytes  6.42 Gbits/sec    0   1.84 MBytes
[  5]   5.00-6.00   sec   766 MBytes  6.43 Gbits/sec    0   1.95 MBytes
[  5]   6.00-7.00   sec   766 MBytes  6.43 Gbits/sec    0   1.95 MBytes
[  5]   7.00-8.00   sec   767 MBytes  6.44 Gbits/sec    0   2.05 MBytes
[  5]   8.00-9.00   sec   766 MBytes  6.42 Gbits/sec    0   2.05 MBytes
[  5]   9.00-10.00  sec   766 MBytes  6.42 Gbits/sec    0   2.05 MBytes
[  5]  10.00-11.00  sec   767 MBytes  6.44 Gbits/sec    0   2.05 MBytes
[  5]  11.00-12.00  sec   766 MBytes  6.42 Gbits/sec    0   2.05 MBytes
[  5]  12.00-13.00  sec   766 MBytes  6.43 Gbits/sec    0   2.05 MBytes
[  5]  13.00-14.00  sec   766 MBytes  6.43 Gbits/sec    0   2.05 MBytes
[  5]  14.00-15.00  sec   766 MBytes  6.43 Gbits/sec    0   2.05 MBytes
[  5]  15.00-16.00  sec   766 MBytes  6.43 Gbits/sec    0   2.05 MBytes
[  5]  16.00-17.00  sec   767 MBytes  6.43 Gbits/sec    0   2.05 MBytes
[  5]  17.00-18.00  sec   766 MBytes  6.42 Gbits/sec    0   2.65 MBytes
[  5]  18.00-19.00  sec   767 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  19.00-20.00  sec   765 MBytes  6.42 Gbits/sec    0   2.65 MBytes
[  5]  20.00-21.00  sec   768 MBytes  6.44 Gbits/sec    0   2.65 MBytes
[  5]  21.00-22.00  sec   765 MBytes  6.42 Gbits/sec    0   2.65 MBytes
[  5]  22.00-23.00  sec   766 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  23.00-24.00  sec   766 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  24.00-25.00  sec   766 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  25.00-26.00  sec   767 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  26.00-27.00  sec   766 MBytes  6.42 Gbits/sec    0   2.65 MBytes
[  5]  27.00-28.00  sec   767 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  28.00-29.00  sec   766 MBytes  6.43 Gbits/sec    0   2.65 MBytes
[  5]  29.00-30.00  sec   767 MBytes  6.43 Gbits/sec    0   2.65 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  22.3 GBytes  6.39 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  22.3 GBytes  6.39 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, reverse direction

```
$ iperf3 -c *** -t 30 -R
Reverse mode, remote host *** is sending
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   1.00-2.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   2.00-3.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   3.00-4.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   4.00-5.00   sec   830 MBytes  6.97 Gbits/sec
[  5]   5.00-6.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   6.00-7.00   sec   830 MBytes  6.97 Gbits/sec
[  5]   7.00-8.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   8.00-9.00   sec   830 MBytes  6.96 Gbits/sec
[  5]   9.00-10.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  10.00-11.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  11.00-12.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  12.00-13.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  13.00-14.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  14.00-15.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  15.00-16.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  16.00-17.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  17.00-18.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  18.00-19.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  19.00-20.00  sec   831 MBytes  6.96 Gbits/sec
[  5]  20.00-21.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  21.00-22.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  22.00-23.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  23.00-24.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  24.00-25.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  25.00-26.00  sec   831 MBytes  6.97 Gbits/sec
[  5]  26.00-27.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  27.00-28.00  sec   830 MBytes  6.96 Gbits/sec
[  5]  28.00-29.00  sec   830 MBytes  6.97 Gbits/sec
[  5]  29.00-30.00  sec   830 MBytes  6.97 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  24.3 GBytes  6.97 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  24.3 GBytes  6.96 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, bidirectional

```
$ iperf3 -c *** -t 30 --bidir
[ ID][Role] Interval           Transfer     Bitrate         Retr  Cwnd
[  5][TX-C]   0.00-1.00   sec   511 MBytes  4.28 Gbits/sec    0   1.82 MBytes
[  7][RX-C]   0.00-1.00   sec   721 MBytes  6.04 Gbits/sec
[  5][TX-C]   1.00-2.00   sec   598 MBytes  5.01 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   1.00-2.00   sec   707 MBytes  5.93 Gbits/sec
[  5][TX-C]   2.00-3.00   sec   675 MBytes  5.66 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   2.00-3.00   sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]   3.00-4.00   sec   696 MBytes  5.84 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   3.00-4.00   sec   686 MBytes  5.75 Gbits/sec
[  5][TX-C]   4.00-5.00   sec   701 MBytes  5.88 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   4.00-5.00   sec   686 MBytes  5.75 Gbits/sec
[  5][TX-C]   5.00-6.00   sec   701 MBytes  5.88 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   5.00-6.00   sec   687 MBytes  5.76 Gbits/sec
[  5][TX-C]   6.00-7.00   sec   700 MBytes  5.88 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   6.00-7.00   sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]   7.00-8.00   sec   704 MBytes  5.90 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   7.00-8.00   sec   684 MBytes  5.74 Gbits/sec
[  5][TX-C]   8.00-9.00   sec   702 MBytes  5.88 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   8.00-9.00   sec   687 MBytes  5.77 Gbits/sec
[  5][TX-C]   9.00-10.00  sec   700 MBytes  5.87 Gbits/sec    0   2.21 MBytes
[  7][RX-C]   9.00-10.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  10.00-11.00  sec   703 MBytes  5.90 Gbits/sec    0   2.21 MBytes
[  7][RX-C]  10.00-11.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  11.00-12.00  sec   706 MBytes  5.92 Gbits/sec    0   2.21 MBytes
[  7][RX-C]  11.00-12.00  sec   686 MBytes  5.76 Gbits/sec
[  5][TX-C]  12.00-13.00  sec   704 MBytes  5.91 Gbits/sec    0   2.21 MBytes
[  7][RX-C]  12.00-13.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  13.00-14.00  sec   700 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  13.00-14.00  sec   688 MBytes  5.78 Gbits/sec
[  5][TX-C]  14.00-15.00  sec   704 MBytes  5.91 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  14.00-15.00  sec   687 MBytes  5.76 Gbits/sec
[  5][TX-C]  15.00-16.00  sec   700 MBytes  5.87 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  15.00-16.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  16.00-17.00  sec   702 MBytes  5.89 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  16.00-17.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  17.00-18.00  sec   702 MBytes  5.89 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  17.00-18.00  sec   688 MBytes  5.78 Gbits/sec
[  5][TX-C]  18.00-19.00  sec   700 MBytes  5.87 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  18.00-19.00  sec   687 MBytes  5.76 Gbits/sec
[  5][TX-C]  19.00-20.00  sec   700 MBytes  5.87 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  19.00-20.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  20.00-21.00  sec   701 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  20.00-21.00  sec   688 MBytes  5.78 Gbits/sec
[  5][TX-C]  21.00-22.00  sec   700 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  21.00-22.00  sec   689 MBytes  5.78 Gbits/sec
[  5][TX-C]  22.00-23.00  sec   701 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  22.00-23.00  sec   689 MBytes  5.78 Gbits/sec
[  5][TX-C]  23.00-24.00  sec   701 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  23.00-24.00  sec   683 MBytes  5.73 Gbits/sec
[  5][TX-C]  24.00-25.00  sec   700 MBytes  5.87 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  24.00-25.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  25.00-26.00  sec   700 MBytes  5.87 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  25.00-26.00  sec   689 MBytes  5.78 Gbits/sec
[  5][TX-C]  26.00-27.00  sec   702 MBytes  5.89 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  26.00-27.00  sec   687 MBytes  5.76 Gbits/sec
[  5][TX-C]  27.00-28.00  sec   701 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  27.00-28.00  sec   688 MBytes  5.77 Gbits/sec
[  5][TX-C]  28.00-29.00  sec   701 MBytes  5.88 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  28.00-29.00  sec   686 MBytes  5.75 Gbits/sec
[  5][TX-C]  29.00-30.00  sec   702 MBytes  5.89 Gbits/sec    0   2.33 MBytes
[  7][RX-C]  29.00-30.00  sec   687 MBytes  5.76 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID][Role] Interval           Transfer     Bitrate         Retr
[  5][TX-C]   0.00-30.00  sec  20.2 GBytes  5.79 Gbits/sec    0            sender
[  5][TX-C]   0.00-30.00  sec  20.2 GBytes  5.79 Gbits/sec                  receiver
[  7][RX-C]   0.00-30.00  sec  20.2 GBytes  5.78 Gbits/sec  124            sender
[  7][RX-C]   0.00-30.00  sec  20.2 GBytes  5.78 Gbits/sec                  receiver

iperf Done.
```
