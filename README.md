
[![Arduino CI](https://github.com/RobTillaart/MINMAX/workflows/Arduino%20CI/badge.svg)](https://github.com/marketplace/actions/arduino_ci)
[![Arduino-lint](https://github.com/RobTillaart/MINMAX/actions/workflows/arduino-lint.yml/badge.svg)](https://github.com/RobTillaart/MINMAX/actions/workflows/arduino-lint.yml)
[![JSON check](https://github.com/RobTillaart/MINMAX/actions/workflows/jsoncheck.yml/badge.svg)](https://github.com/RobTillaart/MINMAX/actions/workflows/jsoncheck.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/RobTillaart/MINMAX/blob/master/LICENSE)
[![GitHub release](https://img.shields.io/github/release/RobTillaart/MINMAX.svg?maxAge=3600)](https://github.com/RobTillaart/MINMAX/releases)


# MINMAX

Library for finding peaks (minimum and maximum) in a signal.


## Description

The MINMAX library is a simple peak finder in a stream of floats.

The **add()** function indicates after adding a number if the minimum and/or the
maximum value has been changed by means of a bit flag which is returned.
If a peak is found, it will be used as the new **minimum()** or **maximum()**
until a call to **reset()**.

The library can **reset()** the minimum and maximum to 0 to start again.
The first **add()** after the **reset()** will set the minimum and maximum
to the value added.

The library has the option to auto-reset after a predefined number of **add()** calls.

Finally the library keeps track when the last peaks occurred.


## Interface

#### Core

- **MINMAX** Constructor,
- **uint8_t add(float value)** add next value. Returns status (bit flags), see table below.
- **void reset()** resets the minimum and maximum to 0.
- **float minimum()** returns last minimum. Can be higher than previous call due to **reset()** or **autoReset()**.
If no call to **add()** is made yet it will return 0.
- **float maximum()** returns last maximum. Can be lower than previous call due to **reset()** or **autoReset()**.
If no call to **add()** is made yet it will return 0.
- **lastValue()** returns last value added.


#### AutoReset

- **uint32_t count()** returns number of **add()** calls since last (auto)reset.
- **void setAutoResetCount(uint32_t count)** sets an auto-reset moment after count calls to **add()**.
There will be at least one value processed.
When count is set to 0, there will be no autoReset.
- **uint32_t getAutoResetCount()** returns set value.


#### Timestamps

- **lastMin()** timestamp in millis() when minimum was last updated.
- **lastMax()** timestamp in millis() when maximum was last updated.


#### Return flags add()

Return flags of **add()** - is a bit mask.

|  flag                |  value  |  description      |
|:---------------------|:-------:|:------------------|
|  MINMAX_NO_CHANGE    |  0x00   |  no change        |
|  MINMAX_MIN_CHANGED  |  0x01   |  minimum changed  |
|  MINMAX_MAX_CHANGED  |  0x02   |  maximum changed  |
|  MINMAX_RESET_DONE   |  0x80   |  reset done       |

NOTE: After a reset() the next add() will return both MINMAX_MIN_CHANGED and MINMAX_MAX_CHANGED (0x03)

NOTE: After an autoReset in add() it will return 0x83.

#### CallBack

- **void addCallBack( void (\* func)(void) )** add a function to be called
when the minimum or the maximum has changed.
See examples.


## Obsolete

- **void autoReset(uint32_t count)** obsolete since 0.2.0
Replaced by **void setAutoResetCount()**


## Operation

The examples show the basic working of the functions.


## Future

#### must

#### should
- separate call back for MINMAX_MIN_CHANGED and MINMAX_MAX_CHANGED
- add getLastEvent()?
- add AVG **average()** **sum()**
  - like a digital multimeter (DMM)
  - **sum()** would be sufficient as average can be derived.

#### could
- Template class to allow other types
  - int32_t uint64_t double etc.
  - now you loose precision

#### wont (unless)
- thresholds, windowing + triggers  (separate class?)
- auto-reset after time? (would affect all functions  ?)
  - need a uint32_t start;
  - need a uint32_t threshold;
  - millis() - start > threshold) => action.
  - should be tested for in every function call.



