#Binary coded decimal
One method for display numbers that take more than 16 bits is to convert it to Binary Coded Decimal
first, and display the result. BCD works by using four bits to store each decimal (base 10) digit of
a number. The following code can convert a number to BCD, and display it. It's currently written to
convert a 24 bit number to a 10 digit BCD number, but can be modified to support anything really. It
is memory ineffecient, because it uses one byte for each digit rather than storing two digits per
byte. This is useful though because it makes the display routine simpler.


##Conversion to BCD

This routine converts a little endian value to a little endian BCD value

```z80
;Converts a 24 bit unsigned int pointed to by HL to BCD
;Convert to BCD with double dabble method, see http://en.wikipedia.org/wiki/Double_dabble
;Handles up to a 10 digit number
;Input: HL - pointer to number
;Output: bcdScratch - stores BCD number.
NUM_DIGITS = 10
NUM_SRC_BYTES = 3
.var NUM_DIGITS, bcdScratch
.var NUM_SRC_BYTES, bcdSource
ConvertToBCD:
    ld de,bcdSource
    ld bc,NUM_SRC_BYTES
    ldir
    ld ix,bcdSource

    xor a
    ld hl,bcdScratch
    ld b,NUM_DIGITS
_zeroScratch:
    ld (hl),a
    inc hl
    djnz _zeroScratch

    ld b,NUM_SRC_BYTES * 8
    _bcdConvLp:
        ;Do increment
        ld c,NUM_DIGITS
        ld hl,bcdScratch
        ;Iterate through each BCD digit.
        ;If digit > 4, add 3
        _bcdIncLp:
            ld a,(hl)
            cp 5
            jr c,{@}
            add a,3
            @:
            ld (hl),a
            inc hl
            dec c
            jr nz,_bcdIncLp

        ;Shift SRC bits
        sla (ix)
        .for _off, 1, NUM_SRC_BYTES - 1
            rl (ix + _off)
        .loop

        ld c,NUM_DIGITS
        ld hl,bcdScratch
        _bcdShiftLp:
            ld a,(hl)
            rla
            bit 4,a
            jr z,{@}
            and %1111 ;Mask out high bits, since we only want the lower 4 bits for the digit
            scf       ;Set carry if bit 4 set
            @:
            ld (hl),a
            inc hl
            dec c
            jr nz,_bcdShiftLp
        djnz _bcdConvLp
    ret
```

##Displaying BCD

Displaying BCD is quite simple, since each digit is stored within its own byte. You can simply add
the char code for '0' to the value to get the text char you want. This routine displays an unsigned
BCD value, without leading zeroes

```z80
;Displays the BCD value at HL
;1 byte per digit
NUM_DIGITS = 10
DispBCD:
    ld de,NUM_DIGITS - 1
    add hl,de ;Go to end

    ;Skip leading zeroes, except if the value IS zero
    ld b,NUM_DIGITS - 1
_skipLeadingZeroes:
    ld a,(hl)
    or a
    jr nz,{@}
    dec hl
    djnz _skipLeadingZeroes
@:
    inc b ;B = num digits to display
_dispBCDDigits:
    ld a,(hl)
    add a,'0'
    push hl
    push bc
    ;Replace this with anything that takes a char code in 'A' and displays it
    b_call(_VPutMap)
    pop bc
    pop hl
    dec hl
    djnz _dispBCDDigits
    ret
```
