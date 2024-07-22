# PPSU - Precision Power Supply

This repository is intended as a collection of precision power supplies for analog circuitry and noise sensitive applications, 
such as test and measurement or audio. The general guidelines are:

- Outputs: Bipolar supplies with at least up to +/- 9V and +/- 100mA output capability.
- Inputs: Support one or more common input voltages / USB-C power delivery output voltages (5V,12V,20V).
- Form factor: Compact layout (small current loops) & low height (to add shielding).
- Components: Avoid exotic or hard to solder parts unless mandatory for good implementation.
- PCB: 2 or 4 layer boards, stay within common manufacturing capabilites (no extra charges).

There are a few dual switcher ICs out there that can be applied in this context such as:

- TPS6513x  (2.7V-5.5V Input, f_sw >= 1.15MHz, good for battery or USB powered applications)
- LT8471    (2.4-16V Input, f_sw >= 1MHz, similar to TPS6513x but more versatile and expensive)
- LT8582    (2.5-22V Input, f_sw <= 2.5MHz, very versatile and beefy 3A switches)
- LT8471    (2.6-50V Input, f_sw <= 2MHz, extremely versatile but not quite as beefy as LT8582)

# The Designs

## LT3471 + TPS7A39

LT3471 circuit basically copied from datasheet / evaluation boards. Rev 01 Layout not very optimized.

![IMG_0170](https://github.com/PWieland/PPSU/assets/65927363/a29632f6-3ba1-496c-818b-5c1f025618a1)

Changes for Rev 02:
- Change most 0603 passives to 0402
- Shrink & optimize overall layout
- Make it an easily implemented sub-assembly


## LT8582 + LDOs

LT8582 is a really interesting switcher IC. It features two multitopology DC/DC converters that can each be configured as boost,
SEPIC, inverting or flyback regulators. The package however absoltely requires reflow soldering and to achieve a decent layout, 
extensive use of 0603 or even 0402 passives is as necessary as a 4-Layer PCB. While slightly more challenging to implement properly,
this IC is too interesting to pass on, which is why I have decided to first design a prototype with a combination of Cuk and SEPIC topologies.
With the goal of maximum miniaturization while avoiding 0402 components and maintaining good layout practices, I came up with this 35x35mm PCB:





