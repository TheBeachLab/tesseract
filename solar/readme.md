# Solar Powered Mobile Fab Lab

## Introduction
Outside the atmosphere, the [solar irradiance](https://en.wikipedia.org/wiki/Solar_irradiance) is about 1350 W/m2, that is called the [solar constant](https://en.wikipedia.org/wiki/Solar_constant). This radiation crosses the Earths's atmosphere and finally, down here, it reaches around 1000 W/m2. Now, the exact number depends on the location. The device that measures solar radiation is called [Pyranometer](https://en.wikipedia.org/wiki/Pyranometer). It actually costs a lot of money but you could build one yourself. There are radiation maps where you can also check this data.

Now another factor to consider when designing a solar installation is the peak sun hours in your location and season. Because the sun only gives that much energy during these peak hours. The rest of the hours there is much less energy.

## Equipment needed
You will need:
* A solar panel. You have to get a monocristline panel. Because they are the most efficient and you are in a reduced space.
* A charge regulator. Get one with LCD.
* A battery. Get a gel one. You don't want sulfuric acid leaking in your car, do you?
* An inverter. Make sure it is a sinusoidal one and you can connect resistive and inductive loads.

## Calculate your loads

| Load | Power | Dayly usage | Total |
|------------------------|-------| ---| ---|
| Ultimaker 2 3D Printer | 200W | 3h | 600wh
| Light | 3W | 2h | 6Wh
| Roland Modela MDX-20 | 40W | 1h | 40Wh
| Roland GX-24 Vinyl Cutter | 30W | 0.5h | 15Wh
| Full Spectrum 5th Gen Laser | 300W* | 1h | 300 Wh
| Oscilloscope | 30W | 0.5h | 15 Wh
| Soldering Station | 40W | 1h | 40 Wh
| Weller Heat Gun | 250W | 0.1h | 25Wh
| Power Supply 30V 5A | 150W | 0.2h | 30Wh
| Total | 1043W |  | 1071 Wh

## Dimension the battery
1100 Wh x 1AV/W x 1/12v = 92Ah. Interestingly enough, this is roughly the capacity of the Mercedes G battery. So it might be interesting acquire the same model and have a dual battery system that could act as a back up and also use the solar system to charge the car battery. The only question is, would a car battery resist that amount of charge discharge cycles? I keep a note for looking up for this information.

## Dimension the solar panel
We need to refill this capacity during the sun hours, so, assuming 6 hours of sun: 6h x Power = 1100 Wh. Therefore Power = 185 W. Taking into account unexpected losses I would recommend getting a 200W solar panel.

## Matching the requirements with the market and the vehicle
The next step is to adjust your needs to what is possibly available in the market. In my case I need to use the maximum width of the roof rack, 1.4m.


