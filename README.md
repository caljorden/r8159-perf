# RTL8159 USB 10G ethernet adapter testing with upstream Linux driver (kernel v7.2+)

I have been testing our the 10-gigabit ethernet RTL8159 chipset in a few different adapters on a number of different
systems.  Unfortunately, there is a confusing set of USB standards that make knowing what speed you can get through
these adapters difficult to estimate.  My goal here is to share what I have learned, in the hope that it might be
useful to others.

This information is specific to running the upstream Linux driver that is available in the v7.2+
Linux kernel.  Most of this information is focused on the WisdPi 10G Ethernet expansion card for
Framework devices.  However, there are two additional r8159 devices that are tested on the Framework 13 Pro
laptop (which links to these devices with full capabilities).  Also I have thrown in an Intel Wildcat Lake
laptop to estimate what might be possible with the Framework 12 laptop second generation that is coming out
soon (though for full disclosure, it may not be as capable as the Dell laptop tested here).

## Test systems

* [Framework Desktop - AMD Ryzen AI MAX+ 395](strix-halo-r8159.md)
* [Framework Laptop 13 Pro - Intel Core Ultra 7 358H](ptl-r8159.md)
* [Framework Laptop 13 - AMD Ryzen 7 7840U](phoenix-r8159.md)
* [Framework Laptop 13 - Intel Core Ultra 5 125H](mtl-r8159.md)
* [Dell XPS 13 - Intel Core 5 320 (Wildcat Lake)](wildcat-lake-r8159.md)

## Test RTL8159 devices

* WisdPi 10G Ethernet Expansion Card - for Framework devices
* XikeStor SKN-U310GT (purchased from Amazon.com)
* lidkew Type C to RJ45 with RTL8159 (purchased from Amazon.com)

## Remote endpoint

* Custom-built Ryzen 7 5700X with AQC107 10G PCIe adapter
    * Connected through multiple TRENDnet TEG-S750 switches
* Custom-built Intel Core Ultra 7 270K Plus with RTL8127 10G PCIe adapter
    * Connected through single TRENDnet TEG-S750 switch

## Software environment

* Arch Linux running 7.2.3-arch1-3 on all systems
* iperf3 version 3.21-1 from the Arch Linux repositories
* Linux upstream driver firmware extracted with rtlnic_fw (https://gitlab.com/koblitz-rtlnic/rtlnic_fw)
   * Commit used: 8af3a0324fae40d74e6c4bef0a1409dab01e7c73

# High-level summary

Intel's latest platforms (Panther Lake & Wildcat Lake) appear to have integrated 20000/x2 USB controllers,
and thus pair well with the RTL8159 devices.  At this time, as far as I know, Framework has not yet released
details on the USB capabilities of the Wildcat Lake Framework 12 gen 2 devices.  Thus, it is not known how
well they will pair with the RTL8159 devices.

AMD's previous-gen mobile platform (Phoenix), and current-gen Strix Halo (at least in Framework's implementations)
only have 10000M USB controllers available.  Even so, they can achieve 6.5Gbps to nearly 8Gbps, depending on the
exact device and direction of the traffic (see the device-specific links above for details on what was observed).

Intel's previous-gen platform (Meteor Lake) appears to have the controllers to support 20000/x2, but at least in
Framework's implementation does not expose the full speed to the expansion slots.

As for the RTL8159 devices, the WisdPi 10G framework module is very tiny compared to the other two adapters I
tested.  This makes it ideal for quick 10Gigabit transfers and portability, but it does get very hot quickly.
The other two devices have much larger cases, and thus more area to sink the heat (and have metal bodies).  Thus,
for extended use, I would recommend one of these larger devices rather than the WisdPi 10G module.  All of the
RTL8159 devices I tested appeared to perform the same in my tests (see the Framework 13 Pro link above for details).

## Notice

This information is provided "as is", and with no guarantees as to the accuracy or ability of others to reproduce
what has been gathered here.  I have made my best effort to insure these details are helpful and accurate, but do
not provide any guarantees based on this data.

This information was collected on my personal systems, and was not compensated for in any way by any 3rd party.
This information does not reflect the perspective of any employer past or present, it was gathered on my own time. 
