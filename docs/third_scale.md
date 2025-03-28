---
layout: default
title: Third-Scale Vehicle
---

# Third-Scale Vehicle


## Drive-by-Wire Retrofit

### Force measurements

The following measurements were taken to determine design specifications for the motors used for steer and brake by-wire. These were performed with the incredibly sophisticated equipment of a luggage scale.
* 7kg measured to turn the steering wheel. Measured perpendicular to the radius of the steering wheel at a distance of 3in from the center. This results in (7kg)(9.8m/s/s)(0.08m) = (68.6N)(0.08m) = 5.5 Nm of torque.
* 35kg measured to rotate (apply) the brake. Measured at the small metal plate at a radius of 1.5in. This results in (35kg)(9.8m/s/s)(0.038m) = 13 Nm of torque.
* 14kg measured to rotate (apply) the brake. Measured on the metal tubing extending from the brake pedal, at a radius of 4in. This results in (14kg)(9.8m/s/s)(0.1m) = 13.7 Nm of torque.
Since the last two measurements corroborate each other, the torque specification for the motor for brake-by-wire is set to 14 Nm.

### Motor Selection

### Motor Mounts

There are two motors mounts in this prototype. 

The first is the Brake Motor which is mounted beneath the toy car. This motor is mounted with a xft by yft hard aluminum plate and is screwed in place. This placement was used because the motor is as close to the top of the car and does not extend out of the lowest part of the car, so there is no risk of the motor being damaged. This placement also allowed for the mount to be supported by the existing shaft on the vehicle and dont add much weight compared to using the extrusion shafts.

## Power and Electrical

Based on the Battery selected being 51.2V with a 30 amp per hour output the gauge wires needed to be changed to a 0 gauge wire. The calculation used to do this can be seen below:
1. Calculate the Voltage Drop Index (VDI) using VDI = (Amps x Feet)/(% Voltage Drop x Voltage)
* Amps = amp-hours divided by the number of hours running
  The battery runs on 30 ah and arbitrarily choosing one hour will lead to -> 30 ah/ 1 hour = 30 amps
* Feet = One-way wire distance
  Measuring the length between the electronics and battery using a measuring tape the distance is about 2ft. Now adding .5ft   for any othe connections to other electronics that may be necessary.
* % Voltage Drop = percentage of voltage drop acceptable for this circuit (tpically 2 - 5%)
  
The equation looked like this for this poroject's use case:
VDI = 48.82 = (30amps x 2.5ft)/(3% x 51.2v)
 
 2. Since the VDI number did not match exactly to a VDI number already on the chart, This calls for rounding the value up to the next nearest one which is a VDI number of 49 and this ties to a wire gauge of 0 for a copper wire. The gauge size and VDI number will be different for different materials of wire.


### Electronics Voltage Needs

* [Victron Energy Orion DC-DC Converter 48V>>24V](https://www.amazon.com/Victron-Energy-Orion-Tr-380-Watt-Converter/dp/B07DPZ9G7M) - rated up to 16A (380W) and accepts voltages between 32-70V.
* [Victron Energy Orion DC-DC Converter 48V>>12V](https://www.amazon.com/Victron-Orion-TR-DC-DC-Converter-Isolated/dp/B07DQ5H3T2) - rated up to 30A (360W) and accepts voltages between 32-70V.
* The [Flipsky-75100-pro VESC motor controller board](https://flipsky.net/products/flipsky-75100-pro-with-aluminum-pcb-based-on-vesc-for-electric-skateboard-scooter-ebike-speed-controller) accepts voltages between 14-84V. We had considered the [TRAMPA VESC 100V 250A](https://trampaboards.com/vesc-100v-250a-in-cnc-t6-silicone-sealed-aluminum-box--p-28113.html) that is a bit more capable, but we did not need that extra capability and it would be harder to order.
* The [Onlogic Karbon 804, On Board Computer (OBC)](https://www.onlogic.com/k804/) accepts voltages between 12-48V.
* The [Docyne motor](https://www.docyke.com/products/servo-motor) accepts voltages between 12-24V.
* The NVIDIA Orin accepts voltages between 7-20V.
* The LIDAR operates on PoE sourced from the OBC.
* The ZED cameras operate on GMSL connections from the NVIDIA Orin.

### Power Requirements

* The stock motor pulls 16A at 24V, leading to 16*24= **384W**
* The Docyne motor (throttle) is 5A at 18V --> 5*18 = **90W**
* The Docyne motor (brake) is also **90W** (although used much less frequently)
* The On Board Computer (OBC) uses **65W**
* The NVIDIA Orin + ZED cameras use roughly **100W** (?check this empirically?)

These power needs **sum to 729W** (Watts).  This informs the capacity of the battery we select (in Amp-Hours, Ah) based on the length of time we wish to operate the vehicle.

### Battery Selection

There is a benefit to selecting a higher voltage battery largely because it enables faster speeds, by driving the stock drive motor at a higher voltage.  There are also DC-DC step down converters that can be used to provide lower voltages for the electronics onboard. Our battery selection considers the following criteria:

* Voltage greater than 24V
* [Hobbyists](https://www.youtube.com/@ExtremePowerWheels/videos) have demonstrated that the stock motor can handle at least up to 75V and maybe 92.5V.  So we aim for a voltage less than 75V.
* The vehicle should be able to run continuously for 2 hours.

We found cost effective batteries typically used for golf carts at 48V.  Li Time sells a [48V 30Ah LiFePO Battery](https://www.litime.com/products/litime-48v-30ah-gc2-golf-cart-lithium-battery-gc2-battery-for-club-cart-golf-cart) that has bluetooth connectivity for diagnostics.  The nominal voltage is actually 51.2V, so a step-down converter may be needed for the OBC.

Given the 48V, assuming no losses in the DC-DC conversion, the current draw would be 729W/48V = 15.2A (amps). Rounding this up to 16A to include losses, a 16Ah = 16000mAh battery would last 1 hour of operation and a 32Ah battery would last 2 hours. Thus the 30Ah battery should last roughly 2 hours.

## Sensor Mounts


## Component information:

### Ignition Control Relay
Littelfuse DCNLM100NB12-01

DCNLM 100A 48V NP 12Vcoil DC | Series: DCNLM

[DATASHEET](https://www.littelfuse.com/products/relays-contactors-transformers/high-voltage-dc-contactor-relays/dcnlm/dcnlm100nb12-01)

The DCNLM Series 60V High-Current DC Contactor Relay features 100A contact switching capability with a 12V coil rating, which is suitable for a wide variety of applications, including use in electrical control systems, communication power supplies, engineering machines, and uninterruptible power supplies (UPS).

This configuration of the DCNLM normally open, high-current DC contactor (DCNLM100NB12-01) features 60V non-polarized main contacts and a dual-coil design.

* Current Rating (Continuous) in Amps: 100
* Current Rating (inrush) in Amps: 400A 5ms
* Voltage Rating (V): 60
* Circuitry: SPST NO
* Ingress Protection: IP4X
* Input Terminals: M6 Bolt
* Output Terminals: M6 Bolt
* Contacts: Silver alloy contact
* Normal Position: Normally Open
* Hardware: M6 Nuts
* Housing: Metal
* Mounting Method: SIDE MOUNT
* Recommended Torque: 4-6 N.M
* Agency Approval - Shock: DCNLM50NB DVP 50G, 6ms
* Agency Approval - Vibration: 1~500Hz, About 1G, 8h/axis
* Temperature Maximum (°C): 70
* Temperature Minimum (°C): -40
* Temperature Maximum (°F): 158
* Temperature Minimum (°F): -40
* Aux Contacts: No
* Coil Type: Dual
* Agency Approval - Humidity: 20%~90% RH
* Polarized: No
* Coil Voltage: 12

### 12V Battery for Ignition Control of Relay
Rapthor Portable 12V 2600mAh Rechargeable Battery Pack with Charger and DIY cable
[Amazon Link](https://www.amazon.com/dp/B0D9D5L3B5?ref=ppx_yo2ov_dt_b_fed_asin_title)

This portable 2600mAh lithium ion battery pack with DC 9.0-12.6V/3A (Max) output, the input is DC12.6V/1A. It comes with 12.6V/1A Charger, DC power connector and DC power pigtail cable, great choice to do the DIY projects.

Compatible with CCTV camera, IP camera, LED panel, amplifier, modem, walkie-talkies, camcorders, Bluetooth devices, aviation models, LED strip, electronic piano, optical network unit, router, small Bluetooth amp, electric scooter 12V turn signals, car DVR etc.

Buck-boost converter protects against overheating. Battery Management System (BMS) prevents over discharge. Microcontroller (MCU) offers short circuit protection.

Premium lithium-ion batteries with over 800 times charge-discharge cycles without memory effect.

**Battery Pack Specifications:**
* Battery Type: Lithium ion
* Capacity: 2600mAh.
* Input: DC12.6V/1A.
* Output: DC 9.0-12.6V /3A (Max).

**Charger Specifications**
* Input: 100-240V-50/60Hz 0.8A.
* Output: 12.6V /1A.

**Package Includes**
* 1x Llithium ion battery pack
* 1x Charger
* 1x DC power connector
* 1x DC power pigtail cable
* 1x User Manual

**NOTES**
No long-term placement in a low voltage state. In order to extend the battery life, it's suggested charge every three months if long term storage.
