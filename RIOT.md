# Setting up RIOT and MQTTSN

1. Clone `RIOT` repository
2. Setup `RIOTBASE ?= ...` into `Makefile`

## Setup 
```s
cd device/riot/sensors_mqttsn
./start_network.sh
```

## Usage
```s
PORT=tap0 make clean all term
```
- To connect to a broker, use the `con` command:
On `riot-shell`:
```s
ifconfig 5 add fec0:affe::99
con fec0:affe::1 1885
set_device "Device Piano"
pub_telemetry
```


### Other utilities
```s
sudo netstat -ltup
mosquitto_pub -d -h "127.0.0.1" -t "v1/devices/me/telemetry" -u "$ACCESS_TOKEN" -f "telemetry-data-as-object.json"
```

Into RIOT shell:
```s
pub v1/gateway/telemetry "{ 'Device Piano': [ { 'ts': 1585744760000, 'values':{'humidity': 42 }}]}" 1
```

# IoT-LAB

1. Register to IoT-Lab. (*Replace*  `colasant` *with your iot-lab username*) 
2. Configure SSH Access [link](https://www.iot-lab.info/tutorials/ssh-access/). Just create a pair key and copy your public key into your IoT-lab profile.
3. Follow this [tutorial (riot-compilation)](https://www.iot-lab.info/tutorials/riot-compilation/)

My SSH credential is: 
```s
ssh colasant@grenoble.iot-lab.info
```
To build: *(into your SSH remote connection, after have configured as (3))*
```sh
source /opt/riot.source
BOARD=iotlab-m3 make all
```

## IoT-LAB Networking example for M3 Nodes
1. Connect to SSH
2. Compible the firmware in remote (in your SSH connection)
3. Copy the remote elf into your local pc. 
```s
scp colasant@grenoble.iot-lab.info:iot-lab/parts/RIOT/examples/gnrc_networking/bin/iotlab-m3/gnrc_networking.elf gnrc_networking.elf
```


# Issues
Errors:
SSH config:
```s
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```