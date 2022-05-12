# minim
A playable chord sequencer and arpeggiator for Monome Teletype and Monome Grid

Tutorial: https://youtu.be/1SCG_FcJc24

To load onto Teletype, download the .txt file, rename to the scene slot you wish to overwrite (e.g. tt07.txt) and drop on a thumb drive. Insert into Teletype and commence jams.

TELETYPE I/O:
- LEFT SIDE: CHORD SEQ
- CENTER: SET LOOP START+END (USE 2 FINGERS TO SET)
- RIGHT SIDE: ARP SEQ
- IN 1: ADVANCE CHORD
- IN 2: RESET ARP
- IN 3: ADVANCE ARP
- CV IN: CHORD SPREAD/VOICING
- PARAM KNOB: SCALE
- TR 1: CHORD TRIGGER
- TR 2: LIVE CHORD TRIGGER
- TR 3: ARP TRIGGER
- TR 4: LIVE ARP TRIGGER
- CV 1-3: CHORD
- CV 4: ARP

SCALES:
- 0-major
- 1-natural-minor
- 2-harmonic-minor
- 3-melodic-minor
- 4-dorian	
- 5-phrygian
- 6-lydian
- 7-mixolydian
- 8-locrian

SCRIPT NOTES:
- $ 1 Triggers chord sequence advancing, CV and TR out
- $ 2 Spread/voicing algo for chord CV, triggers reset of arp section
- $ 3 Triggers arp sequence advancing, CV and TR out
- $ 4 Handler for sequence advancing (P.NEXT, reset, setting loop start/PN.L)
- $ 5 Sets dim previous/reset loop button LEDs
- $ 6 Looper column button handler
- $ 7 Sets loop variables post-handler
- $ 8 Sequence button handler (including live play triggering)

VARIABLES:
- A Enable Chord P.NEXT
- B Enable Seq P.NEXT
- C Current Chord
- D Local var for $ 8, + Init (via Metro)
- X Loop BTN GRPI (8/9), + Init (via Metro)
- Y Loop BTN -8 (0/1)
- Z Indicates Chord/Arp (0/1) when calling $ 4
- T Local var for $ 3
- R IN + modifiers
- PRT 7 Metro/Init
- PRT 8 PRM/Scale
- PRT 9 Raw IN/CV

PATTERN VARIABLES:
|  P | Section | PN 3                 | From 1/0 (Z/Y) | From 8/9 (X) | Note      |
|----|---------|----------------------|----------------|--------------|-----------|
|  0 | Chord   | Current Start        | Z/Y            | - X 8        |           |
|  1 | Arp     | Current Start        | Z/Y            | - X 8        |           |
|  2 | Chord   | Current Loop Length  | + Z/Y 2        | - X 6        | 0 indexed |
|  3 | Arp     | Current Loop Length  | + Z/Y 2        | - X 6        | 0 indexed |
|  4 | Chord   | Pending Start        | + Z/Y 4        | - X 4        |           |
|  5 | Arp     | Pending Start        | + Z/Y 4        | - X 4        |           |
|  6 | Chord   | Pending Loop Length  | + Z/Y 6        | - X 2        |           |
|  7 | Arp     | Pending Loop Length  | + Z/Y 6        | - X 2        |           |
|  8 | Chord   | Previous Loop Length | + Z/Y 8        | X            |           |
|  9 | Arp     | Previous Loop Length | + Z/Y 8        | X            |           |
| 10 | Chord   | Looper G.BTN.C       | + Z/Y 10       | + X 2        |           |
| 11 | Arp     | Looper G.BTN.C       | + Z/Y 10       | + X 2        |           |
| 12 | Chord   | Loop state           | + Z/Y 12       | + X 4        |           |
| 13 | Arp     | Loop state           | + Z/Y 12       | + X 4        |           |
| 14 | Chord   | Reset State          | + Z/Y 14       | + X 6        |           |
| 15 | Arp     | Reset State          | + Z/Y 14       | + X 6        |           |

RESET LOGIC FLOW:
![Minim reset logic flow](https://user-images.githubusercontent.com/435570/168101025-a86ee025-c8e6-416e-b1e6-7aa585dda051.svg)
