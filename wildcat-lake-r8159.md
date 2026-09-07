# Dell XPS 13 - Intel Core 5 320

Note: All tests to AQC107

Note 2: This device achieves nearly 10Gigabit throughput bidirectionally, but seems to struggle slightly.
I'm not sure the cause of this, but it operates fine in the single-direction tests.  My guess is that it
might be due to the speed of the low power cores, but of this I do not have any direct confirmation.

## WisdPi framework module

### dmesg output when device plugged in (Left USB-C port)

```
[   43.641831] usb 2-2: new SuperSpeed Plus Gen 2x2 USB device number 2 using xhci_hcd
[   43.654153] usb 2-2: New USB device found, idVendor=0bda, idProduct=815a, bcdDevice=30.00
[   43.654648] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 0 ep 0x83: setting to 16
[   43.654655] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 1 ep 0x83: setting to 16
[   43.654659] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 2 ep 0x83: setting to 16
[   43.654662] usb 2-2: Int endpoint with wBytesPerInterval of 2 in config 1 interface 0 altsetting 3 ep 0x83: setting to 16
[   43.654897] usb 2-2: Int endpoint with wBytesPerInterval of 8 in config 2 interface 0 altsetting 0 ep 0x83: setting to 16
[   43.655071] usb 2-2: Int endpoint with wBytesPerInterval of 8 in config 3 interface 0 altsetting 0 ep 0x83: setting to 16
[   43.655371] usb 2-2: New USB device strings: Mfr=1, Product=2, SerialNumber=7
[   43.655374] usb 2-2: Product: USB 10/100/1G/2.5G/5G/10G LAN
[   43.655376] usb 2-2: Manufacturer: Realtek
[   43.655378] usb 2-2: SerialNumber: 000334C8D6******
[   43.803192] r8152-cfgselector 2-2: reset SuperSpeed Plus Gen 2x2 USB device number 2 using xhci_hcd
[   43.965847] r8152 2-2:1.0 enp0s13f0u2: renamed from eth0

```

### USB connectivity

Everything here is optimal.  Note that the host speed shows "20000M/x2", and the
device shows "20000M/x2".  This is the best case possible.

### "lsusb -t" relevant output:

```
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 20000M/x2
    |__ Port 002: Dev 002, If 0, Class=Vendor Specific Class, Driver=r8152, 20000M/x2
```

### iperf TCP test, 30 seconds, single stream

```
$ iperf3 -c *** -t 30
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  1.08 GBytes  9.23 Gbits/sec    0   2.23 MBytes
[  5]   1.00-2.00   sec  1.09 GBytes  9.39 Gbits/sec    0   2.23 MBytes
[  5]   2.00-3.00   sec  1.09 GBytes  9.37 Gbits/sec    0   2.38 MBytes
[  5]   3.00-4.00   sec  1.09 GBytes  9.40 Gbits/sec    0   2.53 MBytes
[  5]   4.00-5.00   sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]   5.00-6.00   sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]   6.00-7.00   sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]   7.00-8.00   sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]   8.00-9.00   sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]   9.00-10.00  sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]  10.00-11.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  11.00-12.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  12.00-13.00  sec  1.09 GBytes  9.39 Gbits/sec    0   2.53 MBytes
[  5]  13.00-14.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  14.00-15.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  15.00-16.00  sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]  16.00-17.00  sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]  17.00-18.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  18.00-19.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  19.00-20.00  sec  1.10 GBytes  9.42 Gbits/sec    0   2.53 MBytes
[  5]  20.00-21.00  sec  1.10 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  21.00-22.00  sec  1.09 GBytes  9.41 Gbits/sec    0   2.53 MBytes
[  5]  22.00-23.00  sec  1.10 GBytes  9.41 Gbits/sec    0   3.80 MBytes
[  5]  23.00-24.00  sec  1.09 GBytes  9.40 Gbits/sec    0   3.80 MBytes
[  5]  24.00-25.00  sec  1.10 GBytes  9.41 Gbits/sec    0   3.80 MBytes
[  5]  25.00-26.00  sec  1.10 GBytes  9.42 Gbits/sec    0   3.80 MBytes
[  5]  26.00-27.00  sec  1.10 GBytes  9.41 Gbits/sec    0   3.80 MBytes
[  5]  27.00-28.00  sec  1.09 GBytes  9.40 Gbits/sec    0   3.80 MBytes
[  5]  28.00-29.00  sec  1.09 GBytes  9.40 Gbits/sec    0   3.80 MBytes
[  5]  29.00-30.00  sec  1.10 GBytes  9.41 Gbits/sec    0   3.80 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  32.8 GBytes  9.40 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  32.8 GBytes  9.40 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, reverse direction

```
$ iperf3 -c *** -t 30 -R
Reverse mode, remote host *** is sending
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec  1.05 GBytes  9.03 Gbits/sec
[  5]   1.00-2.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   2.00-3.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   3.00-4.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   4.00-5.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   5.00-6.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   6.00-7.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   7.00-8.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   8.00-9.00   sec  1.07 GBytes  9.22 Gbits/sec
[  5]   9.00-10.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  10.00-11.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  11.00-12.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  12.00-13.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  13.00-14.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  14.00-15.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  15.00-16.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  16.00-17.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  17.00-18.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  18.00-19.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  19.00-20.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  20.00-21.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  21.00-22.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  22.00-23.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  23.00-24.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  24.00-25.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  25.00-26.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  26.00-27.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  27.00-28.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  28.00-29.00  sec  1.07 GBytes  9.22 Gbits/sec
[  5]  29.00-30.00  sec  1.07 GBytes  9.22 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.00  sec  32.2 GBytes  9.22 Gbits/sec    0            sender
[  5]   0.00-30.00  sec  32.2 GBytes  9.22 Gbits/sec                  receiver

iperf Done.
```

### iperf TCP test, 30 seconds, single stream, bidirectional

```
$ iperf3 -c *** -t 30 --bidir
[ ID][Role] Interval           Transfer     Bitrate         Retr  Cwnd
[  5][TX-C]   0.00-1.00   sec   981 MBytes  8.23 Gbits/sec    0   2.72 MBytes
[  7][RX-C]   0.00-1.00   sec   890 MBytes  7.47 Gbits/sec
[  5][TX-C]   1.00-2.00   sec  1.05 GBytes  9.03 Gbits/sec    0   3.36 MBytes
[  7][RX-C]   1.00-2.00   sec  1.02 GBytes  8.80 Gbits/sec
[  5][TX-C]   2.00-3.00   sec  1.05 GBytes  8.98 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   2.00-3.00   sec  1.05 GBytes  8.98 Gbits/sec
[  5][TX-C]   3.00-4.00   sec  1.06 GBytes  9.13 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   3.00-4.00   sec  1.04 GBytes  8.95 Gbits/sec
[  5][TX-C]   4.00-5.00   sec  1.08 GBytes  9.28 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   4.00-5.00   sec  1.05 GBytes  9.04 Gbits/sec
[  5][TX-C]   5.00-6.00   sec  1.09 GBytes  9.34 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   5.00-6.00   sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]   6.00-7.00   sec   993 MBytes  8.33 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   6.00-7.00   sec  1.05 GBytes  8.99 Gbits/sec
[  5][TX-C]   7.00-8.00   sec  1.06 GBytes  9.10 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   7.00-8.00   sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]   8.00-9.00   sec  1.09 GBytes  9.33 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   8.00-9.00   sec  1.07 GBytes  9.18 Gbits/sec
[  5][TX-C]   9.00-10.00  sec  1.08 GBytes  9.24 Gbits/sec    0   3.54 MBytes
[  7][RX-C]   9.00-10.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  10.00-11.00  sec  1.08 GBytes  9.25 Gbits/sec    0   3.54 MBytes
[  7][RX-C]  10.00-11.00  sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]  11.00-12.00  sec  1.08 GBytes  9.26 Gbits/sec    0   3.54 MBytes
[  7][RX-C]  11.00-12.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  12.00-13.00  sec  1.09 GBytes  9.33 Gbits/sec    0   3.54 MBytes
[  7][RX-C]  12.00-13.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  13.00-14.00  sec  1.08 GBytes  9.29 Gbits/sec    0   3.54 MBytes
[  7][RX-C]  13.00-14.00  sec  1.07 GBytes  9.18 Gbits/sec
[  5][TX-C]  14.00-15.00  sec  1.01 GBytes  8.70 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  14.00-15.00  sec  1.07 GBytes  9.15 Gbits/sec
[  5][TX-C]  15.00-16.00  sec   986 MBytes  8.28 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  15.00-16.00  sec  1.06 GBytes  9.11 Gbits/sec
[  5][TX-C]  16.00-17.00  sec  1.08 GBytes  9.24 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  16.00-17.00  sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]  17.00-18.00  sec  1.09 GBytes  9.33 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  17.00-18.00  sec  1.07 GBytes  9.18 Gbits/sec
[  5][TX-C]  18.00-19.00  sec  1.08 GBytes  9.30 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  18.00-19.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  19.00-20.00  sec  1.02 GBytes  8.79 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  19.00-20.00  sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]  20.00-21.00  sec  1.08 GBytes  9.29 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  20.00-21.00  sec  1.07 GBytes  9.18 Gbits/sec
[  5][TX-C]  21.00-22.00  sec  1.08 GBytes  9.25 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  21.00-22.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  22.00-23.00  sec  1.02 GBytes  8.72 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  22.00-23.00  sec  1.06 GBytes  9.10 Gbits/sec
[  5][TX-C]  23.00-24.00  sec  1.08 GBytes  9.25 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  23.00-24.00  sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]  24.00-25.00  sec  1.08 GBytes  9.25 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  24.00-25.00  sec  1.07 GBytes  9.16 Gbits/sec
[  5][TX-C]  25.00-26.00  sec  1.08 GBytes  9.27 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  25.00-26.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  26.00-27.00  sec  1.08 GBytes  9.31 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  26.00-27.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  27.00-28.00  sec  1.08 GBytes  9.27 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  27.00-28.00  sec  1.07 GBytes  9.17 Gbits/sec
[  5][TX-C]  28.00-29.00  sec  1.05 GBytes  9.00 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  28.00-29.00  sec  1.06 GBytes  9.14 Gbits/sec
[  5][TX-C]  29.00-30.00  sec  1.00 GBytes  8.62 Gbits/sec    0   3.72 MBytes
[  7][RX-C]  29.00-30.00  sec  1.05 GBytes  9.06 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID][Role] Interval           Transfer     Bitrate         Retr
[  5][TX-C]   0.00-30.00  sec  31.7 GBytes  9.07 Gbits/sec    0            sender
[  5][TX-C]   0.00-30.00  sec  31.7 GBytes  9.07 Gbits/sec                  receiver
[  7][RX-C]   0.00-30.00  sec  31.7 GBytes  9.07 Gbits/sec    6            sender
[  7][RX-C]   0.00-30.00  sec  31.7 GBytes  9.07 Gbits/sec                  receiver

iperf Done.
```
