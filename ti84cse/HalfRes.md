# Half-res mode on the CSE

Half res mode is an LCD mode which results in a halved horizontal resolution.
This can also be used for double buffering, because one can write to the
left side of the screen while displaying the right side or vice versa.

Entering half-res mode takes 4 steps:
  1. Enable interlacing
  2. Enable partial images 1 and 2
  3. Position the source areas of both partial images on top of each other, and make them 160 pixels in size.
  4. Set the output destinations of the partial images to be 160 pixels apart.

## Enabling Interlacing
To enable interlacing, set bit 10 of LCD register 01h

```
ld a,01h
out (10h),a
out (10h),a
ld a,%00000100  ;bit 10 set
out (11h),a
xor a           ;a = 0 for low bits
out (11h),a
```

To disable interlacing, set LCD register 01h back to 0000h

```
ld a,01h
out (10h),a
out (10h),a
xor a
out (11h),a
out (11h),a
```

## Enable partial images
Partial images are enabled by setting bits 12 and 13 of lcd register
07h for partial images 1 and 2 respectively.

```
ld a,07h
out (10h),a
out (10h),a
ld a,%00110001  ;Enable both partial images
out (11h),a
ld a,%01001100  ;Default values for low bits
out (11h),a
```

To disable, reset bits 12 and 13

```
ld a,07h
out (10h),a
out (10h),a
ld a,%00000001  ;Disable both partial images
out (11h),a
ld a,%01001100  ;Default values for low bits
out (11h),a
```

## Set partial image positions
The partial image display positions are controlled by LCD registers
80h and 83h. Their starting lines are controlled by 81h and 84h, and
their ending lines are controlled by 82h and 85h. When using half-res mode,
set the display position of image 1 to 0, and set the display position
of image 2 to 160.

The start and end lines of both images should be identical.
For example, to display the left half of the screen, set
the start lines to 0 and the end lines to 159. To display
the right half, set the start lines to 160 and the end
lines to 319. In other words, to display a section of the screen starting at
'N', set the start lines to N and the end lines to N + 159.

This code will set up the display positions, and then set
the start and end lines to display the left half of the screen.

```
ld a,80h        ;Img 1 disp position
out (10h),a
out (10h),a
xor a           ;Display position of first img = 0
out (11h),a
out (11h),a

ld a,83h        ;Img 2 disp position
out (10h),a
out (10h),a
xor a           ;MSB should be 0 since 160 < 256
out (11h),a
ld a,160        ;Display position of second img = 160
out (11h),a

ld c,10h        ;Used later to simplify some register setting code

ld a,81h        ;Img 1 start line
out (10h),a
out (10h),a
xor a
out (11h),a
out (11h),a

ld a,84h        ;Img 2 start line
out (10h),a
out (10h),a
xor a
out (11h),a
out (11h),a

ld de, 159      ;End lines for partial images

ld a,82h        ;Img 1 end line
out (10h),a
out (10h),a
out (c),d
out (c),e

ld a, 85h       ;Img 2 end line
out (10h),a
out (10h),a
out (c),d
out (c),e
```
