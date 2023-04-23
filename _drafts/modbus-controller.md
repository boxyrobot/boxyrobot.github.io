---
layout: post
title: "Komfovent ModBus controller using Raspberry Pi"
date: 2023-04-23 13:29:51 +0200
category: projects
tags: komfovent modbus raspberry-pi
---

## Stacking modules

The target is to have controller running on the power over Ethernet (PoE) which means stacking two HATs:

* Raspberry Pi PoE+ HAT
* WaveShare 2-channel RS485 HAT

The PoE HAT has only 2.5 mm offsets bundled.
Once installed over the Raspberry Pi, the GPIO header pins are no longer usable.
Pin header extension is needed to use additional HATs on the same board.

RS485 HAT comes with a pin header extension and a set of 2.5 mm offsets that are sized for installation on top of the Raspberry Pi.
The size of the extension bundled with the RS485 HAT is a perfect fit -- base height 8.5 mm, pin length ca. 11.5 mm.

The case needs two 10 mm extensions to house both HATs.

### Missing parts

- [ ] Pin header extender
- [ ] Another 10 mm case extender
