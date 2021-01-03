# gRPC on FPGA

Implement an overlay to offload computation to the PYNQ FPGA using gRPC

Github repository is available [here](https://github.com/nimashoghi/matmult).

## Motivation

The goal of this project is to deploy an FPGA in a distributed robotic system. The system will run load intensive algorithms (such as SLAM) on the robots, which offload resource intensive computation onto the integrated FPGA. 

## Code Description

The project [repository](https://github.com/nimashoghi/matmult) contains the HLS files along with the build instructions found in `boards/Pynq-Z1/matmult/README.md`. 

The overlay contains the built files from HLS. 

The service is the contained in `server.py` and `client.py` and must be run respectively on the PYNQ board and Raspberry Pi. 


## Project Setup

### Installing Vivado

Vivado must be run on Ubuntu and can be downloaded [here](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/2019-2.html). Follow this [tutorial](https://www.youtube.com/watch?v=3L0baY-DA3c) to install Vivado.  

### Building Overlay

These instructions found in `boards/Pynq-Z1/matmult/README.md` build the `matmult.bit`, `matmult.tcl`, and `matmult.hwc` and must be transferred to to the `https://github.com/nimashoghi/matmult/tree/master/overlay/matmult`. 

### Pynq Board

Clone the repository onto the PYNQ board. Make sure that the overlay folder has updated files from the previous step. This will serve as the server.

### Raspberry Pi

Clone the repository onto a device on the same network as the Pynq board. The Pi will serve as the client.

## Execution

Install python3 and the following python modules on the server and client

```
pip3 install grpcio
pip3 install grpcio-tools
pip3 install protobuf
```

Run the server on the Pynq through `sudo python3 server.py` and the client in the Raspberry Pi `python3 client.py <ip:port>`.