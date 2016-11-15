# TwinCAT ADS
This is an example of communication between different PC through TwinCAT ADS.
The idea is to let the TwinCAT in one PC to access the PLC variable of the TwinCAT in another PC.


![alt tag](https://puu.sh/siywA/5124e30c04.png)


## Usage

1. Run the TwinCAT program inside the "First PC" folder in the first PC
2. Run the TwinCAT program inside the "Second PC" folder in the first PC


## How it works

What's happening inside the program:

1. Inside the "First PC", there's a structure called "ST_Record" consisting of three arrays of 100,000 DWORD objects. Inside the MAIN program, a variable "bla" will show that the variables are populated.
2. Inside the "Second PC" program, there's the same structure called ST_Record. Random number will be assign to this variable every cycle. Every second, the program will write the value of the variable "record" to the other PC through ADS.


## How ADS works

1. The name of the variable from the first PC to be written is indicated in "TargetVarName". Function block ADSRDWRT with index group "16#F003" will take this variable name and return a handle.
2. Function block ADSWRITE with index group "16#F005" will get access to this variable handle and write a new value of "record" variable
3. Function block ADSWRITE with index group "16#F006" will delete the handle after it finishes writing.


## Application Example

This is useful, for example if you want a backup of all the PLC data inside the computer. Every second, the PLC variable value will be backed up inside the second PC.

Further application example: 

![alt tag](https://puu.sh/siBRl/8bd57b5afa.png)

Load the same program to both PCs. If the 1st PC is connected to the IO (detected from the status of the coupler), execute normal program and backup data to 2nd PC. If the PC is not connected to the IO, don't do anything. 

![alt tag](https://puu.sh/siBXW/f431bee462.png)

If the 1st PC is down, just plug out the Ethernet connection and connect the IO to the 2nd PC, thus the IO will keep running without significant downtime.




