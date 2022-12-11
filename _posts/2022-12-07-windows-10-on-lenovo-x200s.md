---
layout: post
title: "Windows 10 on Lenovo X200s"
date: 2022-12-07 17:02:52 +0200
category: notes
tags: windows 10 lenovo x200s fingerprint trackpoint ultranav driver
---

The latest Windows version Lenovo officially supports on one of their first
ultraportables is 7, yet it manages to run Windows 10 relatively well.
Finding (working) drivers can be challenging.

## Microsoft drivers

Windows update contains the latest drivers for battery management service (labeled as
system), graphics, monitor, and TrackPoint.
The latter will only partially function in the updated Metro UI, annoyingly lacking
scrolling support (see [TrackPoint driver](#trackpoint-driver)).

## Lenovo drivers

[Lenovo EOL portal][lenovo-eol-portal] supplies drivers, albeit only for Windows 7.
The following drivers (from the complete [matrix][lenovo-driver-matrix]) are compatible
with Windows 10 (tested with version [20H2][windows-20h2]):

* Intel Chipset Support ([installer][intel-chipset-driver], [read me][intel-chipset-readme])
* Intel AMT 4.2 Management Engine Interface ([installer][intel-amt-driver], [read me][intel-amt-readme])
* Intel Matrix Storage Manager ([installer][intel-storage-driver], [read me][intel-storage-readme])

Intel Turbo Memory driver ([read me][intel-turbo-readme]) may be, and fingerprint
software ([read me][lenovo-fingerprint-readme]) is not compatible with Windows 10.
The Turbo Memory driver will stop the system from booting, likely due to the missing
module.

## Fingerprint reader driver

Surprisingly, the only supported driver for the AuthenTec AES2810 fingerprint reader
compatible with Windows Hello is available from Dell:

* AuthenTec AES2810 Windows Biometric Framework ([installer][dell-fingerprint-driver])

## TrackPoint driver {#trackpoint-driver}

The updated Synaptics UltraNav driver is available only for later X-series models:

* Lenovo TrackPoint ([installer][lenovo-ultranav-driver], [read me][lenovo-ultranav-readme])

Windows will not automatically pick up the updated driver, even if manually selected.
To use the driver, launch the self-extracting archive and unpack its contents.
Then, locate the driver installer executable `dpinst.exe`, typically in
`C:\DRIVERS\WIN\UNAV\WinWDF\x64` or `x86`.
Launch the installer and let it finish.

Locate “PS/2 TrackPoint” in Device Manager, right-click and select device “Properties”;
then click “Update Driver” from the “Driver” tab.
Choose "Browse my computer for drivers" and then "Let me pick from a list of
available drivers on my computer.
Uncheck "Show compatible hardware" and select Lenovo Synaptics Pointing Device.
Ignore compatibility warnings, install the driver, and restart.

Scrolling should work now without further configuration.

[dell-fingerprint-driver]: https://dl.dell.com/FOLDER01134387M/4/AES2810_WBF_Setup_A01_64bit_ZPE.exe
[intel-amt-driver]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/7vr308ww.exe
[intel-amt-readme]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/7vr308ww.txt
[intel-chipset-driver]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/g1ic09ww.exe
[intel-chipset-readme]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/g1ic09ww.txt
[intel-storage-driver]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/6iio10ww.exe
[intel-storage-readme]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/6iio10ww.txt
[intel-turbo-readme]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/7zin85ww.txt
[lenovo-eol-portal]: https://download.lenovo.com/eol/index.html
[lenovo-driver-matrix]: https://download.lenovo.com/lenovo/content/ddfm/X200s.html
[lenovo-fingerprint-readme]: https://download.lenovo.com/ibmdl/pub/pc/pccbbs/thinkvantage_en/lfs33250w764.txt
[lenovo-ultranav-driver]: https://download.lenovo.com/pccbbs/mobiles/gggr07ww.exe
[lenovo-ultranav-readme]: https://download.lenovo.com/pccbbs/mobiles/gggr07ww.txt
[windows-20h2]: https://docs.microsoft.com/en-us/windows/release-information/status-windows-10-20h2
