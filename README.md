# HAB LoRaWAN Transmitter 

Program for loading on to an ESP32 for transmitting telemetry data from a high altitude balloon payload to The Things Network over LoRaWAN.

## Components

Uses an ESP32 microcontroller with various components wired in to transmit telemetry data to The Things Network using LoRa radio. Components include:

- ESP32 microcontroller - main board which sends/receives data between attached components
- LoRa transceiver - sends telemetry data over radio to be received by other LoRa transceivers within range
- SPI connection to second ESP32 module - receive telemetry data from controller ESP32 module

## Receiving from SPI controller ESP32

This is for use with a peripheral ESP32 device. The other ESP32 (controller) is the main board which receives the sensor and telemetry data from components. Once this repo receives the telemetry data over SPI, it proceeds to send that data over LoRaWAN to The Things Network.

## Transmitting to TTN

This repo is a fork from [LMIC-node](https://github.com/lnlp/LMIC-node). Using TTN to track a HAB isn't the most ideal solution because of the fair usage policy limits, however this is very much a secondary method of tracking with very infrequent transmissions. My main transmitter repo for non-LoRaWAN (point to point) LoRa transmissions [can be found here](https://github.com/jaygould/hab-lora-transmitter).

## Additional notes

- The starting example `LMIC-node.cpp` file contains more extraneous/supplementary than I'd like, so it will be good to abstract some of that out to other files, or I may look to find another more stripped down example repo to start with.
- All areas of interest are prefixed with `// * Custom code`.

## Parts of original repo updated

- Added `lorawan-keys.h` file (hidden from repo) which contains TTN keys.
- Updated `LMIC-node.cpp` file to remove all example code I could (the counter related code) and replaced with a SPI peripheral receiver. Received data is sent in uplink.
- Customised `platform.ini` to reflect my ESP32 board and added ESP32 peripheral lib.
- Added `readme.md` file.