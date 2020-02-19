# IO
This is the io template of InHand InGateway900 products, we provide some python APIs you can earsily used in you IoT solutions.
## Contents


<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->
  - [Usage](#usage)
    - [Getting Started](#getting-started)
      - [get io list](#get-io-list)
      - [set mode of digital io](#set-mode-of-digital-io)
      - [read io](#read-io)
    - [IO](#io-1)
    - [Constructor Example](#constructor-example)
  - [API Reference](#api-reference)
    - [get_io_list()](#get_io_list)
    - [get_io_info(io_name)](#get_io_infoio_name)
    - [get_all_io_info(io_name)](#get_all_io_infoio_name)
    - [setup_digital_io(io_name="di1", direction=INPUT_DIRECTION, mode=DIGITAL_DRY_CONTACT_MODE)](#setup_digital_ioio_namedi1-directioninput_direction-modedigital_dry_contact_mode)
    - [setup_analog_io(io_name="ai1",  mode=ANALOG_HIGH_V_MODE)](#setup_analog_ioio_nameai1-modeanalog_high_v_mode)
    - [read_io("di1")](#read_iodi1)
    - [mwrite_io(io_name=”di2”, value=DRY_CONTACT_HIGH_VALUE)](#mwrite_ioio_namedi2-valuedry_contact_high_value)

<!-- /code_chunk_output -->




## Usage
### Getting Started
#### get io list
Here is a very simple example that shows how to get io list.
``` python
from mobiuspi_lib.io import IO

# you can use io as an instance of IO class
io = IO()

# get io list
io_list = io.get_io_list()
print("io_list: %s " %  (io_list, ))
```
And the results are as follows:
``` python
#IG902 has 4 digital inputs, 2 digital outputs and 2 analog inputs
io_list: [u'di1', u'di2', u'di3', u'di4', u'do1', u'do2', u'ai1', u'ai2']
```

#### set mode of digital io
Here is a very simple example that shows how to set mode of digital io.
``` python
from mobiuspi_lib.io import IO, INPUT_DIRECTION, DIGITAL_DRY_CONTACT_MODE

#you can use io as an instance of IO class
io = IO()

# set mode of digital io 1, before you read io you should call this function firstly to set io mode and direction 
sdi = io.setup_digital_io(io_name='di1', direction=INPUT_DIRECTION, mode=DIGITAL_DRY_CONTACT_MODE)
print("sdi: %s" % sdi)
```
And the results are as follows:
``` python
#Digital input 1 mode is drycontact
sdi: {u'index': 1, u'type': u'digital input', u'name': u'di1', u'mode': u'drycontact'}
```

#### read io
Here is a very simple example that shows how to read io.
``` python
from mobiuspi_lib.io import IO

#you can use io as an instance of IO class
io = IO()

# read io 
ri = io.read_io('di1')
print("ri: %s" % ri)
```
And the results are as follows:
``` python
#Digital input 1 level status is high level
ri: HIGH
```

### IO

You can use the io class as an instance, within a class or by subclassing. The general usage flow is as follows:

* Create an io instance
* Get io list of the ``get_io_list()`` functions
* Use ``setup_digital_io()`` to set digital io
* Use ``setup_analog_io()`` to set analog io
* Get io info of the ``get_io_info()`` functions
* Get all io info of the ``get_all_io_info()`` functions
* Use ``read_io()`` to read io
* Use ``write_io()`` to write io

### Constructor Example

``` python
from mobiuspi_lib.io import IO

#method1, set default ip:127.0.0.1, port:48888
io = IO()

#method2, set the custom ip and port
ip = "127.0.0.1"
#port should be string
port = "48888"
io = IO(ip=ip,port=port)
```

## API Reference
### get_io_list()
Get IO list.
- parameter

  None  

- return value  

        ["di1", "di2", "di3", "di4", "do1", "do2", "ai1", "ai2"]

### get_io_info(io_name)
Get the information of the IO.
- parameter
  
  `io_name`: the name of io which you can call get_io_list function to get.  

- return value
  
        {   
            "name": "di1",
            "type": "digital input",
            "mode": "shutdown",
            "index": 1,
        }

### get_all_io_info(io_name)
Get the information of all IO.
- parameter  
  
  None  

- return value  

        {
            "di1": {
                "name": "di1",
                "type": "digital input",
                "mode": "shutdown",
                "index": 1
            },
            "di2": {
                "name": "di2",
                "index": 2,
                "type": "digital input",
                "mode": "shutdown"
            },
            "di3": {
                "name": "di3",
                "index": 3,
                "type": "digital input",
                "mode": "shutdown",
            },
            "di4": {
                "name": "di4",
                "index": 4,
                "type": "digital input",
                "mode": "shutdown",
            },
            "do1": {
                "name": "do1",
                "index": 1,
                "type": "digital output"
            },
            "do2": {
                "name": "do2",
                "index": 2,
                "type": "digital output"
            },
            "ai1": {
                "name": "ai1",
                "index": 1,
                "type": "analog input"
            },
            "ai2": {
                "name": "ai2",
                "index": 2,
                "type": "analog input"
            }
        }

### setup_digital_io(io_name="di1", direction=INPUT_DIRECTION, mode=DIGITAL_DRY_CONTACT_MODE)
Set direction and mode of digital IO.
- parameter  
  
  `io_name`: the name of digital io which you can call get_io_list function to get.  <br/>

  `direction`: INPUT_DIRECTION or OUTPUT_DIRECTION.  <br/>

  `mode`: DIGITAL_DRY_CONTACT_MODE or DIGITAL_WET_CONTACT_MODE.  

- return value  

        {
            "name": "di1",
            "type": "digital input",
            "mode": "shutdown",
            "index": 1,
        }

### setup_analog_io(io_name="ai1",  mode=ANALOG_HIGH_V_MODE)
Set direction and mode of analog IO.
- parameter  

  `io_name`: the name of analog io which you can call get_io_list function to get.  

  `mode`:  
    - ANALOG_LOW_A_MODE = "0_20mA"  
    - ANALOG_HIGH_A_MODE = "4_20mA"  
    - ANALOG_LOW_V_MODE = "0_5V"  
    - ANALOG_HIGH_V_MODE = "0_10V"  

- return value  
  
        {
            "name": "ai1",
            "type": "analog input",
            "mode": "shutdown",
            "index": 1,
        }

### read_io("di1")
Read the infomation of IO.
- parameter  
  
  `io_name`: the name of analog io which you can call get_io_list function to get, and make sure you shuould rea4td value from input io.  

- return value  

        "HIGH"
        "LOW"
        "ON"
        "OFF"

### mwrite_io(io_name=”di2”, value=DRY_CONTACT_HIGH_VALUE)
Write value to IO.
- parameter  
  
  `io_name`: the name of analog io which you can call get_io_list function to get, and make sure you shuould write value to output io.  
`value`:  
    - DRY_CONTACT_HIGH_VALUE = "HIGH"  
    - DRY_CONTACT_LOW_VALUE = "LOW"  
    - WET_CONTACT_ON = "ON"  
    - WET_CONTACT_OFF = "OFF"

- return value  
  
        True / False