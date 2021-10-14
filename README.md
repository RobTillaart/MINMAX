
[![Arduino CI](https://github.com/RobTillaart/MINMAX/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/MINMAX/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/MINMAX.svg?maxAge=3600)](https://github.com/RobTillaart/MINMAX/releases)

# MINMAX

Library for finding peaks ( minimum and maximum) in signal.

## Description

The MINMAX 


## Interface

- **MINMAX** Constructor
- **uint8_t add(float f)** add next value. Returns status (flags), see table below.
- **void reset()** resets the minimum and maximum 
- **void autoreset(uint32_t cnt)**
- **float minimum()**
- **float maximum()**
- **uint32_t count()**


| flag | description     |
|:----:|:----------------|
| 0x00 | no change       |
| 0x01 | minimum changed |
| 0x02 | maximum changed |
| 0x80 | reset done      |


## Operation

The examples show the basic working of the functions.


## Future

- update documentation
- define FLAGS
- add call back functions?

