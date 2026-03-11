## Overview

Library for Controlling DXL from the PC.

## Note

This library has originally created for the Japanese market, all comments within the source code are written in Japanese.

This library has absolutely no relationship with libraries provided by ROBOTIS or similar entities, and therefore no compatibility with them has been considered whatsoever.

Dynamixel supports multiple protocols, but this library is designed for Protocol V2 operating over TTL or RS-485 interfaces. It does not support other protocols.

The actual implementation is nothing special—it just generates frames according to the protocol—but it's become a bit cumbersome because I wanted to write the same code across different platforms.

Regarding Python, I only created a bare-bones ctype wrapper for a library written in C, so looking back now, it's incredibly cumbersome to use.<br>
If you're using Python, pyDXL is far superior.

## Requirement

- Windows, Linux, MacOS
- GCC, Python, Ruby, LabVIEW, etc.
- Serial Interface for Dynamixel

## Usage

The package includes pre-compiled 32-bit and 64-bit DLLs for Windows, so there is no need to rebuild the library.<br>
Please refer to [this guide](https://www.besttechnology.co.jp/modules/knowledge/?Dynamixel%20Protocol%202%20Library) for rebuilding (Japanese only).

### C language
```c
//#define _DYNAMICLOAD
#include  <stdio.h>
#include  "dxlib.h"

int main (void) {
  TDeviceID  dev;

#if defined(_DYNAMICLOAD)
  if (LoadDLL()) {
#endif
    dev = DX_OpenPort ("\\\\.\\COM10", 57600);
    if (dev) {
      /*
        Here is the actual processing for DXL.
      */

      DX_ClosePort (dev);
    }
#if defined(_DYNAMICLOAD)
    UnloadDLL();
  }
#endif
}
```

### Python
```Python
from dxlib import *
dev = DX_OpenPort('/dev/ttyUSB0', 57600)
if dev is not None:
  # Here is the actual processing for DXL.
  DX_ClosePort(dev)
```

## Licence

[MIT](https://github.com/mukyokyo/dynamixel-library-for-arduino/blob/main/LICENSE)
