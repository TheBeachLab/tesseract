# How to make a solar powered mobile Fab Lab

1. [Introduction](#introduction)
2. [Equipment needed](#equipment-needed)
3. [Calculate your loads](#calculate-your-loads)
4. [Dimension the battery](#dimension-the-battery)
5. [Dimension the solar panel](#dimension-the-solar-panel)
6. [Converting the Equipment from AC to DV](#converting-the-equipment-from-ac-to-dv)
   1. [12V DC](#12v-dc)
   2. [19V DC](#19v-dc)
   3. [24V DC](#24v-dc)
   4. [36V DC](#36v-dc)
   5. [Not yet converted to DC](#not-yet-converted-to-dc)

## Introduction

Outside the atmosphere, the [solar irradiance](https://en.wikipedia.org/wiki/Solar_irradiance) is about 1350 W/m2, that is called the [solar constant](https://en.wikipedia.org/wiki/Solar_constant). This radiation crosses the Earths's atmosphere and finally, down here, it reaches around 1000 W/m2. Now, the exact number depends on the location. The device that measures solar radiation is called [Pyranometer](https://en.wikipedia.org/wiki/Pyranometer). It actually costs a lot of money but you could build one yourself. There are radiation maps where you can also check this data.

Now another factor to consider when designing a solar installation is the peak sun hours in your location and season. Because the sun only gives that much energy during these peak hours. The rest of the hours there is much less energy.

## Equipment needed

You will need:

- A solar panel. You have to get a monocristaline panel. Because they are the most efficient and you are in a reduced space.
- A charge regulator. Get one with LCD. Is you can afford a MPPT, that would be awesome. Mine is a cheap PWM, [this one](https://amzn.to/2HVZ4JF).
- A battery. Get a Full Cycle AGM one. You don't want sulfuric acid leaking inside your car, do you? I got a [small 7Ah battery](https://amzn.to/2Q3coT5) because I just want to use it as a buffer to charge LiPo batteries.
- Optional but recommended. An inverter. If possible make sure it is a pure sinusoidal one and you can connect resistive and inductive loads.

## Calculate your loads

| Load                        | Power | Dayly usage | Total   |
| --------------------------- | ----- | ----------- | ------- |
| Ultimaker 2 3D Printer      | 200W  | 3h          | 600wh   |
| Light                       | 3W    | 2h          | 6Wh     |
| Roland Modela MDX-20        | 40W   | 1h          | 40Wh    |
| Roland GX-24 Vinyl Cutter   | 30W   | 0.5h        | 15Wh    |
| Full Spectrum 5th Gen Laser | 300W* | 1h          | 300 Wh  |
| Oscilloscope                | 30W   | 0.5h        | 15 Wh   |
| Soldering Station           | 40W   | 1h          | 40 Wh   |
| Weller Heat Gun             | 250W  | 0.1h        | 25Wh    |
| Power Supply 30V 5A         | 150W  | 0.2h        | 30Wh    |
| Total                       | 1043W |             | 1071 Wh |

## Dimension the battery

1100 Wh x 1AV/W x 1/12v = 92Ah. Interestingly enough, this is roughly the capacity of the Mercedes G battery. ~~So it might be interesting acquire the same model and have a dual battery system that could act as a back up and also use the solar system to charge the car battery~~. The only question is, would a car battery resist that amount of charge discharge cycles? Answer: No. The crossed out text was a bad idea. Car batteries and solar batteries are very different. 

## Dimension the solar panel

We need to refill this capacity during the sun hours, so, assuming 6 hours of sun: 6h x Power = 1100 Wh. Therefore Power = 185 W. Taking into account unexpected losses I would recommend getting a 200W solar panel.

The next step is to match your dimensional needs to what is possibly available in the market. In my case I would like to use the maximum width of the roof rack, 1.4m.

## Converting the Equipment from AC to DV

### 12V DC

- Fumes absorver. It was converted replacing the 220V AC fan with a 12V DC computer fab
- Soldering Station TS100 (at 12V it draws 17W, takes 40s from 30C to 300C)
- Mavic Pro Drone. It already has a 12V battery charger.
- Kinect 3D Scanner (model 1431, you can see the model number in the power supply). It has a 12V power supply. When you chop the power supply at has 2 wires, one brown (+12V) and one grey (ground). Installed the AUR package libfreenect-git, which also includes the udev rules (restart or reload the udev rules). Current status: not working.
- Dobot Robot Arm (12V 7A 60W)

### 19V DC

- Roland Modela MDX-20 Precision Milling. 
- Soldering Station TS100 (40W, takes 15s from 30C to 300C)

### 24V DC

- Roland GX-24 Vinyl Cutter (tested and also works with 19V)
- Ultimaker 3D printer (in theory also works with 19V). The connector 
- Soldering Station TS100 (65W, takes 11s from 30C to 300C)

### 36V DC

- CNC Machine and Spindle

### Not yet converted to DC

I have a 135W inverter 12VDC to 220VAC for the equipment not yet converted to DC

- LED Loupe Lamp
- Oscilloscope
- Hot glue  60W

Getting a 1500W inverter 12VDC to 110VAC for the following equipment:

- Full Spectrum 5th Gen Laser Cutter. To be modified to [LaserWeb](https://laserweb.yurl.ch)
- Weller Heatgun (currently 110V AC 250W)
