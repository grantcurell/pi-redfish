## hub-ctrl

Control USB power on a port by port basis on some USB hubs.

This only works on USB hubs that have the hardware necessary to allow software controlled power switching. Most hubs DO NOT include the hardware.

https://github.com/codazoda/hub-ctrl.c#controlling-power

    echo "sudo ./hub-ctrl -h 0 -P 1 -p 0" >> /dev/ttyUSB0

Found this in `resetPi0HID.sh`. This means hub 0, port 1, turn power off. `p 1` would turn it back on.

### Pi Zero vs Pi 4

From https://gist.github.com/gbaman/50b6cca61dd1c3f88f41. 

The Pi4 has a USB hub whereas in the Pi0 the USB port is connected directly to the proc.

## checkPi0Login.sh

This seems to be responsible for logging into the pi 0 and can also run a command on it.

## RPi.GPIO

This let's you use Python to control the GPIO on a Raspberry Pi.

### Pin Numbering

There are two ways of numbering the IO pins on a Raspberry Pi within RPi.GPIO. The first is using the BOARD numbering system. This refers to the pin numbers on the P1 header of the Raspberry Pi board. The advantage of using this numbering system is that your hardware will always work, regardless of the board revision of the RPi. You will not need to rewire your connector or change your code.

The second numbering system is the BCM numbers. This is a lower level way of working - it refers to the channel numbers on the Broadcom SOC. You have to always work with a diagram of which channel number goes to which pin on the RPi board. Your script could break between revisions of Raspberry Pi boards.

To specify which you are using using (mandatory):

    GPIO.setmode(GPIO.BOARD)
    # or
    GPIO.setmode(GPIO.BCM)

### Setup a Channel

You need to set up every channel you are using as an input or an output. To configure a channel as an input:

    GPIO.setup(channel, GPIO.IN)

(where channel is the channel number based on the numbering system you have specified (BOARD or BCM)).

More advanced information about setting up input channels can be found here.

To set up a channel as an output:

    GPIO.setup(channel, GPIO.OUT)

(where channel is the channel number based on the numbering system you have specified (BOARD or BCM)).

You can also specify an initial value for your output channel:

    GPIO.setup(channel, GPIO.OUT, initial=GPIO.HIGH)

### Output

To set the output state of a GPIO pin:

    GPIO.output(channel, state)

(where channel is the channel number based on the numbering system you have specified (BOARD or BCM)).

State can be 0 / GPIO.LOW / False or 1 / GPIO.HIGH / True.

## uart (universal asynchronous receiver/transmitter)

UART stands for Universal Asynchronous Receiver/Transmitter. It’s not a communication protocol like SPI and I2C, but a physical circuit in a microcontroller, or a stand-alone IC. A UART’s main purpose is to transmit and receive serial data.

One of the best things about UART is that it only uses two wires to transmit data between devices. 

https://www.circuitbasics.com/basics-uart-communication/

## SPI




## avconv

https://libav.org/avconv.html

avconv is a very fast video and audio converter that can also grab from a live audio/video source. It can also convert between arbitrary sample rates and resize video on the fly with a high quality polyphase filter.

In `image.php`:

    system("avconv -f video4linux2 -i ". $_GET['vid'] ." -vframes 1 -s 720x480 -v quiet -y ". $filename);

    ‘-f fmt (input/output)’
    Force input or output file format. The format is normally autodetected for input files and guessed from file extension for output files, so this option is not needed in most cases.

    ‘-vframes number (output)’
        Set the number of video frames to record. This is an obsolete alias for -frames:v, which you should use instead.

    ‘-s[:stream_specifier] size (input/output,per-stream)’
        Set frame size.

        As an input option, this is a shortcut for the ‘video_size’ private option, recognized by some demuxers for which the frame size is either not stored in the file or is configurable – e.g. raw video or video grabbers.

        As an output option, this inserts the scale video filter to the end of the corresponding filtergraph. Please use the scale filter directly to insert it at the beginning or some other place.

        The format is ‘wxh’ (default - same as source). The following abbreviations are recognized:

    ‘-y (global)’
        Overwrite output files without asking.

    ‘-i filename (input)’
        input file name

## dtoverlay=dwc2

Maybe helpful - I don't really understand: https://raspberrypi.stackexchange.com/questions/77059/what-does-dtoverlay-dwc2-really-do/77061

## Random

OTG = (USB) on the go

What does VCC mean?
- Something to do with the GPIO to relay