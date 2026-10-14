Schematic · Sheet 1 of 1 · Rev A

# AD624 Pressure Amplifier

A single-ended pressure sensor feeds an AD624 instrumentation amplifier. VAR1 sets the gain, the board runs from ±12 V, and the amplified signal leaves on I/O 3. Redrawn from your hand sketch against the datasheet pinout.

n Numbered amber tags mark where this drawing differs from your sketch. Everything else is drawn as you had it.

## Reading of the sketch

The sensor's SIG line (I/O 1) goes to +IN, pin 2, and the sensor's ground returns to −IN, pin 1, so the amplifier measures SIG relative to the sensor's own ground. VAR1 sits across RG1 and RG2 (pins 16 and 3) and sets the gain. REF (pin 6) is grounded and SENSE (pin 10) is tied to OUT (pin 9), so the output is referenced to ground and leaves on I/O 3. The sensor takes its +12 V from the same supply connector as the amplifier.

## Changes from the sketch

1. 1

   ### Supply pins 7 and 8

   On the AD624, pin 7 is −VS and pin 8 is +VS. In the sketch the two supply wires cross near those pins and I can't tell which rail lands where. Check this before power-up, because reversed rails can destroy the chip.
2. 2

   ### VAR2 wiring

   In the sketch VAR2 runs between +12 V and GND, with its wiper heading toward pin 4. The datasheet's input offset null is a 10 kΩ pot across pins 4 and 5 with the wiper to −VS, so that is how it's drawn here. If you meant VAR2 as a zero adjust that shifts the output, it belongs on REF (pin 6) through an op-amp buffer. REF needs a near-zero source impedance: the datasheet notes that even 1 Ω on REF cuts common-mode rejection to about 80 dB.
3. 3

   ### Decoupling added

   The sketch has none. Put 100 nF ceramic from each supply pin to ground right at U1, plus 10 µF per rail at the supply connector.
4. 4

   ### VAR1 turned to zero

   With VAR1 as a bare rheostat, turning it fully down shorts RG1 to RG2 and the gain runs away, so the output slams into a rail. A fixed resistor in series sets a ceiling: 100 Ω gives a range of about 37 to 401. Size it from your sensor's full-scale signal with the gain check.

## Gain check

VAR1 setting

500 Ω

Series resistor (Ω)

Sensor full scale (mV)

Gain

—

Output at full scale

—

—

—

G = 1 + 40 kΩ / (VAR1 + series R). The internal resistors are only ±20 % absolute, so calibrate against a known pressure. Output swing is taken as ±9 V, a little under the ±10 V the datasheet rates at ±15 V supplies. The 100 mV full scale is an example value; enter your sensor's.

If your sensor already outputs volts (many 3-wire sensors give 0.5–4.5 V or 0–5 V), even VAR1's lowest gain of 41 will saturate the output. Leave pins 3 and 16 open for G = 1, or use a much larger gain resistor.

## U1 pin map

| Pin | Name | Connects to |
| --- | --- | --- |
| 1 | −IN | Sensor GND at J1 pin 3 (ground) |
| 2 | +IN | Sensor SIG, J1 pin 2 |
| 3 | RG2 | RV1 (VAR1), other end |
| 4 | IN NULL | RV2 (VAR2), one end2 |
| 5 | IN NULL | RV2 (VAR2), other end2 |
| 6 | REF | Ground, short and direct |
| 7 | −VS | −12 V, J2 pin 3; C2 to ground1 |
| 8 | +VS | +12 V, J2 pin 1; C1 to ground1 |
| 9 | OUT | J3 pin 1 (VOUT) and pin 10 |
| 10 | SENSE | Pin 9 |
| 11 | G=500 | Not connected |
| 12 | G=200 | Not connected |
| 13 | G=100 | Not connected |
| 14 | OUT NULL | Not connected |
| 15 | OUT NULL | Not connected |
| 16 | RG1 | RV1 (VAR1), one end |

## Parts list

| Ref | Value | Part |
| --- | --- | --- |
| U1 | AD624 | Instrumentation amplifier, 16-pin DIP |
| RV1 | 1 kΩ | VAR1, multiturn trimmer used as a variable resistor |
| RV2 | 10 kΩ | VAR2, trimmer for input offset null |
| C1, C2 | 100 nF | Ceramic, X7R, at U1 supply pins3 |
| C3, C4 | 10 µF | 25 V electrolytic or tantalum, at J23 |
| J1 | 3-pin | I/O 1, pressure sensor: +12 V, SIG, GND |
| J2 | 3-pin | I/O 2, supply: +12 V, 0 V, −12 V |
| J3 | 2-pin | I/O 3, output: VOUT, GND |

Pinout, gain equation, offset-null wiring and REF impedance figures are from the [Analog Devices AD624 datasheet, Rev. C](https://www.analog.com/media/en/technical-documentation/data-sheets/AD624.pdf).