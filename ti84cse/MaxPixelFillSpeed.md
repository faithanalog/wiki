#Max pixel fill speed with OTIR

One of the fastest practical ways to write arbitrary pixels (no 1-color rectangles)
to the LCD is with an OTIR loop copying pixel data directly from memory.
That being said, I was wondering how many pixels you could theoretically
update per frame. As mentioned, this is theoretical. This does not take
into account the overhead of adjusting the LCD window, or any of the other
logic you may have. It also assumes that interrupts are disabled.

##The code

The code I'll be using to calculate max fill rate is

```z80
;Input: HL = Amount of pixels to output
;            Generally this would be width * height
;            This means that HL can never be the size of the ENTIRE screen,
;            just 85.3% of it. Normally you'ld be in half-res mode though.

    ld b,l

;If B != 0, we need an extra iteration
    ld a,b
    or a
    jr z,$+3
    inc h

_dispSprtLp:
    otir
    dec h
    jp nz,_dispSprtLp
```

I use JP in the loop to save a few extra cycles. When calculating the
numbers below, I'm basing it only on the runtime of the loop,
and I'm not calculating the negligible setup time for the loop.

##The numbers
The TI-84+CSE uses a z80 processor, which can be set to run at 15Mhz.
This means that it has about 15,000,000 cycles (or T-States) per second. All
instructions take more than one T-State to run. The ones we care about are:

`OTIR: (21 * (B - 1)) + 16` If `B == 0`, evaluate `B - 1` as `255`

`DEC H: 4`

`JP nz, ADDR: 10`

Based on those numbers, we can calculate the amount of T-states for any given
input of HL

When B = 0, the loop takes (21 * 255 + 16) + 4 + 10 T-States, or 5385.
Therefore if L == 0

`f(H,0) = 5385 * H`

Otherwise if L > 0

`f(H,L) = ((21 * (L - 1)) + 30) + 5385 * H`


To simplify calculations, I'm going to ignore the fact that 'H' can not be
greater than 255. This allows me to use the above equation for the dimensions
of the entire screen, and get a reasonably close estimate of how much time it
would take.

##The calculations
The screen is 320x240 pixels large. 320 * 240 = 76800. 76800 / 256 = 300, so
H = 300 and L = 0. 300 * 5385 = 1,615,500.

To update the entire screen with this method it takes
1.077 seconds. Not very promising, but here's a table of screen percentages
vs how much time it takes to update. For any dimensions that you want to calculate
yourself, the simplest way would be to use this formula.

`(WIDTH * HEIGHT) / (320 * 240) * 1615500`

Divide 1,500,000 by the result to get framerate.

Percent of Screen | T-states  | Theoretical Frames/Second | Dimensions
----------------- | --------  | ------------------------- | ----------
100%              | 1,615,500 | 0.93 FPS                  | 320 x 240
50%               | 807,750   | 1.86 FPS                  | 160 x 240 (Half Res)
5.3%              | 86,160    | 17.41 FPS                 | 64 x 64 (Large sprite)
2.7%              | 43,080    | 34.8 FPS                  | 32 x 64 (Large sprite Half Res)
