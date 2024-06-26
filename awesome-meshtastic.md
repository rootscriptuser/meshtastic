# BASICS
* LoRa long-range radio protocol
* CSS => chirp spread spectrum modulation
* rebroadcasting messages for forming mesh networks
* license free on EU868 (863–870/873 MHz)
* opensource software/firmware
 
## Protocol stack

### Layer 0 - LoRa radio
`preamble with lenght of 8 + LoRa physical header`

### Layer 1 - Unreliable Zero Hop Messaging

* pack head - dest
* pack head - uniqew sender nodeID
* pack head - unique packet ID
* pack head - head flag
* pack head - channel hash
* pack head - padding mem aligh
* max237 bytes packet data (encrypted)

### Layer 2 - Reliable Zero Hop Messaging
`wantAck`

### Layer 3 - Flooding for multihop Messaging
` depends on SNR `

#### Packet Header Flasgs
|byte|stuff||
|-|-|-|
|1| Hop limit|
|3 |want ack|
|4 | via MQTT|
|5..7 |unused|

# HARDWARE

## ESP32 BASED
* LILYGO TTGO T-Beam
* LILYGO RRGO Lora
* Nano G1
* Station G2
* Heltec V3
* RAK11200

## nRF52
* RAK4631
* LILYGO TTGO T-Echo

## RP2040
* pipico + waveshare lora module
* RAK11310 core module

# FLASHING

[Web Flasher](https://flasher.meshtastic.org/)

# RADIO CONFIG

## Network
`enbale wifi and set SSID && PSK `

## Channels
`you can onyl listen to one frequency slot!? TO-DO`

### Roles
|Role|No.|Description|
|-|-|-|
|PRIMARY | 1 |  only one can exist and periodic broadcast GPS and telemetry only set over this channel | 
|SECONDARY | 2 | can modify PSK |
| DISABLED | 0 | |

### Downlink uplink enable/disable

## Device
> Device Role, Debug Log

### Device Role
* Clinet
* Router (extending network, visible in node list)
* Router-Clinet ( router && client at same time)
* Repeater ( for extending network, not visible in node list)
* Sensor ( telemetry packets as priority)
* Tracker ( GPS packets broadcast as priority)

> Client-Mute && Client-Hidden (lowest power consumption)

#### Rebroadcast mode
* ALL 
* ALL-SKIP-DECODING (only repeater)
* LOCAL-ONLY (rebroadcasts primary /sec channels )
* KNOWN-ONLY (only rebroadcast nodes known list)

## LoRa

* short-fast
* short-slow
* medium-fast
* medium-slow
* long-fast
* long-moderate
* long-slow
* very-long-slow (unreliable, hard to form mesh)

### Badwidth

* 31 kHz
* 62
* 200
* 400
* 800
* 1600 kHz

## Position
in this menu:
* GPS enable
* update interval
* Flags
*  Broadcast interval

# REMOTE NODE ADMINISTRATION

1. config a channel name of `admin`
1. set psk of admin channel
1. nodes only respod to admin command via localUSB/blueooth/TCP interface

# MQTT

1. set passwd for broker
2. set Url/domian for broker
3. set ROOT topic (segmment mesh network with ACL)
4. set encryption enabled
5. set JSON enabled ( not encrypted)
6. set TLS enabled

main stuff to understand:
1. TOPIC => publish/subscribe to a topic from broker
2. CLIENT => meshtastic node
3. BROKER => iot "server" for retransmiting clients messages
4. MQTT=> messaging queue telemetry transport

> meshtastic receives data from its own network and publish them to the broker using mqtt proto
> telemetry data format varies on the information being published


# USEFULL LINKS

* [Offical](https://meshtastic.org/)
* [Reddit](https://www.reddit.com/r/meshtastic/)
* [Discord](https://discord.com/invite/ktMAKGBnBs)
* [Local Groups list](https://github.com/meshtastic/meshtastic/blob/master/docs/community/local-groups.mdx)
* [Remote Admin gist](https://github.com/meshtastic/meshtastic/blob/master/docs/configuration/remote-admin.mdx)
