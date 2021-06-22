# Roland Modela MDX-20 CNC


<!-- vim-markdown-toc GFM -->

* [Flow control](#flow-control)
* [|DB9  |   DB25|](#db9-----db25)
* [Parts](#parts)

<!-- vim-markdown-toc -->


## Flow control

The Roland modela USB to DB9 cable uses DTR/DSR flow control. But I might have to rewire.

---
|DB9  |   DB25|
---
1    8
2    3
3    14
5    7
6    6
7    4
8    5
9    22

The startech cable does RTS/CTS flow control


http://sgcdn.startech.com/005329/media/sets/ICUSB232_Manual/ICUSB232.pdf

Pin Assignment
1 CD
2 RXD
3 TXD
4 DTR
5 GND
6 DSR
7 RTS
8 CTS
9 RI

and when I see MDX-20 pinout, it's

1: FG
2: TXD
3: RXD
4: RTS
5: CTS
6: DSR 
7: SG
20: DTR

http://support.rolanddga.com/docs/Documents/departments/Technical%20Services/Manuals%20and%20Guides/MDX-20-15_USE_ENGLISH_R5.pdf
(page 69)

For my understanding, shouldn't the pins with same name have to be
connected together?

according to the pinouts  

RS232     Modela    
1 CD    --------- No idea, 20?
2 RXD  --------- 3 RXD
3 TXD  --------- 2 TXD
4 DTR --------- 20 DTR
5 GND -------- 7 SG ?(Ground?)
6 DSR -------- 6 DSR
7 RTS -------- 4 RTS
8 CTS -------- 5 CTS
9 RI

When I see Nadya's instruction(http://wiki.infosyncratic.nl/FabLab)

it's 

1, 8 <-----> 20
   2 <----->  2
   3 <----->  3
   4 <----->  5, 8
   5 <----->  7
   6 <----->  4
   7 <----->  6


---
|DB9  |   DB25 Grey| DB25 Nadya
--- | --- | ---
1  |  8  | 20
2  |  3  | 2
3  |  14 | 3
4  |  20 | 5,8
5  |  7  | 7
6  |  6  | 4
7  |  4  | 6
8  |  5  |20
9  |  22 | none

## Parts

- DRIVE GEAR ASSY MDX-15 7488424000 40,45€
- DRIVE GEAR ASSY 2 MDX-15 7488424100 45,18€



