# KCS modem experiment

A circuit intended to turn a modem into a Kansas City Standard-like modem. This is Roy Antaw's fork of [Mr-Bossman/KCS_modem](https://github.com/Mr-Bossman/KCS_modem).

![Schematic](images/KCS_modem.svg)
![Breadboard](images/breadboard.jpg)

## Repository layout

| Location | Purpose |
| --- | --- |
| [board/KCS_modem/](board/KCS_modem/) | KiCad project, schematic and PCB design |
| [images/KCS_modem.pdf](images/KCS_modem.pdf) | PDF schematic |
| [code/KCS_modem.ino](code/KCS_modem.ino) | Arduino/AVR tone-generation sketch |
| [code/send.sh](code/send.sh) / [code/receive.sh](code/receive.sh) | Linux serial send/receive helpers |
| [code/demo.sh](code/demo.sh) | Example session notes, not an unattended setup script |

## Using the files

Inspect the schematic before building or connecting the circuit. Open `board/KCS_modem/KCS_modem.kicad_pro` in a compatible KiCad version. For the sketch, use a matching `KCS_modem` Arduino sketch folder and an AVR target compatible with its direct `PORTB`, `PINC`, `PIND` and timing operations. It is not portable unchanged to ESP32 or other non-AVR boards.

The serial helper scripts use Bash, GNU command-line tools, a `/dev/tty*` device and 115200 baud with hardware flow control. The host-to-modem serial speed is separate from the generated audio signalling rate. Example invocation from the `code` directory:

```bash
bash send.sh /dev/ttyUSB0 your-file.txt
bash receive.sh /dev/ttyUSB0 received-file.txt
```

These are examples for an already connected and configured modem setup, not a guaranteed file-transfer protocol. The receiver writes its destination file and runs until interrupted; it has no documented automatic end-of-file detection. `demo.sh` refers to `lipsum.txt`, which is not supplied: provide your own test file and adapt the commands.

## Status and structure

The code includes experimental timing and a comment that 1200-baud signalling produced too many errors. Compatibility with every modem or the original Kansas City Standard is not established. The hardware/code/images separation is appropriate and retained. No standalone licence file is present; confirm upstream permission before redistributing changes under a new licence.
