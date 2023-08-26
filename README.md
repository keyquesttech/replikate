<h1 align="center">Replicate</h1>
<p align="center">
This is a custom "Voron V0" modified to increase the bed size, while keeping the Z height the same.
</p>

<h1 align="center"></h1>

**Why? -** The short answer is because I can, and this is my hobby. However, there are some factual reasons as to why I did it and how I went about it.

**Why even bother if the Z height is the same as a V0?** - Sure, you could simply buy or build one of the official Voron printers if you want a larger device. However, if you already own a V0 or simply wish to print more parts in a single run, this could be for you. Here's a list of reasons to consider:

 - Most of the time, to print more parts, you need more bed space, not height.
 - Splitting parts into multiple smaller parts is an option if you're desperate for Z volume.

**If I have a V0, can I upgrade? -** Realistically speaking, yes, but it's not cheap. Most parts are designed to be printed in [SLS](https://3d.jlcpcb.com/).

<h1 align="center">Electronics:</h1>

**Raspberry Pi 4 - 8GB:** Although you could get away with something less powerful, given that I'm using a Beacon probe and running external code, this seemed like the best option for me.

**Beacon Probe:** For bed leveling, I decided to use a [Beacon](https://beacon3d.com/) probe. Admittedly, a clicky could work, but in the next section, I'll discuss why using Beacon is advised so you can make a decision for yourself. As for me and Replicate, Beacon has sometimes been a pain in the ass, but when it works, it's great.

**3 Stepper Z:** Initially, I wasn't planning to use 3 steppers but instead just the 1 stepper of the stock Voron V0. However, due to the size, thickness, and linear rails used on the V0, the front of the bed sagged around 2mm. This is something the Beacon probe can compensate for, but having the level of detail Beacon provides + 3 steppers is the best-case scenario.

For the 3 steppers, I used the standard [Voron V0 Z stepper](https://www.aliexpress.com/item/1005002583135981.html?spm=a2g0o.productlist.main.13.617b46d7nm4Ql1&algo_pvid=a1e41f05-7cbe-4aa0-80d7-c00650259656&algo_exp_id=a1e41f05-7cbe-4aa0-80d7-c00650259656-6&pdp_npi=4@dis!MXN!1392.81!1239.67!!!81.13!!@2101e9cf16930213250356662e45d0!12000021260524378!sea!MX!0!A&curPageLogUid=cFCSvp7dkpR7). This is one of the reasons why I decided not to increase the volume on Z. Getting a kit from AliExpress or Amazon is much easier than sourcing 3 steppers.  For running those steppers, you can use spare ports on the SKR, use an expander, or a second MCU, as I'll discuss later.

**BIGTREETECH-SKR-mini-E3:** This is what's included in the kit I bought, and the documentation is great. There are also plenty of pins if you run a CAN toolhead.

**Hermit Crab CAN:** Before switching to the HCC, I used an [EBB36](https://biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device?variant=39760665215074) + [U2C](https://github.com/bigtreetech/U2C), but my experience with it was terrible, both in terms of hardware and software. For that reason, and given that I'm constantly changing toolheads or tweaking things for projects such as the [RtV6](https://www.indiegogo.com/projects/rvo-to-v6-adapter-expand-speed-up-cut-costs#/), I decided to try something new. The setup for the HCC was a breeze, and my only issue with it is that the connection to the toolhead is via USB-C and it's located in a terrible spot. So, just keep in mind that you'll have to come up with something to avoid hitting it with the Bowden tube or other cables. That's why the hat on Replicate is so big.

Besides hot-swapping modules, the HCC frees up pins on the SKR. With this setup, you can have essentially 2 "managed" Z steppers and 1 "mirrored," useful if you don't want a second MCU for Z but useless for leveling. Think of it like support for the front of the bed.

Also, keep in mind that the HCC uses a hat for the Raspberry Pi, so you will lose access to some pins and brick your printer if you try to use them or have them in use for something else.

**SKR PICO V1.0:** I wanted 3-stepper bed leveling, more thermistors, and more pins in general, so I added the Pico.

**Bed:** The bed is a custom 200x200mm 120VAC 600W silicone heater with a built-in thermistor and built-in 200°C thermal fuse. Besides the thermistor embedded into the silicone, I've added a threaded thermistor to the build plate, but I'll discuss that in another section. The bed is controlled using an [SSR](https://www.amazon.com/gp/product/B01MCWO35P/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) with [fuses](https://www.amazon.com/gp/product/B075MC6W3P/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) for all 120V lines.

**Boost Fans for Bays:** For the bottom and electronics bay, I used [RC car fans](https://www.amazon.com/gp/product/B08R1D7J4X/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1), 2 for the bottom bay and 1 for the electronics bay as a helper for the main 120mm fan. They're small and powerful, but they are extremely loud and use 8VDC for power. To control these, I used a buck converter and a MOSFET connected to the Pi and power respectively.
