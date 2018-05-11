# Solar Powered Mobile Fab Lab

## Introduction, skip if you are straight to the point.
Outside the atmosphere, the [solar irradiance](https://en.wikipedia.org/wiki/Solar_irradiance) is about 1350 W/m2, that is called the [solar constant](https://en.wikipedia.org/wiki/Solar_constant). This radiation crosses the Earths's atmosphere and finally it reaches around 1000 W/m2. Now, the exact number depends on the location. The device that measures solar radiation is called [Pyranometer](https://en.wikipedia.org/wiki/Pyranometer). It actually costs a lot of money but you could build one yourself. There are radiation maps where you can also check this data.

Now another factor to consider when designing a solar installation is the peak sun hours in your location and season. Because the sun only gives that much energy during these peak hours. The rest of the hours there is much less energy.

## Equipment needed
You will need:
* A solar panel. You have to get a monocristline panel. Because they are the most efficient and you are in a reduced space.
* A charge regulator. Get one with LCD.
* A battery. Get a gel one. You don't want sulfuric acid leaking in your car, do you?
* An inverter. Make sure it is a sinusoidal one and you can connect resistive and inductive loads.

## Calculate your loads

| Load | Power |
|------------------------|-------|
| Ultimaker 2 3D Printer | 200W |
| Light | 3W |
| Roland Modela MDX-20 | 40W |
| Roland GX-24 Vinyl Cutter | 30W |
| Full Spectrum 5th Gen Laser | 300W* |
| Oscilloscope | 30W |
| Soldering Station | 40W |
| Weller Heat Gun | 250W |
| Power Supply 30V 5A | 150W |
| Total | 1043W |

Simultaneity factor: 60% (the amount of these loads to be considered to be run simultaneously in any given moment). Therefore 600W.

## Dimension the battery
I will assume here that I want to run 24h a 300W load. The battery should be large enough to hold this load during the periods of darkness.

Estimated sun hours: 6h  
Therefore no sun hours: 18h  
18h x 300W = 5400 Wh This is the capacity of the battery.

## Dimension the solar panel
We need to refill this capacity during the sun hours, so: 6h x Power = 5400 Wh. Therefore Power = 900 W

## Matching the requirements with the market and the vehicle
The next step is to adjust your needs to what is possibly available in the market. In my case I need to use the maximum width of the roof rack, 1.4m.


