# PPSU - Precision Power Supply Unit

This repository is intended as a collection of precision power supplies for analog circuitry and noise sensitive applications, 
such as test and measurement or audio. The general guidelines are:

- **Outputs:** Bipolar supplies with at least +/- 9V and +/- 100mA output capability.
- **Inputs:** Support one or more common input voltages / USB-C power delivery output voltages (5V,12V,20V).
- **Form factor:** Compact layout (small current loops) & low height (to add shielding).
- **Components:** Avoid exotic or hard to solder parts unless mandatory for good implementation.
- **PCB:** 2 or 4 layer boards, stay within common manufacturing capabilites (no extra charges).

There are a few dual switcher ICs out there that can be applied in this context such as:

- [TPS6513x](https://www.ti.com/lit/ds/symlink/tps65131.pdf)  (2.7V-5.5V Input, f_sw = 1.25MHz, good for battery or USB powered applications)
- [LT3471](https://www.analog.com/media/en/technical-documentation/data-sheets/3471fb.pdf)    (2.4-16V Input, f_sw = 1.2MHz, similar to TPS6513x but more versatile and expensive)
- [LT8582](https://www.analog.com/media/en/technical-documentation/data-sheets/8582f.pdf)    (2.5-22V Input, f_sw <= 2.5MHz, very versatile and beefy 3A switches)
- [LT8471](https://www.analog.com/media/en/technical-documentation/data-sheets/8471fd.pdf)    (2.6-50V Input, f_sw <= 2MHz, extremely versatile but not quite as beefy as LT8582)

# The Designs

## LT3471 + TPS7A39

[LT3471](https://www.analog.com/media/en/technical-documentation/data-sheets/3471fb.pdf) and [TPS7A39](https://www.ti.com/lit/ds/symlink/tps7a39.pdf) 
circuits are basically copied together from the respective datasheets / evaluation boards.
This project is specifically aimed at replacing dual 9V batteries in portable projects. The idea is to be able to use any USB power bank
that supports USB-PD in a formerly 9V battery powered project while maintaining reasonably low noise and not breaking the bank.
Rev 01 / prototype layout is not very optimized but decent enough for 2 Layers, in general quite easy to implement and promising combo of ICs.
Linear Technology offers their own split-rail LDO LT3032 that similar to TPS7A39, but it has a split thermal pad which can be annoying during assembly.

![IMG_0170](https://github.com/PWieland/PPSU/assets/65927363/a29632f6-3ba1-496c-818b-5c1f025618a1)

Changes for Rev 02:
- Change most 0603 passives to 0402
- Shrink & optimize overall layout
- Make it an easily implemented sub-assembly


## LT8582 + LDOs

[LT8582](https://www.analog.com/media/en/technical-documentation/data-sheets/8582f.pdf) is a really interesting switcher IC. 
It features two multitopology DC/DC converters that can each be configured as boost, SEPIC, inverting or flyback regulators. 
The package however absoltely requires reflow soldering and to achieve a decent layout, 
extensive use of 0603 or even 0402 passives is as necessary as a 4-Layer PCB. While slightly more challenging to implement properly,
this IC is too interesting to pass on, which is why I have decided to first design a prototype with a combination of Cuk and SEPIC topologies.
With the goal of maximum miniaturization while avoiding 0402 components and maintaining good layout practices, I came up with this 35x35mm PCB:

<img width="887" alt="image" src="https://github.com/user-attachments/assets/97d2ef7b-74bf-42d3-8498-ec679b02308f">

It lacks any mounting holes and placing low noise LDOs right next to the inductors would heavily degrade their performance.

## LT8471

On the last page of the [LT8471 datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/8471fd.pdf)
datasheet we find another promising candidate: A combination of ZETA and Cuk converters, both of which are low-noise
due to the second inductor being in series with the output and the general arrangement of switching and energy storage elements in these topologies.

<img width="865" alt="image" src="https://github.com/user-attachments/assets/8e7938b3-6d40-47ef-bd0e-49bc21eff7f3">

I have seen few implementations of this application circuit, but it is next in line after a functional prototype of the LT8582 version is completed.







